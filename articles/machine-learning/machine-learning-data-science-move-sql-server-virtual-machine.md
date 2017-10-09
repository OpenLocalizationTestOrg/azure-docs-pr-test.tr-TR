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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Bir Azure sanal makinesi üzerinde veri tooSQL sunucu taşıma
Bu konu, bir Azure sanal makineye düz dosyalar (CSV veya TSV biçimleri) veya bir şirket içi SQL Server tooSQL sunucu verilerini taşıma için hello seçenekleri özetler. Bu görevler için taşıma veri toohello bulut hello takım veri bilimi işlemi bir parçasıdır.

Machine Learning hello seçenekleri taşıma veri tooan Azure SQL veritabanı için özetlenmektedir bir konuya bakın [Azure Machine Learning için verileri tooan Azure SQL veritabanı taşıma](machine-learning-data-science-move-sql-azure.md).

Merhaba **menü** burada hello veri depolanabilir ve sırasında işlenen diğer hedef ortamları tooingest verisine takım veri bilimi işlem (TDSP) nasıl hello açıklamak bağlantılar tootopics aşağıda.

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Merhaba aşağıdaki tabloda taşıma veri tooSQL sunucu bir Azure sanal makinesi üzerinde hello seçeneklerini özetlenmektedir.

| <b>KAYNAK</b> | <b>Hedef: SQL Server üzerinde Azure VM</b> |
| --- | --- |
| <b>Düz dosya</b> |1. <a href="#insert-tables-bcp">Komut satırı toplu kopyalama yardımcı programı (BCP)</a><br> 2. <a href="#insert-tables-bulkquery">Toplu ekleme SQL sorgusu</a><br> 3. <a href="#sql-builtin-utilities">SQL Server'da yerleşik grafik yardımcı programları</a> |
| <b>Şirket içi SQL Server</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma</a><br> 2. <a href="#export-flat-file">Tooa verme düz dosya</a><br> 3. <a href="#sql-migration">SQL veritabanı Geçiş Sihirbazı</a> <br> 4. <a href="#sql-backup">Yukarı geri veritabanı ve geri yükleme</a><br> |

Bu belge SQL komutlarını SQL Server Management Studio veya Visual Studio veritabanı Gezgini'nden yürütülür varsaydığını unutmayın.

