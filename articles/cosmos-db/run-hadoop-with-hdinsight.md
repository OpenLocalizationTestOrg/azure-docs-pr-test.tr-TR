---
title: "bir Hadoop aaaRun iş Azure Cosmos DB ve Hdınsight kullanarak | Microsoft Docs"
description: "Azure Cosmos DB ve Azure Hdınsight ile nasıl toorun basit bir Hive, Pig ve MapReduce işi öğrenin."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Azure Cosmos DB ve Hdınsight kullanarak bir Apache Hive, Pig veya Hadoop işini çalıştır
Bu öğretici şunların nasıl yapıldığını gösterir toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], ve [Apache Hadoop] [ apache-hadoop] Cosmos veritabanı Hadoop Bağlayıcısı ile MapReduce işleri Azure hdınsight'ta. Cosmos veritabanı Hadoop Bağlayıcısı Cosmos DB tooact hem kaynak hem de Hive, Pig ve MapReduce işleri için havuz olarak sağlar. Bu öğretici için Hadoop işlerini Cosmos DB hello veri kaynağı ve hedef kullanır.

Bu öğreticiyi tamamladıktan sonra aşağıdaki soruları mümkün tooanswer hello olması:

* Cosmos Hive, Pig ve MapReduce işi kullanılarak DB'den nasıl veri yükleme?
* Cosmos Hive, Pig ve MapReduce işi kullanılarak DB'de nasıl veri depoluyor?

Video, biz Cosmos DB Hdınsight ile Hive işi çalıştırdığı aşağıdaki hello izleyerek çalışmaya başlamanızı öneririz.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

Ardından, toothis makalesi, nasıl Cosmos DB verilerinizde analytics işlerine çalıştırabilirsiniz hello tam Ayrıntılar burada alırsınız döndür.

> [!TIP]
> Bu öğretici, Apache Hadoop, Hive ve/veya Pig kullanma konusunda deneyim sahibi olduğunuzu varsayar. Yeni tooApache Hadoop, Hive veya Pig varsa, hello ziyaret öneririz [Apache Hadoop belgeleri][apache-hadoop-doc]. Bu öğreticinin ayrıca Cosmos DB ile konusunda deneyim sahibi ve bir Cosmos DB hesabına sahip olduğunu varsayar. Lütfen yeni tooCosmos DB ya Cosmos DB hesabınız varsa kullanıma bizim [Başlarken] [ getting-started] sayfası.
>
>

Öğretici hello ve Hive, Pig ve MapReduce tooget hello tam örnek PowerShell komut dosyaları yalnızca istediğiniz zaman toocomplete yok mu? Bir sorun bunları getirmek [burada][hdinsight-samples]. Merhaba indirme Ayrıca bu örnekleri için hello hql, pig ve java dosyaları içerir.

## <a name="NewestVersion"></a>En yeni sürümü
<table border='1'>
    <tr><th>Hadoop Bağlayıcısı sürüm</th>
        <td>1.2.0</td></tr>
    <tr><th>Betik URI'si</th>
        <td>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>Değiştirilme tarihi</th>
        <td>04/26/2016</td></tr>
    <tr><th>Desteklenen Hdınsight sürümleri</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>Değişiklik günlüğü</th>
        <td>Güncelleştirilmiş Azure Cosmos DB Java SDK too1.6.0</br>
            Bir kaynak ve havuz olarak bölümlenmiş koleksiyonlar için destek eklendi</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Önkoşullar
Bu öğreticide Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:

* Cosmos DB hesabı, bir veritabanı ve belgeleri içinde ile bir koleksiyon. Daha fazla bilgi için bkz: [Cosmos DB ile çalışmaya başlama][getting-started]. Cosmos DB hesabınızla hello örnek veri aktarmak [Cosmos DB içeri aktarma aracını][import-data].
* Üretilen iş. Okuma ve yazma hdınsight'tan sayılır, Koleksiyonlarınız için ayrılan isteği birimlerinizi bulunun.
* Ek bir saklı yordam içinde her kapasiteyi koleksiyonu çıktı. Merhaba depolanan yordamlar, sonuçta elde edilen belgeler aktarmak için kullanılır.
* Merhaba elde edilen hello Hive, Pig ve MapReduce işleri belgelerden kapasitesi.
* [*İsteğe bağlı*] kapasite için ek bir koleksiyonu.

