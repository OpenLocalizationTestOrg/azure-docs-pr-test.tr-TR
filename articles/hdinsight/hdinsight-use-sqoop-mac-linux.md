---
title: "aaaApache Hadoop - Azure Hdınsight ile Sqoop | Microsoft Docs"
description: "Bilgi nasıl toouse Apache Sqoop tooimport ve hdınsight'ta Hadoop ile bir Azure SQL veritabanı arasında dışarı aktarma."
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
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="4d6fb-104">Apache Sqoop tooimport kullanın ve hdınsight'ta Hadoop ile SQL veritabanı arasında veri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="4d6fb-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="4d6fb-105">Azure Hdınsight ve Azure SQL Database veya Microsoft SQL Server veritabanı nasıl toouse Apache Sqoop tooimport ve dışarı aktarma arasında bir Hadoop küme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="4d6fb-106">Merhaba adımları bu belgenin kullanımı hello `sqoop` hello Hadoop kümesi hello headnode doğrudan komutu.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="4d6fb-107">SSH tooconnect toohello baş düğüm kullanın ve bu belgede hello komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6fb-108">Merhaba bu belgedeki adımlar yalnızca Linux kullanmak Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="4d6fb-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4d6fb-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4d6fb-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="4d6fb-111">Ücretsiz yükleyin</span><span class="sxs-lookup"><span data-stu-id="4d6fb-111">Install FreeTDS</span></span>

1. <span data-ttu-id="4d6fb-112">SSH tooconnect toohello Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="4d6fb-113">Örneğin, komutu aşağıdaki hello toohello birincil headnode adlı bir kümeye bağlanır `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4d6fb-114">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4d6fb-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4d6fb-115">Aşağıdaki komut tooinstall ücretsiz hello kullan:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="4d6fb-116">Ücretsiz çeşitli adımları tooconnect tooSQL veritabanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="4d6fb-117">SQL veritabanı'nda Hello tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d6fb-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6fb-118">Merhaba Hdınsight kümesi kullanıyorsanız ve SQL veritabanı oluşturuldu [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md), bu bölümdeki hello adımları atlayın.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="4d6fb-119">Merhaba parçası hello adımları gibi hello veritabanı ve tablo oluşturulan [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md) belge.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="4d6fb-120">Merhaba SSH oturumundan komutu tooconnect toohello SQL veritabanı sunucusu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="4d6fb-121">Metin aşağıdaki çıktı benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="4d6fb-122">Merhaba, `1>` isteminde, sorgu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-122">At hello `1>` prompt, enter hello following query:</span></span>

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

    <span data-ttu-id="4d6fb-123">Ne zaman hello `GO` deyimi girilir, hello önceki deyimleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="4d6fb-124">İlk olarak, hello **mobiledata** tablosu oluşturulur ve kümelenmiş bir dizin (SQL veritabanı tarafından gereklidir.) tooit eklenir</span><span class="sxs-lookup"><span data-stu-id="4d6fb-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="4d6fb-125">Tablo hello sorgu tooverify aşağıdaki kullanım hello oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="4d6fb-126">Metin aşağıdaki çıktı benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="4d6fb-127">Girin `exit` hello adresindeki `1>` sor tooexit hello tsql yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="4d6fb-128">Sqoop dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="4d6fb-128">Sqoop export</span></span>

1. <span data-ttu-id="4d6fb-129">Merhaba SSH bağlantı toohello kümeden Sqoop SQL veritabanınız görebilirsiniz komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="4d6fb-130">İstendiğinde, hello parola hello SQL veritabanı oturum açma için girin.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="4d6fb-131">Bu komut hello dahil olmak üzere veritabanlarının listesini döndürür **sqooptest** daha önce oluşturduğunuz veritabanı.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="4d6fb-132">tooexport verileri **hivesampletable** toohello **mobiledata** tablo, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="4d6fb-133">Bu komut Sqoop tooconnect toohello bildirir **sqooptest** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="4d6fb-134">Sqoop sonra verileri dışa aktarır **wasb: / / / hive/ambarı/hivesampletable** toohello **mobiledata** tablo.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4d6fb-135">Kullanım `wasb:///` hello varsayılan depolama kümeniz için bir Azure depolama hesabı ise.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="4d6fb-136">Kullanım `adl:///` bir Azure Data Lake Store ise.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="4d6fb-137">Merhaba komut tamamlandıktan sonra komut tooconnect toohello veritabanı TSQL kullanarak aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="4d6fb-138">Bağlandıktan sonra dışarı aktarılan toohello veri hello deyimleri tooverify aşağıdaki kullanım hello edildi **mobiledata** tablosu:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="4d6fb-139">Merhaba tablodaki verileri listesini görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="4d6fb-140">Tür `exit` tooexit hello tsql yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="4d6fb-141">Sqoop alma</span><span class="sxs-lookup"><span data-stu-id="4d6fb-141">Sqoop import</span></span>

