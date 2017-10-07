---
title: "aaaBuild ve Azure VM'de SQL Server içine tablolar verilerin hızlı paralel alma için en iyi duruma getirme | Microsoft Docs"
description: "SQL Bölüm Tabloları Kullanarak Paralel Toplu Veri Alma"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="6eec5-103">SQL Bölüm Tabloları Kullanarak Paralel Toplu Veri Alma</span><span class="sxs-lookup"><span data-stu-id="6eec5-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="6eec5-104">Bu belgede nasıl toobuild hızlı paralel toplu veri tooa SQL Server veritabanına alma için tablo bölümlenmiş açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6eec5-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="6eec5-105">Büyük veri yükleme/aktarım tooa SQL veritabanı için veri toohello SQL DB ve sonraki sorguları içeri aktarma kullanılarak geliştirilebilir *bölümlenmiş tabloları ve görünümleri*.</span><span class="sxs-lookup"><span data-stu-id="6eec5-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="6eec5-106">Yeni bir veritabanı ve dosya grupları kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6eec5-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="6eec5-107">[Yeni bir veritabanı oluşturmak](https://technet.microsoft.com/library/ms176061.aspx), zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="6eec5-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="6eec5-108">Bölümlenmiş hello fiziksel dosyaları tutacak veritabanı dosya grupları toohello veritabanını ekleyin. Bu, yapılabilir [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) yeni veya [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) hello veritabanı zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="6eec5-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="6eec5-109">Bir veya daha fazla (gerektiğinde) dosyaları tooeach veritabanı dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6eec5-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6eec5-110">Bu bölüm ve hello fiziksel veritabanı dosya adları için verileri hello dosya verileri depolanacağı tutan hello hedef dosya belirtin.</span><span class="sxs-lookup"><span data-stu-id="6eec5-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="6eec5-111">Merhaba aşağıdaki örnek yeni bir veritabanı hello birincil ve günlük grupları, her bir fiziksel dosya içeren dışında üç dosya grupları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6eec5-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="6eec5-112">Merhaba veritabanı dosyaları hello varsayılan SQL Server veri klasörü hello SQL Server örneğinde yapılandırıldığı şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6eec5-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="6eec5-113">Merhaba varsayılan dosya konumları hakkında daha fazla bilgi için bkz: [varsayılan ve SQL Server örnekleri adlı dosya konumlarını](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eec5-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="6eec5-114">Bölümlenmiş bir tablo oluştur</span><span class="sxs-lookup"><span data-stu-id="6eec5-114">Create a partitioned table</span></span>
<span data-ttu-id="6eec5-115">Bölümlenmiş tabloları toohello veri şeması, eşlenen toohello veritabanı dosya grupları hello önceki adımda oluşturduğunuz göre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6eec5-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="6eec5-116">Veri içe toplu olduğunda toohello bölümlenmiş tabloları, aşağıda açıklandığı gibi tooa bölüm düzeni göre hello dosya grupları arasında kayıtları dağıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="6eec5-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="6eec5-117">**toocreate bölüm tablosu, şunları yapmanız gerekir:**</span><span class="sxs-lookup"><span data-stu-id="6eec5-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="6eec5-118">[Bölümleme işlevi oluşturma](https://msdn.microsoft.com/library/ms187802.aspx) değerleri/sınırları toobe hello aralığını tanımlayan her tek tek bölüm tablosuna, örn., aya göre toolimit bölümleri dahil (bazı\_datetime\_alan) hello yıl 2013 ile:</span><span class="sxs-lookup"><span data-stu-id="6eec5-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="6eec5-119">[Bir bölüm düzeni oluşturma](https://msdn.microsoft.com/library/ms179854.aspx) hangi eşlemeleri her bölüm aralığı grubunda hello bölüm işlevi tooa fiziksel dosya, örneğin:</span><span class="sxs-lookup"><span data-stu-id="6eec5-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="6eec5-120">tooverify hello aralıklardaki yürürlükte her according toohello işlevi/düzeni bölüm, sorgu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6eec5-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="6eec5-121">[Bölümlenmiş bir tablo oluşturmak](https://msdn.microsoft.com/library/ms174979.aspx)(s) tooyour veri şemasına göre ve hello bölüm düzeni ve kısıtlama alanı kullanılan toopartition hello tablo, örneğin belirtin:</span><span class="sxs-lookup"><span data-stu-id="6eec5-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="6eec5-122">Daha fazla bilgi için bkz: [bölümlenmiş tablolar oluşturmak ve dizinleri](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eec5-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="6eec5-123">Her tek tek bölüm tablosu için toplu içeri aktarma hello verileri</span><span class="sxs-lookup"><span data-stu-id="6eec5-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="6eec5-124">BCP, toplu ekleme ya da diğer yöntemleri gibi kullanabilir [SQL Server Yükseltme Sihirbazı](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="6eec5-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="6eec5-125">sağlanan hello örnek hello BCP yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6eec5-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="6eec5-126">[Merhaba veritabanı alter](https://msdn.microsoft.com/library/bb522682.aspx) toochange işlem günlüğü, örneğin düzeni tooBULK_LOGGED toominimize yükünü günlüğü:</span><span class="sxs-lookup"><span data-stu-id="6eec5-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="6eec5-127">tooexpedite veri yükleme, hello toplu içeri aktarma işlemleri paralel başlatın.</span><span class="sxs-lookup"><span data-stu-id="6eec5-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="6eec5-128">SQL Server veritabanlarına büyük veri alma toplu hızlandırılması ipuçları için bkz [1 TB 1 saatten az yük](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eec5-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="6eec5-129">Merhaba aşağıdaki PowerShell betiğini paralel veri BCP kullanarak yükleme örneğidir.</span><span class="sxs-lookup"><span data-stu-id="6eec5-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="6eec5-130">Dizinleri toooptimize birleştirmeler ve sorgu performansı oluşturun</span><span class="sxs-lookup"><span data-stu-id="6eec5-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="6eec5-131">Birden çok tablodan veri modelleme için ayıklanır varsa, dizinleri tooimprove hello birleştirme performans hello birleştirme anahtarları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6eec5-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="6eec5-132">[Dizin oluşturma](https://technet.microsoft.com/library/ms188783.aspx) (kümelenmiş veya kümelenmemiş) hedefleme hello her bölüm için aynı dosya için örn:</span><span class="sxs-lookup"><span data-stu-id="6eec5-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="6eec5-133">Veya,</span><span class="sxs-lookup"><span data-stu-id="6eec5-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="6eec5-134">Merhaba dizinleri hello veri alma toplu önce toocreate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eec5-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="6eec5-135">Toplu içe aktarmadan önce dizin oluşturma hello veri yükleme yavaşlatır.</span><span class="sxs-lookup"><span data-stu-id="6eec5-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="6eec5-136">Gelişmiş analizler işlemi ve eylem örnekte teknolojisi</span><span class="sxs-lookup"><span data-stu-id="6eec5-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="6eec5-137">Merhaba Cortana Analytics işlem sahip ortak bir veri kümesi kullanarak uçtan uca kılavuz örneği için bkz [Cortana Analytics eylem işleminde: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="6eec5-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