> [!TIP]
> Alternatif olarak, kullandığınız [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate ve veri tooa SQL Server VM üzerinde Azure taşınır ardışık zamanlayabilirsiniz. Daha fazla bilgi için bkz: [Azure Data Factory (kopyalama etkinliği) ile veri kopyalama](../data-factory/data-factory-data-movement-activities.md).
>
>

## <a name="prereqs"></a>Önkoşullar
Bu öğretici, sahip olduğunuz varsayılmaktadır:

* Bir **Azure aboneliği**. Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Bir **Azure depolama hesabı**. Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanır. Bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesi. Merhaba depolama hesabı oluşturduktan sonra anahtar tooaccess hello depolama kullanılan tooobtain hello hesabı gerekir. Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Sağlanan **Azure VM'de SQL Server**. Yönergeler için bkz: [IPython dizüstü sunucusu gelişmiş analizler için bir Azure SQL Server sanal makinesini yap](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak. Yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Azure VM temelinde bir düz dosya kaynak tooSQL sunucu verilerini taşıma
Verilerinizi (bir satır/sütun biçiminde düzenlenmiş) düz bir dosya ise, yöntemler aşağıdaki hello taşınan tooSQL Server VM Azure ile ilgili olabilir:

1. [Komut satırı toplu kopyalama yardımcı programı (BCP)](#insert-tables-bcp)
2. [Toplu ekleme SQL sorgusu](#insert-tables-bulkquery)
3. [SQL Server (içeri/dışarı aktarma, SSIS) grafik yerleşik yardımcı programları](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Komut satırı toplu kopyalama yardımcı programı (BCP)
BCP ile SQL Server yüklü bir komut satırı aracıdır ve hello hızlı şekilde toomove veri biridir. Bu, tüm üç SQL Server çeşitleri (şirket içi SQL Server, SQL Azure ve SQL Server VM Azure üzerinde) arasında çalışır.

> [!NOTE]
> **Burada verilerim için BCP olması gerekiyor mu?**  
> Bulunan kaynak verilerini içeren dosyaların bulundurulması, gerekli olmamasına karşın hello hello hedef SQL Server ile aynı makineye daha hızlı sağlar (ağ hızını vs yerel disk g/ç hızı) aktarır. Merhaba düz dosyalar içeren veri toohello makine taşıyabilirsiniz çeşitli dosya kopyalama kullanarak SQL Server yüklü olduğu gibi araçları [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Gezgini](http://storageexplorer.com/) ya da windows kopyala/yapıştır uzaktan Masaüstü Protokolü (RDP).
>
>

1. Merhaba veritabanını ve hello tabloları hello hedef SQL Server veritabanında oluşturduğunuzdan emin olun. Örneği nasıl toodo bu kullanarak hello `Create Database` ve `Create Table` komutlar:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Bcp yüklendiği hello hello makinenin komut satırı komut aşağıdaki hello vererek hello tablo için şema hello açıklayan hello biçim dosyası oluşturur.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Merhaba veriler hello bcp komut aşağıdaki gibi kullanarak hello veritabanına ekleyin. Merhaba SQL Server aynı makinede yüklü varsayılarak bu hello komut satırı çalışması gerekir:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **BCP ekler en iyi duruma getirme** aşağıdaki makaleye bakın hello başvurun ['En iyi duruma getirme toplu içeri aktarma yönergeleri'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize gibi ekler.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Ekler için daha hızlı veri taşıma parallelizing
Taşıdığınız hello veri büyükse, şeyler paralel bir PowerShell Betiği olarak aynı anda birden çok BCP komutları yürüterek hızlandırma.

> [!NOTE]
> **Büyük veri alım** toooptimize veri büyük ve çok büyük veri kümeleri için yükleme birden çok dosya grupları ve bölüm tabloları kullanarak, mantıksal ve fiziksel veritabanı tablolarını bölüm. Oluşturma ve veri toopartition tabloları yükleme hakkında daha fazla bilgi için bkz: [paralel yük SQL bölüm tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Merhaba örnek PowerShell komut dosyasını aşağıdaki göstermek bcp kullanarak paralel ekler:

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


### <a name="insert-tables-bulkquery"></a>Toplu ekleme SQL sorgusu
[Toplu ekleme SQL sorgusu](https://msdn.microsoft.com/library/ms188365) kullanılan tooimport veriler satır/sütun tabanlı dosyalarından hello veritabanına olabilir (desteklenen hello türleri ele alınmıştır[toplu dışarı veya içeri aktarma (SQL Server) için verileri hazırlama](https://msdn.microsoft.com/library/ms188609)) konu.

Bulk INSERT için bazı örnek komutları şunlardır aşağıdaki şekilde şunlardır:  

1. Verilerinizi çözümlemek ve toomake hello SQL Server veritabanının aynı tarihleri gibi herhangi bir özel alan için format hello varsayar emin almadan önce tüm özel seçenekleri ayarlayın. Tooset hello tarih biçimini yıl ay-günlük (verileriniz yıl ay gün biçiminde hello tarih içeriyorsa) örneği şöyledir:

        SET DATEFORMAT ymd;    
2. Toplu içeri aktarma deyimlerini kullanarak veri içeri aktarın:

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>SQL Server'da yerleşik yardımcı programları
SQL Server tümleştirmeler Services (SSIS) tooimport verileri azure'da bir düz dosyadan SQL Server VM halinde kullanabilirsiniz.
SSIS iki studio ortamlarında kullanılabilir. Ayrıntılar için bkz [Integration Services (SSIS) ve Studio ortamları](https://technet.microsoft.com/library/ms140028.aspx):

* SQL Server veri araçları hakkında daha fazla bilgi için bkz: [Microsoft SQL Server veri araçları](https://msdn.microsoft.com/data/tools.aspx)  
* Merhaba İçeri/Dışarı Aktarma Sihirbazı hakkında daha fazla bilgi için bkz: [SQL Server içeri ve Dışarı Aktarma Sihirbazı](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Şirket içi SQL Server tooSQL bir Azure VM sunucuda taşıma verileri
Geçiş stratejilerini aşağıdaki hello de kullanabilirsiniz:

1. [Bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [TooFlat dosyası dışarı aktarma](#export-flat-file)
3. [SQL veritabanı Geçiş Sihirbazı](#sql-migration)
4. [Yukarı geri veritabanı ve geri yükleme](#sql-backup)

Biz bunların her biri aşağıda açıklanmıştır:

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma
Merhaba **bir SQL Server veritabanı tooa Microsoft Azure VM Sihirbazı'nı dağıtma** bir basit ve önerilen yol toomove bir şirket içi SQL Server örneği tooSQL bir Azure VM sunucuda verilerdir. Ayrıntılı adımlar yanı sıra tartışma diğer alternatifleri için bkz: [veritabanı tooSQL bir Azure VM sunucuda geçiş](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>TooFlat dosyası dışarı aktarma
Hello belirtildiği gibi çeşitli yöntemler kullanılan toobulk bir şirket içi SQL Server verileri dışa olabilir [toplu içeri ve dışarı aktarma veri (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) konu. Bu belge hello toplu kopyalama programı (BCP) örnek olarak ele alınacaktır. Veri düz bir dosyaya dışarı aktarıldıktan sonra içeri aktarılan tooanother SQL server toplu içeri kullanarak olabilir.

1. Şirket içi SQL Server tooa dosya Hello verilerini dışa aktarma hello bcp yardımcı programını şu şekilde kullanma

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. SQL Server VM hello kullanarak azure'da Hello veritabanı ve hello tablo oluşturmak `create database` ve `create table` 1. adımda dışarı hello tablo şeması için.
3. Merhaba verilerin dışa ve içe olmasıyla hello tablo şemasını tanımlayan bir biçim dosyası oluşturun. Merhaba biçim dosyası ayrıntılarını açıklanmıştır [(SQL Server) bir biçim dosyası oluşturma](https://msdn.microsoft.com/library/ms191516.aspx).

    Ne zaman gelen BCP çalıştıran izin ver hello SQL Server makinesinde biçim dosyası oluşturma

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Biçim dosyası oluşturma çalışırken BCP uzaktan karşı bir SQL Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Bölümünde açıklanan hello yöntemlerden birini kullanın [dosya kaynağı verilerini taşıma](#filesource_to_sqlonazurevm) düz dosyalar tooa SQL Server toomove hello verileri.

### <a name="sql-migration"></a>SQL veritabanı Geçiş Sihirbazı
[SQL Server veritabanı Geçiş Sihirbazı](http://sqlazuremw.codeplex.com/) iki SQL server örnekleri arasında veri kullanımı kolay şekilde toomove sağlar. Kaynak ve hedef tablolar arasında hello kullanıcı toomap hello veri şeması sağlar, sütun türleri ve diğer çeşitli işlevlerin seçin. Merhaba perde arkasında toplu kopyalama (BCP) kullanır. Bir ekran görüntüsünü hello hello SQL veritabanı Geçiş Sihirbazı'nı aşağıda gösterildiği ekran Hoş Geldiniz.  

![SQL Server Yükseltme Sihirbazı][2]

### <a name="sql-backup"></a>Yukarı geri veritabanı ve geri yükleme
SQL Server destekler:

1. [Veritabanı geri yukarı ve işlevlerin geri yüklenmesi](https://msdn.microsoft.com/library/ms187048.aspx) (her iki tooa yerel dosya ya da bacpac verme tooblob) ve [veri katmanı uygulamaları](https://msdn.microsoft.com/library/ee210546.aspx) (bacpac kullanarak).
2. Özelliği toodirectly SQL Server sanal makineleri Azure üzerinde bir kopyalanan veritabanı create veya kopyalama tooan var olan SQL Azure ile. Daha fazla ayrıntı için bkz: [kullanım hello kopyalama Veritabanı Sihirbazı](https://msdn.microsoft.com/library/ms188664.aspx).

Bir ekran görüntüsünü hello veritabanı geri yukarı/geri yükleme seçenekleri SQL Server Management Studio'dan aşağıda gösterilmiştir.

![SQL Server içeri aktarma aracı][1]

## <a name="resources"></a>Kaynaklar
[Veritabanı tooSQL bir Azure VM sunucuda geçirme](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Azure Sanal Makineler’de SQL Server’a genel bakış](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
