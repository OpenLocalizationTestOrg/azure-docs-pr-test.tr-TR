---
title: "Apache Sqoop Hadoop - Azure Hdınsight ile | Microsoft Docs"
description: "Apache Sqoop hdınsight'ta Hadoop ve bir Azure SQL veritabanı arasında almak ve vermek için nasıl kullanılacağını öğrenin."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: 35dcbb91e6af1480685c9fd5b829c54277c1c605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="8b657-104">İçeri ve dışarı aktarma hdınsight'ta Hadoop ile SQL veritabanı arasında veri için Apache Sqoop'u kullanın</span><span class="sxs-lookup"><span data-stu-id="8b657-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="8b657-105">Apache Sqoop Azure hdınsight'ta Hadoop kümesi ve Azure SQL Database veya Microsoft SQL Server veritabanı arasında almak ve vermek için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8b657-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="8b657-106">Bu adımlarda belge kullanımı `sqoop` Hadoop kümesi headnode doğrudan komutu.</span><span class="sxs-lookup"><span data-stu-id="8b657-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="8b657-107">SSH baş düğümüne bağlanmak ve bu belgede komutları çalıştırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b657-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b657-108">Bu belgede yer alan adımlar, yalnızca Linux kullanmak Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="8b657-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="8b657-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="8b657-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8b657-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8b657-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="8b657-111">Ücretsiz yükleyin</span><span class="sxs-lookup"><span data-stu-id="8b657-111">Install FreeTDS</span></span>

1. <span data-ttu-id="8b657-112">SSH Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="8b657-112">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="8b657-113">Örneğin, aşağıdaki komutu adlı bir küme için birincil headnode bağlayan `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="8b657-113">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="8b657-114">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8b657-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8b657-115">Ücretsiz yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b657-115">Use the following command to install FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="8b657-116">Ücretsiz birkaç adımda SQL veritabanına bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b657-116">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="8b657-117">SQL veritabanı tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b657-117">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b657-118">Hdınsight kümesi kullanıyorsanız ve SQL veritabanı oluşturuldu [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md), bu bölümdeki adımları atlayın.</span><span class="sxs-lookup"><span data-stu-id="8b657-118">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="8b657-119">Veritabanı ve tablo adımlarda bir parçası olarak oluşturulan [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md) belge.</span><span class="sxs-lookup"><span data-stu-id="8b657-119">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="8b657-120">SSH oturumundan SQL veritabanı sunucusuna bağlanmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b657-120">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="8b657-121">Aşağıdakine benzer bir çıktı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="8b657-121">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="8b657-122">Konumundaki `1>` isteminde, aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="8b657-122">At the `1>` prompt, enter the following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="8b657-123">Zaman `GO` deyimi girilir, önceki deyimleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8b657-123">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="8b657-124">İlk olarak, **mobiledata** tablosu oluşturulur ve kümelenmiş bir dizin (SQL veritabanı tarafından gereklidir.) kendisine eklenir</span><span class="sxs-lookup"><span data-stu-id="8b657-124">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="8b657-125">Tablo oluşturulduğunu doğrulamak için aşağıdaki sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b657-125">Use the following query to verify that the table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="8b657-126">Aşağıdakine benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="8b657-126">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="8b657-127">Girin `exit` adresindeki `1>` tsql yardımcı programı'ndan çıkmak komut istemi.</span><span class="sxs-lookup"><span data-stu-id="8b657-127">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="8b657-128">Sqoop dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="8b657-128">Sqoop export</span></span>

1. <span data-ttu-id="8b657-129">Kümeye SSH bağlantısı Sqoop SQL veritabanınız görebildiğini doğrulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b657-129">From the SSH connection to the cluster, use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="8b657-130">İstendiğinde, SQL veritabanı oturum açma için parola girin.</span><span class="sxs-lookup"><span data-stu-id="8b657-130">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="8b657-131">Bu komut veritabanları dahil olmak üzere, bir listesini döndürür **sqooptest** daha önce oluşturduğunuz veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8b657-131">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="8b657-132">Verileri dışarı aktarmak için **hivesampletable** için **mobiledata** tablo, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b657-132">To export data from **hivesampletable** to the **mobiledata** table, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="8b657-133">Bu komut bağlanmak için Sqoop bildirir **sqooptest** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8b657-133">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="8b657-134">Sqoop sonra verileri dışa aktarır **wasb: / / / hive/ambarı/hivesampletable** için **mobiledata** tablo.</span><span class="sxs-lookup"><span data-stu-id="8b657-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8b657-135">Kullanım `wasb:///` kümeniz için varsayılan depolama bir Azure depolama hesabı ise.</span><span class="sxs-lookup"><span data-stu-id="8b657-135">Use `wasb:///` if the default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="8b657-136">Kullanım `adl:///` bir Azure Data Lake Store ise.</span><span class="sxs-lookup"><span data-stu-id="8b657-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="8b657-137">Komut tamamlandığında, TSQL kullanılarak veritabanına bağlanmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b657-137">After the command completes, use the following command to connect to the database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="8b657-138">Bağlantı kurulduktan sonra verileri dışarı aktarılan doğrulamak için aşağıdaki ifadeleri kullanın **mobiledata** tablosu:</span><span class="sxs-lookup"><span data-stu-id="8b657-138">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="8b657-139">Tablosunda veri listesini görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="8b657-139">You should see a listing of data in the table.</span></span> <span data-ttu-id="8b657-140">Tür `exit` tsql yardımcı programı'ndan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="8b657-140">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="8b657-141">Sqoop alma</span><span class="sxs-lookup"><span data-stu-id="8b657-141">Sqoop import</span></span>

