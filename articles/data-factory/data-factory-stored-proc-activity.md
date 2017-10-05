---
title: "SQL Server saklı yordam etkinliği"
description: "SQL Server saklı yordam etkinliği bir saklı yordam bir Azure SQL Database veya Azure SQL veri ambarı Data Factory işlem hattı çağırmak için nasıl kullanabileceğinizi öğrenin."
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="9f878-103">SQL Server saklı yordam etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9f878-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9f878-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9f878-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9f878-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9f878-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9f878-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9f878-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9f878-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9f878-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9f878-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9f878-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="9f878-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="9f878-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9f878-114">Overview</span></span>
<span data-ttu-id="9f878-115">Veri fabrikasında veri dönüştürme etkinlikleri kullanma [ardışık düzen](data-factory-create-pipelines.md) dönüştürmek ve Öngörüler ve öngörü ham verileri işlemek için.</span><span class="sxs-lookup"><span data-stu-id="9f878-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="9f878-116">Saklı yordam etkinliği Data Factory destekleyen dönüştürme etkinlikleri biridir.</span><span class="sxs-lookup"><span data-stu-id="9f878-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="9f878-117">Bu makalede derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve veri fabrikası'nda desteklenen dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="9f878-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="9f878-118">Kuruluşunuzdaki veya bir Azure sanal makine (VM) üzerinde bir saklı yordam aşağıdaki veri depolarına birinde çağırmak için saklı yordam etkinliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9f878-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="9f878-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9f878-119">Azure SQL Database</span></span>
- <span data-ttu-id="9f878-120">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="9f878-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="9f878-121">SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="9f878-121">SQL Server Database.</span></span>  <span data-ttu-id="9f878-122">SQL Server kullanıyorsanız, veri yönetimi ağ geçidi veritabanını barındıran aynı makine üzerindeki veya veritabanına erişimi ayrı bir makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f878-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="9f878-123">Veri Yönetimi ağ geçidi, veri bağlayan bir bileşen şirket içi/açma Azure VM bulut Hizmetleri ile güvenli ve yönetilen bir şekilde kaynakları ' dir.</span><span class="sxs-lookup"><span data-stu-id="9f878-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="9f878-124">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="9f878-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f878-125">Azure SQL Database veya SQL Server veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSink** kullanarak bir saklı yordam çağrılacak kopyalama etkinliğinde **sqlWriterStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9f878-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="9f878-126">Daha fazla bilgi için bkz: [çağırma kopyalama etkinliği bir saklı yordamdan](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="9f878-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="9f878-127">Bağlayıcı makaleler özelliği hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9f878-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="9f878-128">Kopyalama etkinliği kullanarak bir Azure SQL Data Warehouse'a veri kopyalama sırasında bir saklı yordam çağırma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9f878-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="9f878-129">Ancak, SQL Data Warehouse saklı yordama çağırmak için saklı yordam etkinliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f878-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="9f878-130">Azure SQL Database veya SQL Server veya Azure SQL Data Warehouse veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSource** kullanarak kaynak veritabanından veri okumak için bir saklı yordam çağrılacak kopyalama etkinliğinde  **sqlReaderStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9f878-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="9f878-131">Daha fazla bilgi için aşağıdaki bağlayıcı makalelerine bakın: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL veri ambarı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="9f878-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="9f878-132">Aşağıdaki örneklerde saklı yordam etkinliği bir Azure SQL veritabanındaki bir saklı yordam çağırmak için bir işlem hattı kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f878-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="9f878-133">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="9f878-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="9f878-134">Örnek tablo ve saklı yordam</span><span class="sxs-lookup"><span data-stu-id="9f878-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="9f878-135">Aşağıdaki oluşturma **tablo** SQL Server Management Studio veya tanımanız başka bir araç kullanarak, Azure SQL veritabanındaki.</span><span class="sxs-lookup"><span data-stu-id="9f878-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="9f878-136">Tarih ve saat karşılık gelen kimliği oluşturulduğunda datetimestamp bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="9f878-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="9f878-137">Kimliği tanımlanan benzersizdir ve karşılık gelen kimliği oluşturulduğunda saat ve tarihi datetimestamp sütundur.</span><span class="sxs-lookup"><span data-stu-id="9f878-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Örnek veriler](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="9f878-139">Bu örnekte, bir Azure SQL veritabanında saklı yordamı vardır.</span><span class="sxs-lookup"><span data-stu-id="9f878-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="9f878-140">Saklı yordam bir Azure SQL veri ambarı ve SQL Server veritabanı varsa, benzer bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="9f878-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="9f878-141">SQL Server veritabanı için yüklemeniz gereken bir [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9f878-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="9f878-142">Aşağıdaki oluşturma **saklı yordamı** için verileri ekler **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="9f878-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="9f878-143">**Ad** ve **büyük/küçük harf** (Bu örnekte DateTime) parametresinin parametre ardışık düzen/JSON etkinliğinde belirtilen eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="9f878-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="9f878-144">Saklı yordam tanımı'nda emin  **@**  parametresi için bir önek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f878-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="9f878-145">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f878-145">Create a data factory</span></span>
1. <span data-ttu-id="9f878-146">[Azure portalı](https://portal.azure.com/)’nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9f878-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f878-147">Tıklatın **yeni** sol menüsünde **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="9f878-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Yeni veri fabrikası](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="9f878-149">İçinde **yeni data factory** dikey penceresinde girin **SProcDF** adı.</span><span class="sxs-lookup"><span data-stu-id="9f878-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="9f878-150">Azure Data Factory adları **genel benzersiz**.</span><span class="sxs-lookup"><span data-stu-id="9f878-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="9f878-151">Veri Fabrikası adı Fabrika başarılı oluşturulmasını sağlamak üzere sizin adınızla öneki gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f878-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Yeni veri fabrikası](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="9f878-153">Seçin, **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="9f878-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="9f878-154">İçin **kaynak grubu**, aşağıdaki adımlardan birini yapın:</span><span class="sxs-lookup"><span data-stu-id="9f878-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="9f878-155">Tıklatın **Yeni Oluştur** ve kaynak grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9f878-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="9f878-156">Tıklatın **var olanı kullan** ve varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="9f878-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="9f878-157">Data factory için **konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="9f878-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="9f878-158">Seçin **panoya Sabitle** böylece oturum sonraki açışınızda Panoda data factory görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f878-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="9f878-159">**Yeni data factory** dikey penceresinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f878-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="9f878-160">Oluşturulmakta veri fabrikası gördüğünüz **Pano** Azure portalının.</span><span class="sxs-lookup"><span data-stu-id="9f878-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="9f878-161">Data factory sorunsuz oluşturulduktan sonra data factory sayfasını görürsünüz, burada size data factory içeriği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9f878-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Data Factory giriş sayfası](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="9f878-163">Bir Azure SQL bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f878-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="9f878-164">Veri Fabrikası oluşturduktan sonra bir Azure SQL oluşturun sampletable tablo ve sp_sample içeren Azure SQL veritabanınızı bağlantılar bağlantılı hizmet saklı yordamı, veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="9f878-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="9f878-165">Tıklatın **yazar ve dağıtma** üzerinde **Data Factory** dikey **SProcDF** Data Factory düzenleyiciyi başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="9f878-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="9f878-166">Tıklatın **yeni veri deposu** komut çubuğu ve seçin **Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="9f878-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="9f878-167">Düzenleyicide Azure SQL bağlı hizmeti oluşturmak için JSON betiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f878-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Yeni veri deposu](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="9f878-169">JSON komut dosyasında aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="9f878-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="9f878-170">Değiştir `<servername>` Azure SQL veritabanı sunucunuzun adını.</span><span class="sxs-lookup"><span data-stu-id="9f878-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="9f878-171">Değiştir `<databasename>` içinde oluşturduğunuz tablo ve saklı yordamı veritabanı ile.</span><span class="sxs-lookup"><span data-stu-id="9f878-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="9f878-172">Değiştir `<username@servername>` veritabanına erişimi olan kullanıcı hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="9f878-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="9f878-173">Değiştir `<password>` kullanıcı hesabı için parola ile.</span><span class="sxs-lookup"><span data-stu-id="9f878-173">Replace `<password>` with the password for the user account.</span></span>

      ![Yeni veri deposu](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="9f878-175">Bağlantılı hizmet dağıtmak için **dağıtma** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9f878-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="9f878-176">AzureSqlLinkedService soldaki ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9f878-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![bağlantılı hizmet bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="9f878-178">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f878-178">Create an output dataset</span></span>
<span data-ttu-id="9f878-179">Saklı yordam herhangi bir veri üretmez olsa bile bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f878-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="9f878-180">Etkinlik (ne sıklıkta etkinlik - saatlik çalıştırılır, günlük, vb.) zamanlamasını sürücüleri çıktı veri kümesi olduğundan olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="9f878-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="9f878-181">Çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** bir Azure SQL Database veya bir Azure SQL Data Warehouse veya çalıştırmak için saklı yordam istediğiniz SQL Server veritabanı başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="9f878-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="9f878-182">Çıktı veri kümesi için saklı yordam sonucunu başka bir etkinlik tarafından işleme sonraki geçirmek için bir yol olarak hizmet verebilir ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="9f878-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="9f878-183">Ancak, veri fabrikası otomatik olarak bir saklı yordam çıktısını bu veri kümesine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="9f878-184">Çıktı veri kümesi işaret eden bir SQL tablosuna Yazar saklı yordam değil.</span><span class="sxs-lookup"><span data-stu-id="9f878-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="9f878-185">Bazı durumlarda, çıktı veri kümesi olabilir bir **kukla dataset** (gerçekten saklı yordamı çıktısını tutmaz bir tabloya işaret eden bir veri kümesi).</span><span class="sxs-lookup"><span data-stu-id="9f878-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="9f878-186">Sahte bu veri kümesi yalnızca saklı yordam etkinliği çalıştırmak için zamanlama belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f878-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="9f878-187">Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** araç çubuğunda tıklatın **yeni veri kümesi**, tıklatıp **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="9f878-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="9f878-188">**Yeni veri kümesi** seçin ve komut çubuğunda **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="9f878-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![bağlantılı hizmet bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="9f878-190">JSON Düzenleyicisi için aşağıdaki JSON komut dosyasında kopyalayıp yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9f878-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="9f878-191">Veri kümesi dağıtmak için **dağıtma** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9f878-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="9f878-192">Veri kümesi ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9f878-192">Confirm that you see the dataset in the tree view.</span></span>

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="9f878-194">SqlServerStoredProcedure etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f878-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="9f878-195">Şimdi, saklı yordam etkinliği ile işlem hattı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="9f878-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="9f878-196">Aşağıdaki özelliklere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9f878-196">Notice the following properties:</span></span> 

- <span data-ttu-id="9f878-197">**Türü** özelliği ayarlanmış **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="9f878-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="9f878-198">**StoredProcedureName** türü özellikleri ayarlanmış **sp_sample** (saklı yordam adı).</span><span class="sxs-lookup"><span data-stu-id="9f878-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="9f878-199">**StoredProcedureParameters** bölüm adlı bir parametre içeren **saniyeyi tarih /**.</span><span class="sxs-lookup"><span data-stu-id="9f878-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="9f878-200">Ad ve büyük/küçük harf JSON içinde parametresinin adını ve büyük/küçük harf saklı yordam tanımındaki parametre eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f878-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="9f878-201">Bir parametre için null başarılı olursa söz dizimini kullanın: `"param1": null` (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="9f878-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="9f878-202">Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** tıklatın ve komut çubuğunda **yeni işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="9f878-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="9f878-203">Aşağıdaki JSON kod parçacığını kopyalayıp yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="9f878-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="9f878-204">İşlem hattını dağıtmak için **dağıtma** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9f878-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="9f878-205">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="9f878-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="9f878-206">Data Factory Düzenleyici dikey penceresini kapatmak ve Data Factory dikey penceresine dönmek için **X** işaretine, sonra da **Diyagram**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f878-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="9f878-208">**Diyagram Görünümü**nde, işlem hatlarına ve bu öğreticide kullanılan veri kümelerine bir genel bakış görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9f878-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="9f878-210">Diyagram Görünümü'nde veri kümesine çift `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="9f878-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="9f878-211">Dilim hazır durumunda bakın.</span><span class="sxs-lookup"><span data-stu-id="9f878-211">You see the slices in Ready state.</span></span> <span data-ttu-id="9f878-212">Başlangıç zamanı ve bitiş zamanı JSON öğesinden arasındaki her bir saat dilimi oluşturduğundan beş dilimler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9f878-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="9f878-214">Bir dilim olduğunda **hazır** Çalıştır durumunda, bir `select * from sampletable` verileri de tabloya saklı yordam tarafından eklenmiş olduğunu doğrulamak için Azure SQL veritabanında sorgu.</span><span class="sxs-lookup"><span data-stu-id="9f878-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Çıktı verileri](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="9f878-216">Bkz: [işlem hattını izleme](data-factory-monitor-manage-pipelines.md) Azure Data Factory işlem hatlarını izleme hakkında ayrıntılı bilgi.</span><span class="sxs-lookup"><span data-stu-id="9f878-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="9f878-217">Bir giriş veri kümesi belirtin</span><span class="sxs-lookup"><span data-stu-id="9f878-217">Specify an input dataset</span></span>
<span data-ttu-id="9f878-218">Kılavuzda saklı yordam etkinliği herhangi bir giriş veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="9f878-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="9f878-219">Bir giriş veri kümesi belirtirseniz, saklı yordam etkinliği girdi veri kümesi dilimin (hazır durumda) kullanılabilir hale gelene kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="9f878-220">Veri kümesi (başka bir etkinliğin aynı ardışık düzen tarafından üretilen değil) bir dış veri kümesi ya da bir Yukarı Akış etkinliği (Bu etkinlik önce çalışır etkinliği) tarafından üretilen bir iç veri kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="9f878-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="9f878-221">Saklı yordam etkinliği için birden çok giriş veri kümesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f878-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="9f878-222">Bunu yaparsanız, yalnızca tüm girdi veri kümesi dilimleri (hazır durumda) kullanılabilir saklı yordam etkinliği çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9f878-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="9f878-223">Girdi veri kümesi saklı yordam, bir parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="9f878-224">Yalnızca saklı yordam etkinliği başlatmadan önce bağımlılık denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f878-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="9f878-225">Diğer etkinliklerle zincirleme</span><span class="sxs-lookup"><span data-stu-id="9f878-225">Chaining with other activities</span></span>
<span data-ttu-id="9f878-226">Bu etkinliği olmayan bir Yukarı Akış etkinliği zincir istiyorsanız, Yukarı Akış etkinliği çıktısını Bu etkinliğin bir giriş olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="9f878-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="9f878-227">Bunu yaptığınızda, saklı yordam etkinliğinin çıkış veri kümesi Yukarı Akış etkinliği (hazır durumunda) kullanılabilir ve Yukarı Akış etkinliği tamamlar kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="9f878-228">Birden çok Yukarı Akış etkinliği çıkış kümelerini saklı yordam etkinliği giriş veri kümeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f878-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="9f878-229">Bunu yaptığınızda, tüm giriş veri kümesi dilimler kullanılabilir olduğunda saklı yordam etkinliği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="9f878-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="9f878-230">Aşağıdaki örnekte, kopya etkinliğinin çıkışıdır: saklı yordam etkinliği bir girdi OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="9f878-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="9f878-231">Bu nedenle, saklı yordam etkinliği kopyalama etkinliği tamamlar ve OutputDataset dilim (hazır durumda) kullanılabilir oluncaya kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="9f878-232">Birden çok giriş veri kümeleri belirtirseniz, saklı yordam etkinliği tüm girdi veri kümesi dilimleri (hazır durumda) kullanılabilir oluncaya kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="9f878-233">Giriş veri kümeleri, doğrudan saklı yordam etkinliği için parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="9f878-234">Etkinlikler zincirleme daha fazla bilgi için bkz: [bir ardışık düzende birden çok etkinlik](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="9f878-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="9f878-235">Benzer şekilde, mağaza yordamı etkinlikle bağlamak için **aşağı akış etkinlikleri** (saklı yordam etkinliği tamamlandıktan sonra çalıştırılan etkinlikleri), bir giriş olarak saklı yordam etkinliğinin çıkış veri kümesi belirtin Ardışık Düzen aşağı akış etkinliğinde.</span><span class="sxs-lookup"><span data-stu-id="9f878-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f878-236">Azure SQL Database veya SQL Server veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSink** kullanarak bir saklı yordam çağrılacak kopyalama etkinliğinde **sqlWriterStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9f878-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="9f878-237">Daha fazla bilgi için bkz: [çağırma kopyalama etkinliği bir saklı yordamdan](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="9f878-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="9f878-238">Özelliği hakkında daha fazla ayrıntı için aşağıdaki bağlayıcı makalelerine bakın: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9f878-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="9f878-239">Azure SQL Database veya SQL Server veya Azure SQL Data Warehouse veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSource** kullanarak kaynak veritabanından veri okumak için bir saklı yordam çağrılacak kopyalama etkinliğinde  **sqlReaderStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9f878-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="9f878-240">Daha fazla bilgi için aşağıdaki bağlayıcı makalelerine bakın: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL veri ambarı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="9f878-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="9f878-241">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="9f878-241">JSON format</span></span>
<span data-ttu-id="9f878-242">Bir saklı yordam etkinliği tanımlamak için JSON biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9f878-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="9f878-243">Aşağıdaki tabloda bu JSON özellikleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="9f878-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="9f878-244">Özellik</span><span class="sxs-lookup"><span data-stu-id="9f878-244">Property</span></span> | <span data-ttu-id="9f878-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9f878-245">Description</span></span> | <span data-ttu-id="9f878-246">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9f878-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f878-247">ad</span><span class="sxs-lookup"><span data-stu-id="9f878-247">name</span></span> | <span data-ttu-id="9f878-248">Etkinlik adı</span><span class="sxs-lookup"><span data-stu-id="9f878-248">Name of the activity</span></span> |<span data-ttu-id="9f878-249">Evet</span><span class="sxs-lookup"><span data-stu-id="9f878-249">Yes</span></span> |
| <span data-ttu-id="9f878-250">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9f878-250">description</span></span> |<span data-ttu-id="9f878-251">Etkinlik hangi amaçla kullanıldığına açıklayan metin</span><span class="sxs-lookup"><span data-stu-id="9f878-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="9f878-252">Hayır</span><span class="sxs-lookup"><span data-stu-id="9f878-252">No</span></span> |
| <span data-ttu-id="9f878-253">type</span><span class="sxs-lookup"><span data-stu-id="9f878-253">type</span></span> | <span data-ttu-id="9f878-254">Ayarlanmalıdır: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="9f878-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="9f878-255">Evet</span><span class="sxs-lookup"><span data-stu-id="9f878-255">Yes</span></span> |
| <span data-ttu-id="9f878-256">Girişleri</span><span class="sxs-lookup"><span data-stu-id="9f878-256">inputs</span></span> | <span data-ttu-id="9f878-257">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="9f878-257">Optional.</span></span> <span data-ttu-id="9f878-258">Bir giriş veri kümesi belirtirseniz, ('Hazır' durumunda) kullanılabilir olmalıdır çalıştırmak saklı yordam etkinliği.</span><span class="sxs-lookup"><span data-stu-id="9f878-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="9f878-259">Girdi veri kümesi saklı yordam, bir parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="9f878-260">Yalnızca saklı yordam etkinliği başlatmadan önce bağımlılık denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f878-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="9f878-261">Hayır</span><span class="sxs-lookup"><span data-stu-id="9f878-261">No</span></span> |
| <span data-ttu-id="9f878-262">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="9f878-262">outputs</span></span> | <span data-ttu-id="9f878-263">Bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f878-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="9f878-264">Çıktı veri kümesi belirtir **zamanlama** saklı yordam etkinliği (saatlik, haftalık, aylık, vb.).</span><span class="sxs-lookup"><span data-stu-id="9f878-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="9f878-265">Çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** bir Azure SQL Database veya bir Azure SQL Data Warehouse veya çalıştırmak için saklı yordam istediğiniz SQL Server veritabanı başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="9f878-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="9f878-266">Çıktı veri kümesi için saklı yordam sonucunu başka bir etkinlik tarafından işleme sonraki geçirmek için bir yol olarak hizmet verebilir ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="9f878-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="9f878-267">Ancak, veri fabrikası otomatik olarak bir saklı yordam çıktısını bu veri kümesine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="9f878-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="9f878-268">Çıktı veri kümesi işaret eden bir SQL tablosuna Yazar saklı yordam değil.</span><span class="sxs-lookup"><span data-stu-id="9f878-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="9f878-269">Bazı durumlarda, çıktı veri kümesi olabilir bir **kukla dataset**, yalnızca saklı yordam etkinliği çalıştırmak için zamanlama belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f878-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="9f878-270">Evet</span><span class="sxs-lookup"><span data-stu-id="9f878-270">Yes</span></span> |
| <span data-ttu-id="9f878-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="9f878-271">storedProcedureName</span></span> |<span data-ttu-id="9f878-272">Azure SQL veya çıktı tablosu kullanır bağlantılı hizmet tarafından temsil edilen Azure SQL Data Warehouse veya SQL Server veritabanı içinde saklı yordamın adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9f878-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="9f878-273">Evet</span><span class="sxs-lookup"><span data-stu-id="9f878-273">Yes</span></span> |
| <span data-ttu-id="9f878-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="9f878-274">storedProcedureParameters</span></span> |<span data-ttu-id="9f878-275">Saklı yordam parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="9f878-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="9f878-276">Bir parametre için null geçmesi gerekiyorsa, söz dizimini kullanın: "param1": null (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="9f878-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="9f878-277">Bu özellik kullanma hakkında bilgi edinmek için aşağıdaki örnek bakın.</span><span class="sxs-lookup"><span data-stu-id="9f878-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="9f878-278">Hayır</span><span class="sxs-lookup"><span data-stu-id="9f878-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="9f878-279">Statik değer geçirme</span><span class="sxs-lookup"><span data-stu-id="9f878-279">Passing a static value</span></span>
<span data-ttu-id="9f878-280">Şimdi, şimdi 'örnek belge' adlı bir statik değeri içeren tabloda 'Senaryo' adlı başka bir sütun eklemeyi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9f878-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Örnek veri 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="9f878-282">**Tablo:**</span><span class="sxs-lookup"><span data-stu-id="9f878-282">**Table:**</span></span>

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

<span data-ttu-id="9f878-283">**Saklı yordam:**</span><span class="sxs-lookup"><span data-stu-id="9f878-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="9f878-284">Şimdi, geçirmek **senaryo** parametresi ve değeri saklı yordam etkinliğinden.</span><span class="sxs-lookup"><span data-stu-id="9f878-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="9f878-285">**TypeProperties** önceki örnek bölümünde aşağıdaki kod parçacığını gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9f878-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="9f878-286">**Data Factory veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="9f878-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="9f878-287">**Data Factory işlem hattı**</span><span class="sxs-lookup"><span data-stu-id="9f878-287">**Data Factory pipeline**</span></span>

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