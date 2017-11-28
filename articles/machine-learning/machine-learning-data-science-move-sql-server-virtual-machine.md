---
title: "Bir Azure sanal makinede SQL Server'a veri taşıma | Microsoft Docs"
description: "Verileri düz dosyalardan veya bir şirket içi SQL Server'dan Azure VM'de SQL Server'a taşıyın."
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="d82fe-103">Bir Azure sanal makinesinde SQL Server’a veri taşıma</span><span class="sxs-lookup"><span data-stu-id="d82fe-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="d82fe-104">Bu konu, verileri düz dosyalar (CSV veya TSV biçimleri) veya bir şirket içi SQL Server'dan SQL Server'a bir Azure sanal makinesi üzerinde taşıma seçeneklerini özetler.</span><span class="sxs-lookup"><span data-stu-id="d82fe-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="d82fe-105">Verileri buluta taşımak için bu görevleri takım veri bilimi işleminin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="d82fe-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="d82fe-106">Machine Learning için bir Azure SQL veritabanına veri taşıma seçeneklerini özetlenmektedir bir konuya bakın [veri taşıma bir Azure SQL veritabanına Azure Machine Learning için](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d82fe-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="d82fe-107">**Menü** burada veri depolanabilir ve takım veri bilimi işlem (TDSP) sırasında işlenen diğer hedef ortamlara veri alma nasıl açıklayan konulara bağlantılar aşağıda.</span><span class="sxs-lookup"><span data-stu-id="d82fe-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="d82fe-108">Bir Azure sanal makinede SQL Server verilerini taşıma seçenekleri aşağıdaki tabloda özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d82fe-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="d82fe-109"><b>KAYNAK</b></span><span class="sxs-lookup"><span data-stu-id="d82fe-109"><b>SOURCE</b></span></span> | <span data-ttu-id="d82fe-110"><b>Hedef: SQL Server üzerinde Azure VM</b></span><span class="sxs-lookup"><span data-stu-id="d82fe-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="d82fe-111"><b>Düz dosya</b></span><span class="sxs-lookup"><span data-stu-id="d82fe-111"><b>Flat File</b></span></span> |<span data-ttu-id="d82fe-112">1. <a href="#insert-tables-bcp">Komut satırı toplu kopyalama yardımcı programı (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="d82fe-113">2. <a href="#insert-tables-bulkquery">Toplu ekleme SQL sorgusu</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="d82fe-114">3. <a href="#sql-builtin-utilities">SQL Server'da yerleşik grafik yardımcı programları</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="d82fe-115"><b>Şirket içi SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="d82fe-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="d82fe-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Microsoft Azure VM Sihirbazı için bir SQL Server veritabanı dağıtma</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="d82fe-117">2. <a href="#export-flat-file">Düz bir dosyaya aktarın</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="d82fe-118">3. <a href="#sql-migration">SQL veritabanı Geçiş Sihirbazı</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="d82fe-119">4. <a href="#sql-backup">Yukarı geri veritabanı ve geri yükleme</a></span><span class="sxs-lookup"><span data-stu-id="d82fe-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="d82fe-120">Bu belge SQL komutlarını SQL Server Management Studio veya Visual Studio veritabanı Gezgini'nden yürütülür varsaydığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d82fe-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="d82fe-121">Alternatif olarak, kullandığınız [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) oluşturmak ve verileri Azure üzerinde bir SQL Server VM taşınır ardışık zamanlamak için.</span><span class="sxs-lookup"><span data-stu-id="d82fe-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="d82fe-122">Daha fazla bilgi için bkz: [Azure Data Factory (kopyalama etkinliği) ile veri kopyalama](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d82fe-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="d82fe-123"><a name="prereqs"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d82fe-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="d82fe-124">Bu öğretici, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d82fe-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="d82fe-125">Bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="d82fe-125">An **Azure subscription**.</span></span> <span data-ttu-id="d82fe-126">Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82fe-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d82fe-127">Bir **Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="d82fe-127">An **Azure storage account**.</span></span> <span data-ttu-id="d82fe-128">Bu öğreticide verileri depolamak için bir Azure depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d82fe-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="d82fe-129">Azure depolama hesabınız yoksa [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="d82fe-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="d82fe-130">Depolama hesabı oluşturduktan sonra depolama erişmek için kullanılan hesap anahtarı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d82fe-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="d82fe-131">Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="d82fe-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="d82fe-132">Sağlanan **Azure VM'de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d82fe-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="d82fe-133">Yönergeler için bkz: [IPython dizüstü sunucusu gelişmiş analizler için bir Azure SQL Server sanal makinesini yap](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="d82fe-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="d82fe-134">Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="d82fe-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="d82fe-135">Yönergeler için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d82fe-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="d82fe-136"><a name="filesource_to_sqlonazurevm"></a>Azure VM'de SQL Server için bir düz dosya kaynaktan veri taşımayı</span><span class="sxs-lookup"><span data-stu-id="d82fe-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="d82fe-137">Verilerinizi (bir satır/sütun biçiminde düzenlenmiş) düz bir dosya ise, bu SQL Server VM Azure üzerinde aşağıdaki yöntemleri taşınabilir:</span><span class="sxs-lookup"><span data-stu-id="d82fe-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="d82fe-138">Komut satırı toplu kopyalama yardımcı programı (BCP)</span><span class="sxs-lookup"><span data-stu-id="d82fe-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="d82fe-139">Toplu ekleme SQL sorgusu</span><span class="sxs-lookup"><span data-stu-id="d82fe-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="d82fe-140">SQL Server (içeri/dışarı aktarma, SSIS) grafik yerleşik yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="d82fe-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="d82fe-141"><a name="insert-tables-bcp"></a>Komut satırı toplu kopyalama yardımcı programı (BCP)</span><span class="sxs-lookup"><span data-stu-id="d82fe-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="d82fe-142">BCP komut satırı yardımcı programı ile SQL Server yüklü olduğundan ve verileri taşımak için hızlı yollarından biri.</span><span class="sxs-lookup"><span data-stu-id="d82fe-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="d82fe-143">Bu, tüm üç SQL Server çeşitleri (şirket içi SQL Server, SQL Azure ve SQL Server VM Azure üzerinde) arasında çalışır.</span><span class="sxs-lookup"><span data-stu-id="d82fe-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="d82fe-144">**Burada verilerim için BCP olması gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="d82fe-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="d82fe-145">Gerekli olmamasına karşın, hedef SQL Server ile aynı makinede bulunan kaynak verilerini içeren dosyaları daha hızlı aktarımları (ağ hızını vs yerel disk g/ç hızı) sağlar.</span><span class="sxs-lookup"><span data-stu-id="d82fe-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="d82fe-146">Makineye verileri içeren düz dosyalar taşıyabilirsiniz çeşitli dosya kopyalama kullanarak SQL Server yüklü olduğu gibi araçları [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Gezgini](http://storageexplorer.com/) veya windows Uzak Masaüstü kopyalayıp yapıştırın Protokolü (RDP).</span><span class="sxs-lookup"><span data-stu-id="d82fe-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="d82fe-147">Veritabanı ve tablo hedef SQL Server veritabanında oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d82fe-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="d82fe-148">Bu kullanılarak nasıl bir örneği burada verilmiştir `Create Database` ve `Create Table` komutlar:</span><span class="sxs-lookup"><span data-stu-id="d82fe-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="d82fe-149">Bcp yüklü olduğu makinenin komut satırından aşağıdaki komutu gönderdikten tarafından tablo için şema açıklayan biçim dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d82fe-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="d82fe-150">Bcp komut aşağıdaki gibi kullanarak veritabanına veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d82fe-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="d82fe-151">SQL Server aynı makinede yüklü varsayılarak bu komut satırı ile çalışması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d82fe-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="d82fe-152">**BCP ekler en iyi duruma getirme** Lütfen aşağıdaki makaleye bakın ['En iyi duruma getirme toplu içeri aktarma yönergeleri'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) böyle ekler en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="d82fe-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="d82fe-153"><a name="insert-tables-bulkquery-parallel"></a>Ekler için daha hızlı veri taşıma parallelizing</span><span class="sxs-lookup"><span data-stu-id="d82fe-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="d82fe-154">Taşıdığınız veri büyükse, şeyler paralel bir PowerShell Betiği olarak aynı anda birden çok BCP komutları yürüterek hızlandırma.</span><span class="sxs-lookup"><span data-stu-id="d82fe-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="d82fe-155">**Büyük veri alım** veri yükleme büyük ve çok büyük veri kümeleri için en iyi duruma getirmek için birden çok dosya grupları ve bölüm tabloları kullanarak, mantıksal ve fiziksel veritabanı tablolarını bölüm.</span><span class="sxs-lookup"><span data-stu-id="d82fe-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="d82fe-156">Oluşturma ve bölüm tablolara veri yükleme hakkında daha fazla bilgi için bkz: [paralel yük SQL bölüm tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d82fe-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="d82fe-157">Aşağıdaki örnek PowerShell komut dosyası bcp kullanarak paralel eklemeleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d82fe-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="d82fe-158"><a name="insert-tables-bulkquery"></a>Toplu ekleme SQL sorgusu</span><span class="sxs-lookup"><span data-stu-id="d82fe-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="d82fe-159">[Toplu ekleme SQL sorgusu](https://msdn.microsoft.com/library/ms188365) satır/sütun göre dosyaları veritabanından veri almak için kullanılan (desteklenen türlerden ele alınmaktadır[toplu dışarı veya içeri aktarma (SQL Server) için verileri hazırlama](https://msdn.microsoft.com/library/ms188609)) konu.</span><span class="sxs-lookup"><span data-stu-id="d82fe-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="d82fe-160">Bulk INSERT için bazı örnek komutları şunlardır aşağıdaki şekilde şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d82fe-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="d82fe-161">Verilerinizi çözümlemek ve SQL Server veritabanı tarihleri gibi herhangi bir özel alan için aynı biçimde varsayar emin olmak için almadan önce tüm özel seçenekleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d82fe-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="d82fe-162">(Verileriniz yıl ay gün biçimine tarih içeriyorsa) tarih biçimi yıl ay-günlük ayarlamak nasıl bir örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d82fe-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="d82fe-163">Toplu içeri aktarma deyimlerini kullanarak veri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="d82fe-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="d82fe-164"><a name="sql-builtin-utilities"></a>SQL Server'da yerleşik yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="d82fe-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="d82fe-165">SQL Server VM azure'da bir düz dosyadan veri almak için SQL Server tümleştirmeler Services (SSIS) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82fe-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="d82fe-166">SSIS iki studio ortamlarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d82fe-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="d82fe-167">Ayrıntılar için bkz [Integration Services (SSIS) ve Studio ortamları](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="d82fe-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="d82fe-168">SQL Server veri araçları hakkında daha fazla bilgi için bkz: [Microsoft SQL Server veri araçları](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="d82fe-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="d82fe-169">İçeri/Dışarı Aktarma Sihirbazı hakkında daha fazla bilgi için bkz: [SQL Server içeri ve Dışarı Aktarma Sihirbazı](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="d82fe-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="d82fe-170"><a name="sqlonprem_to_sqlonazurevm"></a>Şirket içi SQL Server'dan veri taşımayı Azure VM'de SQL Server</span><span class="sxs-lookup"><span data-stu-id="d82fe-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="d82fe-171">Aşağıdaki geçiş stratejilerini de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d82fe-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="d82fe-172">Microsoft Azure VM Sihirbazı için bir SQL Server veritabanı dağıtma</span><span class="sxs-lookup"><span data-stu-id="d82fe-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="d82fe-173">Düz dosya dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d82fe-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="d82fe-174">SQL veritabanı Geçiş Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="d82fe-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="d82fe-175">Yukarı geri veritabanı ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d82fe-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="d82fe-176">Biz bunların her biri aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d82fe-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="d82fe-177">Microsoft Azure VM Sihirbazı için bir SQL Server veritabanı dağıtma</span><span class="sxs-lookup"><span data-stu-id="d82fe-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="d82fe-178">**Microsoft Azure VM Sihirbazı için bir SQL Server veritabanı dağıtmak** verileri bir şirket içi SQL Server örneğini SQL Server için bir Azure VM taşımak için bir basit ve önerilen yoldur.</span><span class="sxs-lookup"><span data-stu-id="d82fe-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="d82fe-179">Ayrıntılı adımlar yanı sıra tartışma diğer alternatifleri için bkz: [Azure VM'de SQL Server veritabanı geçirilecek](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d82fe-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="d82fe-180"><a name="export-flat-file"></a>Düz dosya dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d82fe-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="d82fe-181">Bir şirket içi SQL Server verileri dışa açıklandığı gibi toplu için çeşitli yöntemler kullanılabilir [toplu içeri ve dışarı aktarma veri (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="d82fe-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="d82fe-182">Bu belge toplu kopyalama programı (BCP) örnek olarak ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="d82fe-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="d82fe-183">Veri düz bir dosyaya dışarı aktarıldıktan sonra başka bir SQL server kullanarak toplu içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="d82fe-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="d82fe-184">Verileri şirket içi SQL Server'dan bcp yardımcı programını kullanarak bir dosyaya aktarın.</span><span class="sxs-lookup"><span data-stu-id="d82fe-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="d82fe-185">Azure kullanarak SQL Server VM üzerinde veritabanı ve tablo oluşturma `create database` ve `create table` tablo şemasını dışarı adım 1.</span><span class="sxs-lookup"><span data-stu-id="d82fe-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="d82fe-186">Verilerin dışa ve içe olmasıyla tablo şemasını tanımlayan bir biçim dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d82fe-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="d82fe-187">Biçim dosyası ayrıntılarını açıklanmıştır [(SQL Server) bir biçim dosyası oluşturma](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="d82fe-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="d82fe-188">Biçim dosyası oluşturma SQL Server makine BCP çalışırken</span><span class="sxs-lookup"><span data-stu-id="d82fe-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="d82fe-189">Biçim dosyası oluşturma çalışırken BCP uzaktan karşı bir SQL Server</span><span class="sxs-lookup"><span data-stu-id="d82fe-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="d82fe-190">Bölümünde açıklanan yöntemlerden birini kullanın [dosya kaynağı verilerini taşıma](#filesource_to_sqlonazurevm) verileri bir SQL Server'a düz dosyalarda taşımak için.</span><span class="sxs-lookup"><span data-stu-id="d82fe-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="d82fe-191"><a name="sql-migration"></a>SQL veritabanı Geçiş Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="d82fe-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="d82fe-192">[SQL Server veritabanı Geçiş Sihirbazı](http://sqlazuremw.codeplex.com/) iki SQL server örnekleri arasında verileri taşımak için kullanımı kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="d82fe-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="d82fe-193">Kaynak ve hedef tablolar arasında veri şeması eşlemek için sütun türleri ve diğer çeşitli işlevlerin seçin kullanıcının sağlar.</span><span class="sxs-lookup"><span data-stu-id="d82fe-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="d82fe-194">Kapak altında toplu kopyalama (BCP) kullanır.</span><span class="sxs-lookup"><span data-stu-id="d82fe-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="d82fe-195">SQL veritabanı Geçiş Sihirbazı Hoş Geldiniz ekranının ekran görüntüsü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d82fe-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![SQL Server Yükseltme Sihirbazı][2]