> [!WARNING]
> Sipariş tooavoid hello oluşturulmasında hello işleri hiçbirini sırasında yeni bir koleksiyon, hello sonuçları toostdout yazdırma, hello çıktı tooyour WASB kapsayıcısını kaydedin veya zaten mevcut bir koleksiyonu belirtin. Mevcut bir koleksiyonu belirtmenin hello durumda da, yeni belgeler hello koleksiyon içinde oluşturulur ve zaten var olan belgeler, yalnızca bir çakışma varsa etkilenir *kimlikleri*. **Merhaba bağlayıcı otomatik olarak üzerine yazılacak varolan belgeleri kimliği çakışıyor**. Merhaba upsert seçeneği toofalse ayarlayarak bu özelliği devre dışı bırakabilir. Upsert false ise ve bir çakışma oluşur, hello Hadoop işi başarısız olur; bir kimliği çakışma hata raporlama.
>
>

## <a name="ProvisionHDInsight"></a>1. adım: yeni bir Hdınsight kümesi oluşturma
Bu öğretici, Hdınsight kümenize hello Azure Portal toocustomize betik eylemi kullanır. Bu öğreticide, Hdınsight kümenize hello Azure Portal toocreate kullanacağız. Yönergeler için nasıl toouse PowerShell cmdlet'lerini veya Hdınsight .NET SDK'sı, hello kullanıma [özelleştirme Hdınsight kümeleri betik eylemi kullanarak] [ hdinsight-custom-provision] makalesi.

1. İçinde toohello oturum [Azure Portal][azure-portal].
2. Tıklatın **+ yeni** sol gezinti hello hello üstte arama **Hdınsight** hello yeni dikey penceresinde hello en üstteki arama çubuğunda.
3. **Hdınsight** tarafından yayımlanan **Microsoft** hello sonuçları hello üstünde görünür. Tıklayın ve ardından **oluşturma**.
4. Merhaba yeni Hdınsight kümesi üzerinde oluştur dikey penceresi, girin, **küme adı** ve select hello **abonelik** altında bu kaynak tooprovision istiyor.

    <table border='1'>
        <tr><td>Küme adı</td><td>Merhaba küme adı.<br/>
DNS adı olmalıdır başlangıç ve bitiş bir alfasayısal karakter ile ve kısa çizgi içerebilir.<br/>
Merhaba alan 3 ile 63 karakter arasında bir dize olmalıdır.</td></tr>
        <tr><td>Abonelik adı</td>
            <td>Birden fazla Azure aboneliğiniz varsa, Hdınsight kümenize barındıracak hello aboneliği seçin. </td></tr>
    </table>
5.Tıklatın **küme türü seçin** ve Özellikler toohello aşağıdaki kümesi hello belirtilen değerleri.

    <table border='1'>
        <tr><td>Küme türü</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Küme katmanı</td><td><strong>Standart</strong></td></tr>
        <tr><td>İşletim Sistemi</td><td><strong>Windows</strong></td></tr>
        <tr><td>Sürüm</td><td>En son sürümü</td></tr>
    </table>

    Şimdi, **seçin**.

    ![Hadoop Hdınsight ilk küme ayrıntılarını sağlayın][image-customprovision-page1]
6. Tıklayın **kimlik bilgileri** tooset oturum açma ve Uzaktan erişim kimlik bilgileri. Seçin, **küme oturum açma kullanıcı** ve **küme oturum açma parolası**.

    Kümenizi tooremote istiyorsanız seçin *Evet* hello dikey penceresinde hello altındaki bir kullanıcı adı ve parolasını girin.
7. Tıklayın **veri kaynağı** tooset birincil konumunuz verileri için erişim. Merhaba seçin **seçim yöntemini** ve zaten varolan bir depolama hesabını belirtin veya yeni bir tane oluşturun.
8. Üzerinde Merhaba aynı dikey penceresinde, belirtin bir **varsayılan kapsayıcı** ve **konumu**. Ve tıklayın **seçin**.

   > [!NOTE]
   > Bir konumu Kapat tooyour Cosmos DB hesap bölge daha iyi performans için seçin
   >
   >
9. Tıklayın **fiyatlandırma** tooselect hello sayısı ve düğüm türü. Merhaba varsayılan yapılandırması ve ölçek hello çalışan düğüm sayısı daha sonra tutabilirsiniz.
10. Tıklatın **isteğe bağlı yapılandırma**, ardından **betik eylemleri** hello isteğe bağlı yapılandırma dikey olarak.

     Betik eylemleri bilgi toocustomize aşağıdaki hello Hdınsight kümenize girin.

     <table border='1'>
         <tr><th>Özellik</th><th>Değer</th></tr>
         <tr><td>Ad</td>
             <td>Merhaba betik eylemi için bir ad belirtin.</td></tr>
         <tr><td>Betik URI'si</td>
             <td>Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin.</br></br>
