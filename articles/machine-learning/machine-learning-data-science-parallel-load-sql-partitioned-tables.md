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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>SQL Bölüm Tabloları Kullanarak Paralel Toplu Veri Alma
Bu belgede nasıl toobuild hızlı paralel toplu veri tooa SQL Server veritabanına alma için tablo bölümlenmiş açıklanmaktadır. Büyük veri yükleme/aktarım tooa SQL veritabanı için veri toohello SQL DB ve sonraki sorguları içeri aktarma kullanılarak geliştirilebilir *bölümlenmiş tabloları ve görünümleri*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Yeni bir veritabanı ve dosya grupları kümesi oluşturma
* [Yeni bir veritabanı oluşturmak](https://technet.microsoft.com/library/ms176061.aspx), zaten yoksa.
* Bölümlenmiş hello fiziksel dosyaları tutacak veritabanı dosya grupları toohello veritabanını ekleyin. Bu, yapılabilir [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) yeni veya [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) hello veritabanı zaten varsa.
* Bir veya daha fazla (gerektiğinde) dosyaları tooeach veritabanı dosya ekleyin.
  
  > [!NOTE]
  > Bu bölüm ve hello fiziksel veritabanı dosya adları için verileri hello dosya verileri depolanacağı tutan hello hedef dosya belirtin.
  > 
  > 

Merhaba aşağıdaki örnek yeni bir veritabanı hello birincil ve günlük grupları, her bir fiziksel dosya içeren dışında üç dosya grupları oluşturur. Merhaba veritabanı dosyaları hello varsayılan SQL Server veri klasörü hello SQL Server örneğinde yapılandırıldığı şekilde oluşturulur. Merhaba varsayılan dosya konumları hakkında daha fazla bilgi için bkz: [varsayılan ve SQL Server örnekleri adlı dosya konumlarını](https://msdn.microsoft.com/library/ms143547.aspx).

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

## <a name="create-a-partitioned-table"></a>Bölümlenmiş bir tablo oluştur
Bölümlenmiş tabloları toohello veri şeması, eşlenen toohello veritabanı dosya grupları hello önceki adımda oluşturduğunuz göre oluşturun. Veri içe toplu olduğunda toohello bölümlenmiş tabloları, aşağıda açıklandığı gibi tooa bölüm düzeni göre hello dosya grupları arasında kayıtları dağıtılacaktır.

**toocreate bölüm tablosu, şunları yapmanız gerekir:**

* [Bölümleme işlevi oluşturma](https://msdn.microsoft.com/library/ms187802.aspx) değerleri/sınırları toobe hello aralığını tanımlayan her tek tek bölüm tablosuna, örn., aya göre toolimit bölümleri dahil (bazı\_datetime\_alan) hello yıl 2013 ile:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Bir bölüm düzeni oluşturma](https://msdn.microsoft.com/library/ms179854.aspx) hangi eşlemeleri her bölüm aralığı grubunda hello bölüm işlevi tooa fiziksel dosya, örneğin:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  tooverify hello aralıklardaki yürürlükte her according toohello işlevi/düzeni bölüm, sorgu aşağıdaki hello çalıştırın:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Bölümlenmiş bir tablo oluşturmak](https://msdn.microsoft.com/library/ms174979.aspx)(s) tooyour veri şemasına göre ve hello bölüm düzeni ve kısıtlama alanı kullanılan toopartition hello tablo, örneğin belirtin:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Daha fazla bilgi için bkz: [bölümlenmiş tablolar oluşturmak ve dizinleri](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Her tek tek bölüm tablosu için toplu içeri aktarma hello verileri
* BCP, toplu ekleme ya da diğer yöntemleri gibi kullanabilir [SQL Server Yükseltme Sihirbazı](http://sqlazuremw.codeplex.com/). sağlanan hello örnek hello BCP yöntemini kullanır.
* [Merhaba veritabanı alter](https://msdn.microsoft.com/library/bb522682.aspx) toochange işlem günlüğü, örneğin düzeni tooBULK_LOGGED toominimize yükünü günlüğü:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* tooexpedite veri yükleme, hello toplu içeri aktarma işlemleri paralel başlatın. SQL Server veritabanlarına büyük veri alma toplu hızlandırılması ipuçları için bkz [1 TB 1 saatten az yük](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Merhaba aşağıdaki PowerShell betiğini paralel veri BCP kullanarak yükleme örneğidir.

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Dizinleri toooptimize birleştirmeler ve sorgu performansı oluşturun
* Birden çok tablodan veri modelleme için ayıklanır varsa, dizinleri tooimprove hello birleştirme performans hello birleştirme anahtarları oluşturun.
* [Dizin oluşturma](https://technet.microsoft.com/library/ms188783.aspx) (kümelenmiş veya kümelenmemiş) hedefleme hello her bölüm için aynı dosya için örn:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  Veya,
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Merhaba dizinleri hello veri alma toplu önce toocreate seçebilirsiniz. Toplu içe aktarmadan önce dizin oluşturma hello veri yükleme yavaşlatır.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Gelişmiş analizler işlemi ve eylem örnekte teknolojisi
Merhaba Cortana Analytics işlem sahip ortak bir veri kümesi kullanarak uçtan uca kılavuz örneği için bkz [Cortana Analytics eylem işleminde: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).