### <span data-ttu-id="d82fe-197"><a name="sql-backup"></a>Yukarı geri veritabanı ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d82fe-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="d82fe-198">SQL Server destekler:</span><span class="sxs-lookup"><span data-stu-id="d82fe-198">SQL Server supports:</span></span>

1. <span data-ttu-id="d82fe-199">[Veritabanı geri yukarı ve işlevlerin geri yüklenmesi](https://msdn.microsoft.com/library/ms187048.aspx) (bir yerel dosya veya bacpac her ikisini birden verme blob'a) ve [veri katmanı uygulamaları](https://msdn.microsoft.com/library/ee210546.aspx) (bacpac kullanarak).</span><span class="sxs-lookup"><span data-stu-id="d82fe-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="d82fe-200">Doğrudan kopyalanan veritabanı veya var olan bir SQL Azure veritabanı kopyasına sahip Azure üzerinde SQL Server Vm'lerinin oluşturma yeteneği.</span><span class="sxs-lookup"><span data-stu-id="d82fe-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="d82fe-201">Daha fazla ayrıntı için bkz: [kopya Veritabanı Sihirbazı'nı](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="d82fe-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="d82fe-202">Bir ekran görüntüsünü veritabanı geri yukarı/geri yükleme seçenekleri SQL Server Management Studio'dan aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d82fe-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server içeri aktarma aracı][1]

## <a name="resources"></a><span data-ttu-id="d82fe-204">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d82fe-204">Resources</span></span>
[<span data-ttu-id="d82fe-205">Azure VM'de SQL Server veritabanı geçir</span><span class="sxs-lookup"><span data-stu-id="d82fe-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="d82fe-206">Azure Sanal Makineler’de SQL Server’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="d82fe-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