Lütfen girin: </br> <strong>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>Baş</td>
             <td>Merhaba onay kutusunu toorun hello PowerShell betiğini hello baş düğümü tıklatın.</br></br>
             <strong>Bu onay kutusunu işaretleyin</strong>.</td></tr>
         <tr><td>Çalışan</td>
             <td>Merhaba onay kutusunu toorun hello PowerShell betiğini hello çalışan düğümüne tıklayın.</br></br>
             <strong>Bu onay kutusunu işaretleyin</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Merhaba onay kutusunu toorun hello PowerShell betiğini hello Zookeeper'ı tıklatın.</br></br>
             <strong>Gerekli</strong>.
             </td></tr>
         <tr><td>Parametreler</td>
             <td>Merhaba komut dosyası için gereken Hello parametreleri belirtin.</br></br>
             <strong>Gerekli parametre</strong>.</td></tr>
     </table>
11.Ya da oluşturma yeni bir **kaynak grubu** veya varolan bir kaynak grubunu Azure aboneliğinizdeki kullanın.
12. Şimdi, denetleme **PIN toodashboard** tootrack tıklatın ve dağıtım **oluşturma**!

## <a name="InstallCmdlets"></a>Azure PowerShell'i 2. adım: Yükleme ve yapılandırma
1. Azure PowerShell'i yükleyin. Yönergeler için bkz [burada][powershell-install-configure].

   > [!NOTE]
   > Alternatif olarak, Hive sorguları olduğu için Hdınsight'ın çevrimiçi Hive Düzenleyicisi'ni kullanabilirsiniz. toodo toohello bu nedenle, oturum [Azure Portal][azure-portal], tıklatın **Hdınsight** üzerinde hello sol bölmede tooview Hdınsight kümelerinizi listesi. Toorun Hive sorguları istiyor ve ardından hello kümesine tıklayın **sorgu konsol**.
   >
   >
2. Hello Azure PowerShell Tümleşik komut dosyası ortamı açın:

   * Windows 8 veya Windows Server 2012 veya sonraki sürümlerini çalıştıran bir bilgisayarda hello yerleşik kullanabilirsiniz arama. Merhaba başlangıç ekranından yazın **powershell ISE** tıklatıp **Enter**.
   * Windows 8 veya Windows Server 2012'den önceki bir sürümünü çalıştıran bir bilgisayarda, hello Başlat menüsünü kullanın. Merhaba Başlat menüsünden yazın **komut istemi** hello arama kutusunda sonra sonuçları hello listesini tıklatın **komut istemi**. Hello komut istemi, yazın **powershell_ise** tıklatıp **Enter**.
3. Azure hesabınızda ekleyin.

   1. Hello Konsol bölmesinde, yazın **Add-AzureAccount** tıklatıp **Enter**.
   2. Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**.
   3. Azure aboneliğiniz hello parolasını yazın.
   4. Tıklatın **oturum**.
4. Diyagram aşağıdaki hello Azure PowerShell komut dosyası ortamınızın hello önemli bölümleri tanımlar.

    ![Azure PowerShell diyagramı][azure-powershell-diagram]

## <a name="RunHive"></a>3. adım: Cosmos DB Hdınsight ile Hive işi çalıştırma
> [!IMPORTANT]
> Yapılandırma ayarlarınızı kullanarak < > tarafından belirtilen tüm değişkenleri doldurulması gerekir.
>
>