1. <span data-ttu-id="8b657-142">Verileri içe aktarmak için aşağıdaki komutu kullanın **mobiledata** SQL veritabanında çok tablo **wasb: / / / öğreticileri/usesqoop/importeddata** hdınsight'ta dizin:</span><span class="sxs-lookup"><span data-stu-id="8b657-142">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="8b657-143">Veri alanları bir sekme karakteriyle ayrılır ve satırları yeni satır karakteri tarafından sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8b657-143">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="8b657-144">Alma işlemi tamamlandıktan sonra yeni bir dizinde liste veri çıkışı için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b657-144">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="8b657-145">SQL Server kullanma</span><span class="sxs-lookup"><span data-stu-id="8b657-145">Using SQL Server</span></span>

<span data-ttu-id="8b657-146">Sqoop, veri merkezinizdeki veya Azure üzerinde barındırılan bir sanal makinede SQL Server'dan veri vermek ve almak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b657-146">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="8b657-147">SQL Database ve SQL Server kullanımı arasındaki farklılıklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8b657-147">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="8b657-148">Hdınsight ve SQL Server aynı Azure sanal ağ üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b657-148">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="8b657-149">Bir örnek için bkz: [şirket içi ağınıza bağlanmak Hdınsight](./connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="8b657-149">For an example, see the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="8b657-150">Hdınsight Azure sanal ağı ile kullanma hakkında daha fazla bilgi için bkz: [genişletmek Hdınsight Azure sanal ağ ile](hdinsight-extend-hadoop-virtual-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="8b657-150">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="8b657-151">Azure sanal ağ ile ilgili daha fazla bilgi için bkz: [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md) belge.</span><span class="sxs-lookup"><span data-stu-id="8b657-151">For more information on Azure Virtual Network, see the [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="8b657-152">SQL Server, SQL kimlik doğrulaması izin verecek şekilde yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b657-152">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="8b657-153">Daha fazla bilgi için bkz: [bir kimlik doğrulama modu seçme](https://msdn.microsoft.com/ms144284.aspx) belge.</span><span class="sxs-lookup"><span data-stu-id="8b657-153">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="8b657-154">SQL Server'ın uzak bağlantıları kabul edecek şekilde yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8b657-154">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="8b657-155">Daha fazla bilgi için bkz: [SQL Server veritabanı altyapısına bağlanma ile ilgili sorunları giderme](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) belge.</span><span class="sxs-lookup"><span data-stu-id="8b657-155">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="8b657-156">Oluşturma **sqooptest** gibi bir yardımcı programını kullanarak SQL Server veritabanında **SQL Server Management Studio** veya **tsql**.</span><span class="sxs-lookup"><span data-stu-id="8b657-156">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="8b657-157">Azure CLI kullanarak için adımlar, yalnızca Azure SQL veritabanı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8b657-157">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="8b657-158">Oluşturmak için aşağıdaki Transact-SQL deyimi kullanın **mobiledata** tablosu:</span><span class="sxs-lookup"><span data-stu-id="8b657-158">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="8b657-159">SQL Server'a Hdınsight'ta bağlanırken, SQL Server'ın IP adresi kullanmak zorunda kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b657-159">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="8b657-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8b657-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="8b657-161">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="8b657-161">Limitations</span></span>

* <span data-ttu-id="8b657-162">Toplu export - ile Linux tabanlı Hdınsight, Microsoft SQL Server veya Azure SQL veritabanı için verileri dışa aktarmak için kullanılan Sqoop bağlayıcı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="8b657-162">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="8b657-163">-Kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop yapar INSERT işlemlerine toplu işleme yerine birden çok ekler.</span><span class="sxs-lookup"><span data-stu-id="8b657-163">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b657-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b657-164">Next steps</span></span>

<span data-ttu-id="8b657-165">Şimdi Sqoop kullanma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="8b657-165">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="8b657-166">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="8b657-166">To learn more, see:</span></span>

* <span data-ttu-id="8b657-167">[Hdınsight ile Oozie kullanma][hdinsight-use-oozie]: Oozie iş akışında kullanmak Sqoop eylem.</span><span class="sxs-lookup"><span data-stu-id="8b657-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="8b657-168">[Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-data]: uçuş çözümlemek için kullanmak Hive gecikme veri ve bir Azure SQL veritabanına veri vermek için Sqoop kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b657-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="8b657-169">[Verileri Hdınsight'a yükleme][hdinsight-upload-data]: Hdınsight/Azure Blob depolama alanına veri yüklemek için diğer yöntemler bulun.</span><span class="sxs-lookup"><span data-stu-id="8b657-169">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
