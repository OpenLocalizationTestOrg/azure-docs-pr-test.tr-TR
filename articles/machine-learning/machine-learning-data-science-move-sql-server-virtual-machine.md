---
title: "bir Azure sanal makinesi üzerinde aaaMove veri tooSQL sunucu | Microsoft Docs"
description: "Verileri Azure VM düz dosyalar ya da şirket içi SQL Server tooSQL sunucusuna taşıyın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="b9c18-103">Bir Azure sanal makinesi üzerinde veri tooSQL sunucu taşıma</span><span class="sxs-lookup"><span data-stu-id="b9c18-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="b9c18-104">Bu konu, bir Azure sanal makineye düz dosyalar (CSV veya TSV biçimleri) veya bir şirket içi SQL Server tooSQL sunucu verilerini taşıma için hello seçenekleri özetler.</span><span class="sxs-lookup"><span data-stu-id="b9c18-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="b9c18-105">Bu görevler için taşıma veri toohello bulut hello takım veri bilimi işlemi bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b9c18-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="b9c18-106">Machine Learning hello seçenekleri taşıma veri tooan Azure SQL veritabanı için özetlenmektedir bir konuya bakın [Azure Machine Learning için verileri tooan Azure SQL veritabanı taşıma](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b9c18-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="b9c18-107">Merhaba **menü** burada hello veri depolanabilir ve sırasında işlenen diğer hedef ortamları tooingest verisine takım veri bilimi işlem (TDSP) nasıl hello açıklamak bağlantılar tootopics aşağıda.</span><span class="sxs-lookup"><span data-stu-id="b9c18-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="b9c18-108">Merhaba aşağıdaki tabloda taşıma veri tooSQL sunucu bir Azure sanal makinesi üzerinde hello seçeneklerini özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="b9c18-109"><b>KAYNAK</b></span><span class="sxs-lookup"><span data-stu-id="b9c18-109"><b>SOURCE</b></span></span> | <span data-ttu-id="b9c18-110"><b>Hedef: SQL Server üzerinde Azure VM</b></span><span class="sxs-lookup"><span data-stu-id="b9c18-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="b9c18-111"><b>Düz dosya</b></span><span class="sxs-lookup"><span data-stu-id="b9c18-111"><b>Flat File</b></span></span> |<span data-ttu-id="b9c18-112">1. <a href="#insert-tables-bcp">Komut satırı toplu kopyalama yardımcı programı (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="b9c18-113">2. <a href="#insert-tables-bulkquery">Toplu ekleme SQL sorgusu</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="b9c18-114">3. <a href="#sql-builtin-utilities">SQL Server'da yerleşik grafik yardımcı programları</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="b9c18-115"><b>Şirket içi SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="b9c18-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="b9c18-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="b9c18-117">2. <a href="#export-flat-file">Tooa verme düz dosya</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="b9c18-118">3. <a href="#sql-migration">SQL veritabanı Geçiş Sihirbazı</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="b9c18-119">4. <a href="#sql-backup">Yukarı geri veritabanı ve geri yükleme</a></span><span class="sxs-lookup"><span data-stu-id="b9c18-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="b9c18-120">Bu belge SQL komutlarını SQL Server Management Studio veya Visual Studio veritabanı Gezgini'nden yürütülür varsaydığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b9c18-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="b9c18-121">Alternatif olarak, kullandığınız [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate ve veri tooa SQL Server VM üzerinde Azure taşınır ardışık zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9c18-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="b9c18-122">Daha fazla bilgi için bkz: [Azure Data Factory (kopyalama etkinliği) ile veri kopyalama](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b9c18-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="b9c18-123"><a name="prereqs"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b9c18-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="b9c18-124">Bu öğretici, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b9c18-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="b9c18-125">Bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="b9c18-125">An **Azure subscription**.</span></span> <span data-ttu-id="b9c18-126">Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9c18-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b9c18-127">Bir **Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="b9c18-127">An **Azure storage account**.</span></span> <span data-ttu-id="b9c18-128">Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9c18-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="b9c18-129">Bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b9c18-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="b9c18-130">Merhaba depolama hesabı oluşturduktan sonra anahtar tooaccess hello depolama kullanılan tooobtain hello hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="b9c18-131">Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="b9c18-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="b9c18-132">Sağlanan **Azure VM'de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b9c18-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="b9c18-133">Yönergeler için bkz: [IPython dizüstü sunucusu gelişmiş analizler için bir Azure SQL Server sanal makinesini yap](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="b9c18-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="b9c18-134">Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="b9c18-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="b9c18-135">Yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9c18-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="b9c18-136"><a name="filesource_to_sqlonazurevm"></a>Azure VM temelinde bir düz dosya kaynak tooSQL sunucu verilerini taşıma</span><span class="sxs-lookup"><span data-stu-id="b9c18-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="b9c18-137">Verilerinizi (bir satır/sütun biçiminde düzenlenmiş) düz bir dosya ise, yöntemler aşağıdaki hello taşınan tooSQL Server VM Azure ile ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="b9c18-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="b9c18-138">Komut satırı toplu kopyalama yardımcı programı (BCP)</span><span class="sxs-lookup"><span data-stu-id="b9c18-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="b9c18-139">Toplu ekleme SQL sorgusu</span><span class="sxs-lookup"><span data-stu-id="b9c18-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="b9c18-140">SQL Server (içeri/dışarı aktarma, SSIS) grafik yerleşik yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="b9c18-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="b9c18-141"><a name="insert-tables-bcp"></a>Komut satırı toplu kopyalama yardımcı programı (BCP)</span><span class="sxs-lookup"><span data-stu-id="b9c18-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="b9c18-142">BCP ile SQL Server yüklü bir komut satırı aracıdır ve hello hızlı şekilde toomove veri biridir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="b9c18-143">Bu, tüm üç SQL Server çeşitleri (şirket içi SQL Server, SQL Azure ve SQL Server VM Azure üzerinde) arasında çalışır.</span><span class="sxs-lookup"><span data-stu-id="b9c18-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="b9c18-144">**Burada verilerim için BCP olması gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="b9c18-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="b9c18-145">Bulunan kaynak verilerini içeren dosyaların bulundurulması, gerekli olmamasına karşın hello hello hedef SQL Server ile aynı makineye daha hızlı sağlar (ağ hızını vs yerel disk g/ç hızı) aktarır.</span><span class="sxs-lookup"><span data-stu-id="b9c18-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="b9c18-146">Merhaba düz dosyalar içeren veri toohello makine taşıyabilirsiniz çeşitli dosya kopyalama kullanarak SQL Server yüklü olduğu gibi araçları [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Gezgini](http://storageexplorer.com/) ya da windows kopyala/yapıştır uzaktan Masaüstü Protokolü (RDP).</span><span class="sxs-lookup"><span data-stu-id="b9c18-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="b9c18-147">Merhaba veritabanını ve hello tabloları hello hedef SQL Server veritabanında oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b9c18-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="b9c18-148">Örneği nasıl toodo bu kullanarak hello `Create Database` ve `Create Table` komutlar:</span><span class="sxs-lookup"><span data-stu-id="b9c18-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="b9c18-149">Bcp yüklendiği hello hello makinenin komut satırı komut aşağıdaki hello vererek hello tablo için şema hello açıklayan hello biçim dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b9c18-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="b9c18-150">Merhaba veriler hello bcp komut aşağıdaki gibi kullanarak hello veritabanına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9c18-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="b9c18-151">Merhaba SQL Server aynı makinede yüklü varsayılarak bu hello komut satırı çalışması gerekir:</span><span class="sxs-lookup"><span data-stu-id="b9c18-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="b9c18-152">**BCP ekler en iyi duruma getirme** aşağıdaki makaleye bakın hello başvurun ['En iyi duruma getirme toplu içeri aktarma yönergeleri'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize gibi ekler.</span><span class="sxs-lookup"><span data-stu-id="b9c18-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="b9c18-153"><a name="insert-tables-bulkquery-parallel"></a>Ekler için daha hızlı veri taşıma parallelizing</span><span class="sxs-lookup"><span data-stu-id="b9c18-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="b9c18-154">Taşıdığınız hello veri büyükse, şeyler paralel bir PowerShell Betiği olarak aynı anda birden çok BCP komutları yürüterek hızlandırma.</span><span class="sxs-lookup"><span data-stu-id="b9c18-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="b9c18-155">**Büyük veri alım** toooptimize veri büyük ve çok büyük veri kümeleri için yükleme birden çok dosya grupları ve bölüm tabloları kullanarak, mantıksal ve fiziksel veritabanı tablolarını bölüm.</span><span class="sxs-lookup"><span data-stu-id="b9c18-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="b9c18-156">Oluşturma ve veri toopartition tabloları yükleme hakkında daha fazla bilgi için bkz: [paralel yük SQL bölüm tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="b9c18-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="b9c18-157">Merhaba örnek PowerShell komut dosyasını aşağıdaki göstermek bcp kullanarak paralel ekler:</span><span class="sxs-lookup"><span data-stu-id="b9c18-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <span data-ttu-id="b9c18-158"><a name="insert-tables-bulkquery"></a>Toplu ekleme SQL sorgusu</span><span class="sxs-lookup"><span data-stu-id="b9c18-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="b9c18-159">[Toplu ekleme SQL sorgusu](https://msdn.microsoft.com/library/ms188365) kullanılan tooimport veriler satır/sütun tabanlı dosyalarından hello veritabanına olabilir (desteklenen hello türleri ele alınmıştır[toplu dışarı veya içeri aktarma (SQL Server) için verileri hazırlama](https://msdn.microsoft.com/library/ms188609)) konu.</span><span class="sxs-lookup"><span data-stu-id="b9c18-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="b9c18-160">Bulk INSERT için bazı örnek komutları şunlardır aşağıdaki şekilde şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b9c18-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="b9c18-161">Verilerinizi çözümlemek ve toomake hello SQL Server veritabanının aynı tarihleri gibi herhangi bir özel alan için format hello varsayar emin almadan önce tüm özel seçenekleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b9c18-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="b9c18-162">Tooset hello tarih biçimini yıl ay-günlük (verileriniz yıl ay gün biçiminde hello tarih içeriyorsa) örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b9c18-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="b9c18-163">Toplu içeri aktarma deyimlerini kullanarak veri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="b9c18-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="b9c18-164"><a name="sql-builtin-utilities"></a>SQL Server'da yerleşik yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="b9c18-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="b9c18-165">SQL Server tümleştirmeler Services (SSIS) tooimport verileri azure'da bir düz dosyadan SQL Server VM halinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9c18-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="b9c18-166">SSIS iki studio ortamlarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="b9c18-167">Ayrıntılar için bkz [Integration Services (SSIS) ve Studio ortamları](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="b9c18-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="b9c18-168">SQL Server veri araçları hakkında daha fazla bilgi için bkz: [Microsoft SQL Server veri araçları](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="b9c18-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="b9c18-169">Merhaba İçeri/Dışarı Aktarma Sihirbazı hakkında daha fazla bilgi için bkz: [SQL Server içeri ve Dışarı Aktarma Sihirbazı](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="b9c18-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="b9c18-170"><a name="sqlonprem_to_sqlonazurevm"></a>Şirket içi SQL Server tooSQL bir Azure VM sunucuda taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="b9c18-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="b9c18-171">Geçiş stratejilerini aşağıdaki hello de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b9c18-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="b9c18-172">Bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma</span><span class="sxs-lookup"><span data-stu-id="b9c18-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="b9c18-173">TooFlat dosyası dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="b9c18-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="b9c18-174">SQL veritabanı Geçiş Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="b9c18-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="b9c18-175">Yukarı geri veritabanı ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b9c18-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="b9c18-176">Biz bunların her biri aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="b9c18-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="b9c18-177">Bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma</span><span class="sxs-lookup"><span data-stu-id="b9c18-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="b9c18-178">Merhaba **bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma** bir basit ve önerilen yol toomove bir şirket içi SQL Server örneği tooSQL bir Azure VM sunucuda verilerdir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="b9c18-179">Ayrıntılı adımlar yanı sıra tartışma diğer alternatifleri için bkz: [veritabanı tooSQL bir Azure VM sunucuda geçiş](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b9c18-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="b9c18-180"><a name="export-flat-file"></a>TooFlat dosyası dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="b9c18-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="b9c18-181">Hello belirtildiği gibi çeşitli yöntemler kullanılan toobulk bir şirket içi SQL Server verileri dışa olabilir [toplu içeri ve dışarı aktarma veri (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="b9c18-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="b9c18-182">Bu belge hello toplu kopyalama programı (BCP) örnek olarak ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="b9c18-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="b9c18-183">Veri düz bir dosyaya dışarı aktarıldıktan sonra içeri aktarılan tooanother SQL server toplu içeri kullanarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="b9c18-184">Şirket içi SQL Server tooa dosya Hello verilerini dışa aktarma hello bcp yardımcı programını şu şekilde kullanma</span><span class="sxs-lookup"><span data-stu-id="b9c18-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="b9c18-185">SQL Server VM hello kullanarak azure'da Hello veritabanı ve hello tablo oluşturmak `create database` ve `create table` 1. adımda dışarı hello tablo şeması için.</span><span class="sxs-lookup"><span data-stu-id="b9c18-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="b9c18-186">Merhaba verilerin dışa ve içe olmasıyla hello tablo şemasını tanımlayan bir biçim dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9c18-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="b9c18-187">Merhaba biçim dosyası ayrıntılarını açıklanmıştır [(SQL Server) bir biçim dosyası oluşturma](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9c18-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="b9c18-188">Ne zaman gelen BCP çalıştıran izin ver hello SQL Server makinesinde biçim dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9c18-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="b9c18-189">Biçim dosyası oluşturma çalışırken BCP uzaktan karşı bir SQL Server</span><span class="sxs-lookup"><span data-stu-id="b9c18-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="b9c18-190">Bölümünde açıklanan hello yöntemlerden birini kullanın [dosya kaynağı verilerini taşıma](#filesource_to_sqlonazurevm) düz dosyalar tooa SQL Server toomove hello verileri.</span><span class="sxs-lookup"><span data-stu-id="b9c18-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="b9c18-191"><a name="sql-migration"></a>SQL veritabanı Geçiş Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="b9c18-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="b9c18-192">[SQL Server veritabanı Geçiş Sihirbazı](http://sqlazuremw.codeplex.com/) iki SQL server örnekleri arasında veri kullanımı kolay şekilde toomove sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9c18-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="b9c18-193">Kaynak ve hedef tablolar arasında hello kullanıcı toomap hello veri şeması sağlar, sütun türleri ve diğer çeşitli işlevlerin seçin.</span><span class="sxs-lookup"><span data-stu-id="b9c18-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="b9c18-194">Merhaba perde arkasında toplu kopyalama (BCP) kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9c18-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="b9c18-195">Bir ekran görüntüsünü hello hello SQL veritabanı Geçiş Sihirbazı'nı aşağıda gösterildiği ekran Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="b9c18-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![SQL Server Yükseltme Sihirbazı][2]