1. PowerShell betik bölmesinde değişkenleri aşağıdaki hello ayarlayın.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Sorgu dizesi oluşturma başlayalım. Biz tüm belgeleri sistem tarafından oluşturulan zaman damgaları (_ts) ve bir Azure Cosmos DB koleksiyonundan benzersiz kimlikler (_rid) alır, tüm belgeleri hello dakikaya göre hesaplar ve ardından geri yeni bir Azure Cosmos DB koleksiyona hello sonuçları depolayan bir Hive sorgusu yazacaksınız.</p>

    <p>İlk olarak, bir Hive tablosu bizim Azure Cosmos DB koleksiyonundan oluşturalım. Aşağıdaki kod parçacığını toohello PowerShell betik bölmesine hello eklemek <strong>sonra</strong> hello kod parçacığı # 1. Bizim belgeleri toojust _ts ve _rid hello isteğe bağlı DocumentDB.query t parametresi kırpma eklediğinizden emin olun.</p>

   > [!NOTE]
   > **DocumentDB.inputCollections adlandırma bir hata oldu.** Evet, bir giriş olarak birden çok koleksiyon ekleme ver: </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. Ardından, bir Hive tablosu hello çıkış koleksiyon için oluşturalım. Merhaba çıkış belge özellikleri hello ay, gün, saat, dakika ve hello toplam sayısı olacaktır.

   > [!NOTE]
   > **Henüz bir yeniden adlandırma DocumentDB.outputCollections bir hata oldu.** Evet, çıkış olarak birden çok koleksiyon ekleme ver: </br>
   > '*DocumentDB.outputCollections*'='*\<DocumentDB çıkış koleksiyon adı 1\>*,*\<DocumentDB çıkış koleksiyon adı 2\>* ' </br> Merhaba koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır. </br></br>
   > Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır. Belgeleri toplu bir koleksiyonda depolanacak sonra ikinci bir toplu iş belgelerin hello sonraki koleksiyonu ve benzeri depolanır.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Son olarak, şirketinizdeki ay, gün, saat ve dakika ve INSERT hello sonuçları hello uygulamasına geri tarafından tally hello belge Hive tablosu çıktı.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Kod parçacığı toocreate bir Hive işi tanımı hello önceki sorgu aşağıdaki hello ekleyin.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    Aynı zamanda hello - dosya geçiş toospecify HDFS üzerinde HiveQL komut dosyası.
4. Aşağıdaki kod parçacığında toosave hello başlangıç saati hello ekleyin ve hello Hive işi göndermek.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Merhaba Hive işi toocomplete toowait aşağıdaki hello ekleyin.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Tooprint hello standart çıktı hello başlatın ve aşağıdaki hello ekleyin ve bitiş saatlerini.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Çalıştırma** yeni kodunuzu! **Tıklatın** hello yeşil düğmesi yürütün.
8. Merhaba sonuçlarını denetleyin. Merhaba içine oturum [Azure Portal][azure-portal].

   1. Tıklatın <strong>Gözat</strong> hello sol taraftaki panelindeki. </br>
   2. Tıklatın <strong>her şeyi</strong> hello üst-panelin sağ tarafındaki hello göz atın. </br>
   3. Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>. </br>
   4. Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen hello çıkış koleksiyonu ile ilişkili Hive sorgunuzu.</br>
   5. Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</br></p>

   Hive sorgunuzu hello sonuçları görürsünüz.

   ![Hive sorgusu sonuçları][image-hive-query-results]

## <a name="RunPig"></a>Adım 4: Cosmos DB Hdınsight ile Pig işi çalıştırma
> [!IMPORTANT]
> Yapılandırma ayarlarınızı kullanarak < > tarafından belirtilen tüm değişkenleri doldurulması gerekir.
>
>

1. PowerShell betik bölmesinde değişkenleri aşağıdaki hello ayarlayın.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Sorgu dizesi oluşturma başlayalım. Biz tüm belgeleri sistem tarafından oluşturulan zaman damgaları (_ts) ve bir Azure Cosmos DB koleksiyonundan benzersiz kimlikler (_rid) alır, tüm belgeleri hello dakikaya göre hesaplar ve ardından geri yeni bir Azure Cosmos DB koleksiyona hello sonuçları depolayan bir Pig sorgu yazacaksınız.</p>
    <p>İlk olarak, belge Hdınsight'a Cosmos DB'den yükleme. Aşağıdaki kod parçacığını toohello PowerShell betik bölmesine hello eklemek <strong>sonra</strong> hello kod parçacığı # 1. Tooadd bir DocumentDB sorgu toohello isteğe bağlı DocumentDB sorgu parametresi tootrim bizim belgeleri toojust _ts ve _rid emin olun.</p>

   > [!NOTE]
   > Evet, bir giriş olarak birden çok koleksiyon ekleme ver: </br>
   > '*\<DocumentDB giriş koleksiyon adı 1\>*,*\<DocumentDB giriş koleksiyon adı 2\>*'</br> Merhaba koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır. </b>
   >
   >

    Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır. Belgeleri toplu bir koleksiyonda depolanacak sonra ikinci bir toplu iş belgelerin hello sonraki koleksiyonu ve benzeri depolanır.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Ardından, şimdi hello belgeleri hello ay, gün, saat, dakika ve hello toplam sayısı tarafından tally.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Son olarak, şirketinizdeki hello sonuçları bizim yeni çıkış koleksiyona depolar.

   > [!NOTE]
   > Evet, çıkış olarak birden çok koleksiyon ekleme ver: </br>
   > '\<DocumentDB çıkış koleksiyon adı 1\>,\<DocumentDB çıkış koleksiyon adı 2\>'</br> Merhaba koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</br>
   > Belgeleri dağıtılmış hepsini birden çok koleksiyon hello arasında olmalıdır. Belgeleri toplu bir koleksiyonda depolanacak sonra ikinci bir toplu iş belgelerin hello sonraki koleksiyonu ve benzeri depolanır.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Kod parçacığı toocreate Pig iş tanımı hello önceki sorgu aşağıdaki hello ekleyin.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    Aynı zamanda hello - dosya geçiş toospecify HDFS üzerinde Pig betiği.
