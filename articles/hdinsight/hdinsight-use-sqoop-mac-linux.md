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
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Apache Sqoop tooimport kullanın ve hdınsight'ta Hadoop ile SQL veritabanı arasında veri dışarı aktarma

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Azure Hdınsight ve Azure SQL Database veya Microsoft SQL Server veritabanı nasıl toouse Apache Sqoop tooimport ve dışarı aktarma arasında bir Hadoop küme öğrenin. Merhaba adımları bu belgenin kullanımı hello `sqoop` hello Hadoop kümesi hello headnode doğrudan komutu. SSH tooconnect toohello baş düğüm kullanın ve bu belgede hello komutları çalıştırın.

> [!IMPORTANT]
> Merhaba bu belgedeki adımlar yalnızca Linux kullanmak Hdınsight kümeleri ile çalışır. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="install-freetds"></a>Ücretsiz yükleyin

1. SSH tooconnect toohello Hdınsight kümesi kullanın. Örneğin, komutu aşağıdaki hello toohello birincil headnode adlı bir kümeye bağlanır `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Aşağıdaki komut tooinstall ücretsiz hello kullan:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    Ücretsiz çeşitli adımları tooconnect tooSQL veritabanı kullanılır.

## <a name="create-hello-table-in-sql-database"></a>SQL veritabanı'nda Hello tablosu oluşturma

> [!IMPORTANT]
> Merhaba Hdınsight kümesi kullanıyorsanız ve SQL veritabanı oluşturuldu [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md), bu bölümdeki hello adımları atlayın. Merhaba parçası hello adımları gibi hello veritabanı ve tablo oluşturulan [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md) belge.

1. Merhaba SSH oturumundan komutu tooconnect toohello SQL veritabanı sunucusu aşağıdaki hello kullanın.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Metin aşağıdaki çıktı benzer toohello alırsınız:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. Merhaba, `1>` isteminde, sorgu aşağıdaki hello girin:

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

    Ne zaman hello `GO` deyimi girilir, hello önceki deyimleri değerlendirilir. İlk olarak, hello **mobiledata** tablosu oluşturulur ve kümelenmiş bir dizin (SQL veritabanı tarafından gereklidir.) tooit eklenir

    Tablo hello sorgu tooverify aşağıdaki kullanım hello oluşturuldu:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Metin aşağıdaki çıktı benzer toohello bakın:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Girin `exit` hello adresindeki `1>` sor tooexit hello tsql yardımcı programı.

## <a name="sqoop-export"></a>Sqoop dışarı aktarma

1. Merhaba SSH bağlantı toohello kümeden Sqoop SQL veritabanınız görebilirsiniz komutu tooverify aşağıdaki hello kullan:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    İstendiğinde, hello parola hello SQL veritabanı oturum açma için girin.

    Bu komut hello dahil olmak üzere veritabanlarının listesini döndürür **sqooptest** daha önce oluşturduğunuz veritabanı.

2. tooexport verileri **hivesampletable** toohello **mobiledata** tablo, hello aşağıdaki komutu kullanın:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Bu komut Sqoop tooconnect toohello bildirir **sqooptest** veritabanı. Sqoop sonra verileri dışa aktarır **wasb: / / / hive/ambarı/hivesampletable** toohello **mobiledata** tablo.

    > [!IMPORTANT]
    > Kullanım `wasb:///` hello varsayılan depolama kümeniz için bir Azure depolama hesabı ise. Kullanım `adl:///` bir Azure Data Lake Store ise.

3. Merhaba komut tamamlandıktan sonra komut tooconnect toohello veritabanı TSQL kullanarak aşağıdaki hello kullanın:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Bağlandıktan sonra dışarı aktarılan toohello veri hello deyimleri tooverify aşağıdaki kullanım hello edildi **mobiledata** tablosu:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Merhaba tablodaki verileri listesini görmelisiniz. Tür `exit` tooexit hello tsql yardımcı programı.

## <a name="sqoop-import"></a>Sqoop alma

1. Kullanım hello şu komutu hello tooimport verileri **mobiledata** SQL veritabanındaki toohello tablosu **wasb: / / / öğreticileri/usesqoop/importeddata** hdınsight'ta dizin:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    Merhaba veri Hello alanları bir sekme karakteriyle ayrılır ve hello satırları yeni satır karakteri tarafından sonlandırılır.

2. Merhaba içeri aktarma tamamlandıktan sonra komut toolist hello dizininde bulunan verileri hello yeni çıkışı aşağıdaki hello kullanın:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>SQL Server kullanma

Ayrıca, Sqoop tooimport kullanmak ve verileri, veri merkezinizdeki veya Azure üzerinde barındırılan bir sanal makinede SQL Server'dan dışarı aktarma. SQL Database ve SQL Server kullanarak arasında hello farklılıklar şunlardır:

* Hdınsight ve SQL Server gerekir olması üzerinde hello aynı Azure sanal ağı.

    Merhaba bir örnek için bkz: [bağlanmak Hdınsight tooyour şirket içi ağ](./connect-on-premises-network.md) belge.

    Merhaba Hdınsight bir Azure sanal ağı ile kullanma hakkında daha fazla bilgi için bkz: [genişletmek Hdınsight Azure sanal ağ ile](hdinsight-extend-hadoop-virtual-network.md) belge. Azure sanal ağ ile ilgili daha fazla bilgi için bkz: Merhaba [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md) belge.

* SQL Server yapılandırılmış tooallow SQL kimlik doğrulaması olması gerekir. Daha fazla bilgi için bkz: Merhaba [bir kimlik doğrulama modu seçme](https://msdn.microsoft.com/ms144284.aspx) belge.

* Tooconfigure SQL Server tooaccept uzak bağlantıları olabilir. Daha fazla bilgi için bkz: Merhaba [nasıl tootroubleshoot bağlanan toohello SQL Server veritabanı altyapısı](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) belge.

* Merhaba oluşturma **sqooptest** gibi bir yardımcı programını kullanarak SQL Server veritabanında **SQL Server Management Studio** veya **tsql**. hello Azure CLI kullanma hello adımlar, yalnızca Azure SQL veritabanı için geçerlidir.

    Transact-SQL deyimleri toocreate hello aşağıdaki kullanım hello **mobiledata** tablosu:

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

* SQL Server toohello Hdınsight'ta bağlanırken hello SQL Server toouse başlangıç IP adresi olabilir. Örneğin:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Sınırlamalar

* Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.

* -Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop yapar hello INSERT işlemlerine toplu işleme yerine birden çok ekler.

## <a name="next-steps"></a>Sonraki adımlar

Öğrendiğiniz artık nasıl toouse Sqoop. toolearn daha bakın:

* [Hdınsight ile Oozie kullanma][hdinsight-use-oozie]: Oozie iş akışında kullanmak Sqoop eylem.
* [Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-data]: kullanmak Hive tooanalyze uçuş gecikme veri ve Sqoop tooexport veri tooan Azure SQL veritabanını kullanın.
* [Veri tooHDInsight karşıya][hdinsight-upload-data]: veri tooHDInsight/Azure Blob Depolama yüklemek için diğer yöntemler bulun.

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
