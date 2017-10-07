---
title: "Data Lake Store ile Sqoop kullanarak Azure SQL veritabanı arasında aaaCopy veri | Microsoft Docs"
description: "Azure SQL veritabanı ve Data Lake Store arasında Sqoop toocopy veri kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="18ee8-103">Data Lake Store ile Sqoop kullanarak Azure SQL veritabanı arasında veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="18ee8-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="18ee8-104">Bilgi nasıl Azure SQL veritabanı ve Data Lake Store arasında toouse Apache Sqoop tooimport ve dışarı aktarma veri.</span><span class="sxs-lookup"><span data-stu-id="18ee8-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="18ee8-105">Sqoop nedir?</span><span class="sxs-lookup"><span data-stu-id="18ee8-105">What is Sqoop?</span></span>
<span data-ttu-id="18ee8-106">Büyük veri uygulamaları günlükleri ve dosyaları gibi yapılandırılmamış ve yarı yapılandırılmış veri işleme için doğal bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="18ee8-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="18ee8-107">Ancak, aynı zamanda olabilir ilişkisel veritabanlarında depolanan bir gereksinim tooprocess yapılandırılmış veri.</span><span class="sxs-lookup"><span data-stu-id="18ee8-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="18ee8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) tasarlanmış aracı tootransfer ilişkisel veritabanları ve Data Lake Store gibi bir büyük veri deposu arasındaki verilerdir.</span><span class="sxs-lookup"><span data-stu-id="18ee8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="18ee8-109">Bunu Azure SQL veritabanı gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) tooimport verileri Data Lake Store kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18ee8-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="18ee8-110">Ardından dönüştürme ve büyük veri iş yüklerini kullanarak hello verileri analiz ve bir RDBMS hello verilerini dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="18ee8-111">Bu öğreticide, ilişkisel veritabanı tooimport/verme etki alanından farklı bir Azure SQL Database kullanın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18ee8-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="18ee8-112">Prerequisites</span></span>
<span data-ttu-id="18ee8-113">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="18ee8-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="18ee8-114">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="18ee8-114">**An Azure subscription**.</span></span> <span data-ttu-id="18ee8-115">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18ee8-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="18ee8-116">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="18ee8-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="18ee8-117">Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="18ee8-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="18ee8-118">**Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="18ee8-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="18ee8-119">Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18ee8-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="18ee8-120">Bu makalede, Data Lake Store erişimi olan bir Hdınsight Linux kümesi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="18ee8-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="18ee8-121">**Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="18ee8-121">**Azure SQL Database**.</span></span> <span data-ttu-id="18ee8-122">Yönergeler için toocreate bir, bkz: [bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="18ee8-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="18ee8-123">Videolarla daha hızlı mı öğreniyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="18ee8-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="18ee8-124">[Bu videoyu izleyin](https://mix.office.com/watch/1butcdjxmu114) nasıl toocopy verileri Azure Storage Bloblarında ve Distcp'yi kullanarak Data Lake Store arasında.</span><span class="sxs-lookup"><span data-stu-id="18ee8-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="18ee8-125">Örnek tablo hello Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18ee8-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="18ee8-126">toostart ile iki örnek tablolar hello Azure SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="18ee8-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="18ee8-127">Kullanım [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) veya Visual Studio tooconnect toohello Azure SQL veritabanı ve sonra çalışma hello aşağıdaki sorgular.</span><span class="sxs-lookup"><span data-stu-id="18ee8-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="18ee8-128">**Tablo1 oluşturma**</span><span class="sxs-lookup"><span data-stu-id="18ee8-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="18ee8-129">**Tablo2 oluşturma**</span><span class="sxs-lookup"><span data-stu-id="18ee8-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="18ee8-130">İçinde **tablo1**, bazı örnek veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="18ee8-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="18ee8-131">Bırakın **tablo2** boş.</span><span class="sxs-lookup"><span data-stu-id="18ee8-131">Leave **Table2** empty.</span></span> <span data-ttu-id="18ee8-132">Verileri içeri aktaracak **tablo1** Data Lake Store içine.</span><span class="sxs-lookup"><span data-stu-id="18ee8-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="18ee8-133">Ardından, biz veri Data Lake Store verilecek **tablo2**.</span><span class="sxs-lookup"><span data-stu-id="18ee8-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="18ee8-134">Aşağıdaki kod parçacığında hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="18ee8-135">Kullanım Sqoop bir Hdınsight kümesini gelen erişim tooData Lake deposu</span><span class="sxs-lookup"><span data-stu-id="18ee8-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="18ee8-136">Hdınsight kümesi hello Sqoop paketler zaten var.</span><span class="sxs-lookup"><span data-stu-id="18ee8-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="18ee8-137">Ek depolama alanı hello Hdınsight küme toouse Data Lake Store yapılandırdıysanız, ilişkisel veritabanı (Bu örnekte, Azure SQL veritabanı) arasında (olmadan herhangi bir yapılandırma değişikliği) Sqoop tooimport/dışarı aktarma veri kullanabilirsiniz ve Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="18ee8-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="18ee8-138">Bu öğretici için SSH tooconnect toohello küme kullanması gereken şekilde Linux kümesi oluşturulan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="18ee8-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="18ee8-139">Bkz: [Bağlan tooa Linux tabanlı Hdınsight kümesi](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="18ee8-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="18ee8-140">Merhaba kümeden hello Data Lake Store hesabı erişip erişemeyeceğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="18ee8-141">Merhaba SSH isteminden komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="18ee8-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="18ee8-142">Bu dosyalar/klasörler hello Data Lake Store hesabı içinde listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18ee8-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="18ee8-143">Data Lake Store Azure SQL veritabanından veri içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="18ee8-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="18ee8-144">Sqoop paketlerinin kullanılabildiği toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="18ee8-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="18ee8-145">Genellikle, bu anda olacaktır `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="18ee8-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="18ee8-146">Merhaba verileri alın **tablo1** hello Data Lake Store hesabı içine.</span><span class="sxs-lookup"><span data-stu-id="18ee8-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="18ee8-147">Sözdizimi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="18ee8-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="18ee8-148">Unutmayın **sql veritabanı sunucusu adı** yer tutucu hello hello Azure SQL veritabanı çalıştığı hello sunucusunun adını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="18ee8-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="18ee8-149">**SQL veritabanı adı** yer tutucu hello gerçek veritabanı adını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="18ee8-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="18ee8-150">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="18ee8-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="18ee8-151">Veriler o hello toohello Data Lake Store hesabına transfer doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="18ee8-152">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="18ee8-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="18ee8-153">Çıktı aşağıdaki hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="18ee8-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="18ee8-154">Her **bölümü-m -*** dosya tooa satır hello kaynak tablosunda karşılık gelen **tablo1**.</span><span class="sxs-lookup"><span data-stu-id="18ee8-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="18ee8-155">Merhaba bölümünün - m - hello içeriğini görüntüleyebilir * tooverify dosyaları.</span><span class="sxs-lookup"><span data-stu-id="18ee8-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="18ee8-156">Data Lake Store Azure SQL veritabanına verileri dışa</span><span class="sxs-lookup"><span data-stu-id="18ee8-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="18ee8-157">Data Lake Store hesabı toohello boş tablosundan Hello verilerini dışa **tablo2**, hello Azure SQL veritabanı içinde.</span><span class="sxs-lookup"><span data-stu-id="18ee8-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="18ee8-158">Sözdizimi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="18ee8-159">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="18ee8-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="18ee8-160">Veri olan bu hello toohello SQL veritabanı tablosu karşıya doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="18ee8-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="18ee8-161">Kullanım [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) veya Visual Studio tooconnect toohello Azure SQL veritabanı ve sonra çalışma hello aşağıdaki sorgu.</span><span class="sxs-lookup"><span data-stu-id="18ee8-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="18ee8-162">Çıktı aşağıdaki hello sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="18ee8-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="18ee8-163">Sqoop kullanırken performans etkenleri</span><span class="sxs-lookup"><span data-stu-id="18ee8-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="18ee8-164">Performans, Sqoop ayarlama toocopy veri tooData Lake deposu işi için bkz: [Sqoop performans belge](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="18ee8-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="18ee8-165">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="18ee8-165">See also</span></span>
* [<span data-ttu-id="18ee8-166">Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="18ee8-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="18ee8-167">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="18ee8-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="18ee8-168">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="18ee8-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="18ee8-169">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="18ee8-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