6. Aşağıdaki kod parçacığında toosave hello başlangıç saati hello ekleyin ve hello Pig işi göndermek.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Merhaba Pig işi toocomplete toowait aşağıdaki hello ekleyin.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Tooprint hello standart çıktı hello başlatın ve aşağıdaki hello ekleyin ve bitiş saatlerini.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Çalıştırma** yeni kodunuzu! **Tıklatın** hello yeşil düğmesi yürütün.
10. Merhaba sonuçlarını denetleyin. Merhaba içine oturum [Azure Portal][azure-portal].

    1. Tıklatın <strong>Gözat</strong> hello sol taraftaki panelindeki. </br>
    2. Tıklatın <strong>her şeyi</strong> hello üst-panelin sağ tarafındaki hello göz atın. </br>
    3. Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>. </br>
    4. Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen hello çıkış koleksiyonu ile ilişkili Pig sorgunuzu.</br>
    5. Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</br></p>

    Pig sorgunuzu hello sonuçları görürsünüz.

    ![Pig sorgu sonuçları][image-pig-query-results]

## <a name="RunMapReduce"></a>5. adım: Azure Cosmos DB Hdınsight ile MapReduce işi çalıştırma
1. PowerShell betik bölmesinde değişkenleri aşağıdaki hello ayarlayın.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Biz hello Azure Cosmos DB koleksiyondaki her bir belge özellik için yineleme sayısı hesaplayan bir MapReduce işi yürüteceksiniz. Bu kod parçacığını ekleyin **sonra** yukarıdaki hello parçacığında.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar hello özel yüklemesi hello Cosmos DB Hadoop bağlayıcı ile gelir.
   >
   >
3. Komut toosubmit hello MapReduce işi aşağıdaki hello ekleyin.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Ayrıca toohello MapReduce iş tanımı, size ayrıca toorun hello MapReduce işi ve hello kimlik bilgilerini istediğiniz yere hello Hdınsight küme adını belirtin. Merhaba başlangıç AzureHDInsightJob zaman bir çağrıdır. Merhaba işin kullanım hello toocheck hello tamamlama *bekleme AzureHDInsightJob* cmdlet'i.
4. Komut toocheck aşağıdaki hello hatalarını çalışan hello MapReduce işi ile ekleyin.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Çalıştırma** yeni kodunuzu! **Tıklatın** hello yeşil düğmesi yürütün.
6. Merhaba sonuçlarını denetleyin. Merhaba içine oturum [Azure Portal][azure-portal].

   1. Tıklatın <strong>Gözat</strong> hello sol taraftaki panelindeki.
   2. Tıklatın <strong>her şeyi</strong> hello üst-panelin sağ tarafındaki hello göz atın.
   3. Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.
   4. Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen hello çıkış koleksiyonu ile ilişkili MapReduce işi.
   5. Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.

      MapReduce işi hello sonuçları görürsünüz.

      ![MapReduce sorgu sonuçları][image-mapreduce-query-results]

## <a name="NextSteps"></a>Sonraki Adımlar
Tebrikler! Yalnızca Azure Cosmos DB ve Hdınsight kullanarak, ilk Hive, Pig ve MapReduce işleri çalıştırdığınız.

Bizim açık kaynaklıdır bizim Hadoop bağlayıcı. İlginizi çekiyorsa üzerinde katkıda bulunabilirsiniz [GitHub][github].

toolearn daha makaleler hello bakın:

* [Documentdb ile bir Java uygulaması geliştirme][documentdb-java-application]
* [Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek][hdinsight-develop-deploy-java-mapreduce]
* [Hadoop ile Hive Hdınsight tooanalyze mobil ahize kullanımda kullanmaya başlama][hdinsight-get-started]
* [Hdınsight ile MapReduce kullanma][hdinsight-use-mapreduce]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Betik eylemi kullanarak Hdınsight kümelerini özelleştirme][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
