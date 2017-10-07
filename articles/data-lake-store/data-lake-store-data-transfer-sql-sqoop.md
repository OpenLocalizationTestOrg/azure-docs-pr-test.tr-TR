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
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Data Lake Store ile Sqoop kullanarak Azure SQL veritabanı arasında veri kopyalama
Bilgi nasıl Azure SQL veritabanı ve Data Lake Store arasında toouse Apache Sqoop tooimport ve dışarı aktarma veri.

## <a name="what-is-sqoop"></a>Sqoop nedir?
Büyük veri uygulamaları günlükleri ve dosyaları gibi yapılandırılmamış ve yarı yapılandırılmış veri işleme için doğal bir seçimdir. Ancak, aynı zamanda olabilir ilişkisel veritabanlarında depolanan bir gereksinim tooprocess yapılandırılmış veri.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) tasarlanmış aracı tootransfer ilişkisel veritabanları ve Data Lake Store gibi bir büyük veri deposu arasındaki verilerdir. Bunu Azure SQL veritabanı gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) tooimport verileri Data Lake Store kullanabilirsiniz. Ardından dönüştürme ve büyük veri iş yüklerini kullanarak hello verileri analiz ve bir RDBMS hello verilerini dışarı aktarın. Bu öğreticide, ilişkisel veritabanı tooimport/verme etki alanından farklı bir Azure SQL Database kullanın.

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* **Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile. Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md). Bu makalede, Data Lake Store erişimi olan bir Hdınsight Linux kümesi olduğunu varsayar.
* **Azure SQL veritabanı**. Yönergeler için toocreate bir, bkz: [bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Videolarla daha hızlı mı öğreniyorsunuz?
[Bu videoyu izleyin](https://mix.office.com/watch/1butcdjxmu114) nasıl toocopy verileri Azure Storage Bloblarında ve Distcp'yi kullanarak Data Lake Store arasında.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Örnek tablo hello Azure SQL veritabanı oluşturma
1. toostart ile iki örnek tablolar hello Azure SQL veritabanı oluşturun. Kullanım [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) veya Visual Studio tooconnect toohello Azure SQL veritabanı ve sonra çalışma hello aşağıdaki sorgular.

    **Tablo1 oluşturma**

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

    **Tablo2 oluşturma**

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
2. İçinde **tablo1**, bazı örnek veri ekleyin. Bırakın **tablo2** boş. Verileri içeri aktaracak **tablo1** Data Lake Store içine. Ardından, biz veri Data Lake Store verilecek **tablo2**. Aşağıdaki kod parçacığında hello çalıştırın.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Kullanım Sqoop bir Hdınsight kümesini gelen erişim tooData Lake deposu
Hdınsight kümesi hello Sqoop paketler zaten var. Ek depolama alanı hello Hdınsight küme toouse Data Lake Store yapılandırdıysanız, ilişkisel veritabanı (Bu örnekte, Azure SQL veritabanı) arasında (olmadan herhangi bir yapılandırma değişikliği) Sqoop tooimport/dışarı aktarma veri kullanabilirsiniz ve Data Lake Store hesabı.

1. Bu öğretici için SSH tooconnect toohello küme kullanması gereken şekilde Linux kümesi oluşturulan varsayalım. Bkz: [Bağlan tooa Linux tabanlı Hdınsight kümesi](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Merhaba kümeden hello Data Lake Store hesabı erişip erişemeyeceğini doğrulayın. Merhaba SSH isteminden komutu aşağıdaki hello çalıştırın:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Bu dosyalar/klasörler hello Data Lake Store hesabı içinde listesini sağlamanız gerekir.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Data Lake Store Azure SQL veritabanından veri içeri aktarın
1. Sqoop paketlerinin kullanılabildiği toohello dizinine gidin. Genellikle, bu anda olacaktır `/usr/hdp/<version>/sqoop/bin`.
2. Merhaba verileri alın **tablo1** hello Data Lake Store hesabı içine. Sözdizimi aşağıdaki hello kullan:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Unutmayın **sql veritabanı sunucusu adı** yer tutucu hello hello Azure SQL veritabanı çalıştığı hello sunucusunun adını temsil eder. **SQL veritabanı adı** yer tutucu hello gerçek veritabanı adını temsil eder.

    Örneğin,


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Veriler o hello toohello Data Lake Store hesabına transfer doğrulayın. Merhaba aşağıdaki komutu çalıştırın:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Çıktı aşağıdaki hello görmeniz gerekir.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Her **bölümü-m -*** dosya tooa satır hello kaynak tablosunda karşılık gelen **tablo1**. Merhaba bölümünün - m - hello içeriğini görüntüleyebilir * tooverify dosyaları.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Data Lake Store Azure SQL veritabanına verileri dışa
1. Data Lake Store hesabı toohello boş tablosundan Hello verilerini dışa **tablo2**, hello Azure SQL veritabanı içinde. Sözdizimi aşağıdaki hello kullanın.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Örneğin,


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Veri olan bu hello toohello SQL veritabanı tablosu karşıya doğrulayın. Kullanım [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) veya Visual Studio tooconnect toohello Azure SQL veritabanı ve sonra çalışma hello aşağıdaki sorgu.

        SELECT * FROM TABLE2

    Çıktı aşağıdaki hello sahip olması gerekir.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Sqoop kullanırken performans etkenleri

Performans, Sqoop ayarlama toocopy veri tooData Lake deposu işi için bkz: [Sqoop performans belge](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama](data-lake-store-copy-data-azure-storage-blob.md)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