1. <span data-ttu-id="4d6fb-142">Kullanım hello şu komutu hello tooimport verileri **mobiledata** SQL veritabanındaki toohello tablosu **wasb: / / / öğreticileri/usesqoop/importeddata** hdınsight'ta dizin:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="4d6fb-143">Merhaba veri Hello alanları bir sekme karakteriyle ayrılır ve hello satırları yeni satır karakteri tarafından sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="4d6fb-144">Merhaba içeri aktarma tamamlandıktan sonra komut toolist hello dizininde bulunan verileri hello yeni çıkışı aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="4d6fb-145">SQL Server kullanma</span><span class="sxs-lookup"><span data-stu-id="4d6fb-145">Using SQL Server</span></span>

<span data-ttu-id="4d6fb-146">Ayrıca, Sqoop tooimport kullanmak ve verileri, veri merkezinizdeki veya Azure üzerinde barındırılan bir sanal makinede SQL Server'dan dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="4d6fb-147">SQL Database ve SQL Server kullanarak arasında hello farklılıklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="4d6fb-148">Hdınsight ve SQL Server gerekir olması üzerinde hello aynı Azure sanal ağı.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="4d6fb-149">Merhaba bir örnek için bkz: [bağlanmak Hdınsight tooyour şirket içi ağ](./connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="4d6fb-150">Merhaba Hdınsight bir Azure sanal ağı ile kullanma hakkında daha fazla bilgi için bkz: [genişletmek Hdınsight Azure sanal ağ ile](hdinsight-extend-hadoop-virtual-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="4d6fb-151">Azure sanal ağ ile ilgili daha fazla bilgi için bkz: Merhaba [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md) belge.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="4d6fb-152">SQL Server yapılandırılmış tooallow SQL kimlik doğrulaması olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="4d6fb-153">Daha fazla bilgi için bkz: Merhaba [bir kimlik doğrulama modu seçme](https://msdn.microsoft.com/ms144284.aspx) belge.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="4d6fb-154">Tooconfigure SQL Server tooaccept uzak bağlantıları olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="4d6fb-155">Daha fazla bilgi için bkz: Merhaba [nasıl tootroubleshoot bağlanan toohello SQL Server veritabanı altyapısı](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) belge.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="4d6fb-156">Merhaba oluşturma **sqooptest** gibi bir yardımcı programını kullanarak SQL Server veritabanında **SQL Server Management Studio** veya **tsql**.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="4d6fb-157">hello Azure CLI kullanma hello adımlar, yalnızca Azure SQL veritabanı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="4d6fb-158">Transact-SQL deyimleri toocreate hello aşağıdaki kullanım hello **mobiledata** tablosu:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

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

* <span data-ttu-id="4d6fb-159">SQL Server toohello Hdınsight'ta bağlanırken hello SQL Server toouse başlangıç IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="4d6fb-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="4d6fb-161">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="4d6fb-161">Limitations</span></span>

* <span data-ttu-id="4d6fb-162">Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="4d6fb-163">-Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop yapar hello INSERT işlemlerine toplu işleme yerine birden çok ekler.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d6fb-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d6fb-164">Next steps</span></span>

<span data-ttu-id="4d6fb-165">Öğrendiğiniz artık nasıl toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="4d6fb-166">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="4d6fb-166">toolearn more, see:</span></span>

* <span data-ttu-id="4d6fb-167">[Hdınsight ile Oozie kullanma][hdinsight-use-oozie]: Oozie iş akışında kullanmak Sqoop eylem.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="4d6fb-168">[Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-data]: kullanmak Hive tooanalyze uçuş gecikme veri ve Sqoop tooexport veri tooan Azure SQL veritabanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="4d6fb-169">[Veri tooHDInsight karşıya][hdinsight-upload-data]: veri tooHDInsight/Azure Blob Depolama yüklemek için diğer yöntemler bulun.</span><span class="sxs-lookup"><span data-stu-id="4d6fb-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

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