### <span data-ttu-id="b9c18-197"><a name="sql-backup"></a>Yukarı geri veritabanı ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b9c18-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="b9c18-198">SQL Server destekler:</span><span class="sxs-lookup"><span data-stu-id="b9c18-198">SQL Server supports:</span></span>

1. <span data-ttu-id="b9c18-199">[Veritabanı geri yukarı ve işlevlerin geri yüklenmesi](https://msdn.microsoft.com/library/ms187048.aspx) (her iki tooa yerel dosya ya da bacpac verme tooblob) ve [veri katmanı uygulamaları](https://msdn.microsoft.com/library/ee210546.aspx) (bacpac kullanarak).</span><span class="sxs-lookup"><span data-stu-id="b9c18-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="b9c18-200">Özelliği toodirectly SQL Server sanal makineleri Azure üzerinde bir kopyalanan veritabanı create veya kopyalama tooan var olan SQL Azure ile.</span><span class="sxs-lookup"><span data-stu-id="b9c18-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="b9c18-201">Daha fazla ayrıntı için bkz: [kullanım hello kopyalama Veritabanı Sihirbazı](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9c18-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="b9c18-202">Bir ekran görüntüsünü hello veritabanı geri yukarı/geri yükleme seçenekleri SQL Server Management Studio'dan aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b9c18-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server içeri aktarma aracı][1]

## <a name="resources"></a><span data-ttu-id="b9c18-204">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b9c18-204">Resources</span></span>
[<span data-ttu-id="b9c18-205">Veritabanı tooSQL bir Azure VM sunucuda geçirme</span><span class="sxs-lookup"><span data-stu-id="b9c18-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="b9c18-206">Azure Sanal Makineler’de SQL Server’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="b9c18-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
