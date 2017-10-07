---
title: "aaaUse hdınsight'ta Hadoop Oozie Düzenleyicisi zamana dayalı | Microsoft Docs"
description: "Hdınsight, büyük veri hizmeti zamana dayalı Hadoop Oozie düzenleyicisi kullanın. Bilgi nasıl toodefine Oozie iş akışları ve düzenleyicileri ve işleri göndermek."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Hdınsight toodefine akışlarında Hadoop ile zamana dayalı Oozie düzenleyicisi kullanın ve işleri koordine
Bu makalede, nasıl toodefine iş akışları ve düzenleyiciler ve nasıl tootrigger hello Düzenleyicisi işleri, zamana dayalı öğreneceksiniz. Aracılığıyla yararlı toogo olan [Hdınsight ile kullanım Oozie] [ hdinsight-use-oozie] önce bu makaleyi okuyun. Ayrıca tooOozie, Azure Data Factory kullanarak işleri de zamanlayabilirsiniz. Azure Data Factory toolearn bkz [kullanım Pig ve Hive Data Factory ile](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Bu makalede Windows tabanlı Hdınsight kümesi gerektirir. Oozie, Linux tabanlı bir kümede zaman tabanlı işleri de dahil olmak üzere kullanma hakkında bilgi için bkz: [kullanım Oozie Hadoop toodefine ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırma](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Oozie nedir
Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir. Merhaba Hadoop yığını ile tümleştirilir ve Apache MapReduce, Apache Pig, Apache Hive ve Apache Sqoop için Hadoop işlerini destekler. Ayrıca, Java programları veya kabuk betikleri gibi belirli tooa sistem kullanılan tooschedule işler de olabilir.

Merhaba aşağıdaki resimde, gerçekleştireceksiniz hello iş akışı gösterilmiştir:

![İş akışı diyagramı][img-workflow-diagram]

Merhaba iş akışı iki eylemleri içerir:

1. Bir Hive eylem HiveQL betiğini toocount hello log4j günlük dosyasına günlük düzeyi türlerinin oluşumları çalıştırır. Her log4j günlük bir [günlük düzeyi] alan tooshow hello türü ve hello önem derecesi, örneğin içeren bir dizi alanlarının oluşur:

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    Merhaba Hive betik çıktısı benzer:

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].
2. Sqoop eylemin hello HiveQL eylem çıktı tooa tablosu bir Azure SQL veritabanında dışa aktarır. Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop].

> [!NOTE]
> Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler nelerdir?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Azure PowerShell içeren bir iş istasyonu**.

    > [!IMPORTANT]
    > Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışıdır** ve 1 Ocak 2017 tarihine kadar kaldırılacaktır. Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.
    >
    > Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü. Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.

* **Hdınsight kümesi**. Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight kümeleri oluşturma][hdinsight-provision], veya [Hdınsight kullanmaya başlama][hdinsight-get-started]. Başlangıç Öğreticisi aracılığıyla veri toogo aşağıdaki hello gerekir:

    <table border = "1">
    <tr><th>Küme özelliği</th><th>Windows PowerShell değişken adı</th><th>Değer</th><th>Açıklama</th></tr>
    <tr><td>Hdınsight küme adı</td><td>$clusterName</td><td></td><td>Bu öğretici çalışacağı hello Hdınsight kümesi.</td></tr>
    <tr><td>Hdınsight küme kullanıcı</td><td>$clusterUsername</td><td></td><td>Merhaba Hdınsight küme kullanıcı adı. </td></tr>
    <tr><td>Hdınsight küme kullanıcı parolası </td><td>$clusterPassword</td><td></td><td>Merhaba Hdınsight küme kullanıcı parolası.</td></tr>
    <tr><td>Azure depolama hesabı adı</td><td>$storageAccountName</td><td></td><td>Azure depolama hesabı kullanılabilir toohello Hdınsight kümesi. Bu öğretici için hello küme sağlama işlemi sırasında belirtilen hello varsayılan depolama hesabı kullanın.</td></tr>
    <tr><td>Azure Blob kapsayıcı adı</td><td>$containerName</td><td></td><td>Bu örnekte, hello varsayılan Hdınsight küme dosya sistemi için kullanılan hello Azure Blob Depolama kapsayıcısını kullanın. Varsayılan olarak, aynı hello Hdınsight kümesi olarak ad hello içeriyor.</td></tr>
    </table>
* **Bir Azure SQL veritabanı**. Merhaba SQL veritabanı sunucusu tooallow erişimi için bir güvenlik duvarı kuralı istasyonunuzdan yapılandırmanız gerekir. Bir Azure SQL veritabanı oluşturma ve hello güvenlik duvarını yapılandırma hakkında yönergeler için bkz. [Azure SQL veritabanı ile çalışmaya başlamak] [sqldatabase-get-started]. Bu makalede, Bu öğretici için gereksinim duyduğunuz hello Azure SQL veritabanı tablosu oluşturmak için bir Windows PowerShell komut dosyası sağlar.

    <table border = "1">
    <tr><th>SQL veritabanı özelliği</th><th>Windows PowerShell değişken adı</th><th>Değer</th><th>Açıklama</th></tr>
    <tr><td>SQL veritabanı sunucusu adı</td><td>$sqlDatabaseServer</td><td></td><td>Merhaba SQL veritabanı sunucusu toowhich Sqoop veri aktarır. </td></tr>
    <tr><td>SQL veritabanı oturum açma adı</td><td>$sqlDatabaseLogin</td><td></td><td>SQL veritabanı oturum açma adı.</td></tr>
    <tr><td>SQL veritabanı oturum açma parolası</td><td>$sqlDatabaseLoginPassword</td><td></td><td>SQL veritabanı oturum açma parolası.</td></tr>
    <tr><td>SQL veritabanı adı</td><td>$sqlDatabaseName</td><td></td><td>Hello Azure SQL veritabanı toowhich Sqoop veri aktarır. </td></tr>
    </table>

  > [!NOTE]
  > Varsayılan olarak, Azure Hdınsight gibi Azure hizmetlerinden bağlantıları bir Azure SQL veritabanı sağlar. Bu güvenlik duvarı ayarı devre dışıysa, hello Azure Portalı ' etkinleştirmeniz gerekir. Bir SQL veritabanı oluşturma ve güvenlik duvarı kuralları yapılandırma hakkında daha fazla yönerge için bkz: [oluşturma ve yapılandırma SQL veritabanı][sqldatabase-get-started].

> [!NOTE]
> Merhaba tablolardaki doldurma hello değerleri. Bu öğreticide olmaya yardımcı olacaktır.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Merhaba HiveQL betiğini ilgili ve Oozie iş akışı tanımlama
Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır. Merhaba varsayılan iş akışı dosya adı *workflow.xml*.  Merhaba iş akışı dosyasını yerel olarak kaydedin ve ardından daha sonra Bu öğreticide Azure PowerShell kullanarak toohello Hdınsight kümesi dağıtın.

Merhaba Hive eylemin hello iş akışında bir HiveQL komut dosyasını çağırır. Bu komut dosyasını üç HiveQL ifadelerini içerir:

1. **Merhaba DROP TABLE deyimi** siler hello log4j Hive tablosu varsa.
2. **Merhaba CREATE TABLE deyimi** toohello günlük dosyasının konumu hello log4j; gösteren bir log4j Hive dış tablo oluşturur
3. **Merhaba hello log4j günlük dosyasının konumunu**. Merhaba alan sınırlayıcı ",". Merhaba varsayılan satır ayırıcı "\n" dir. Birden çok kez toorun hello Oozie iş akışı istemeniz durumunda Hive dış tablo hello özgün konumundan kaldırılmakta kullanılan tooavoid hello veri dosyasıdır.
4. **Merhaba Ekle üzerine deyimi** her günlük düzeyi türünden hello oluşumlarını sayar log4j Hive tablosu hello ve hello çıkış tooan Azure Blob Depolama konumu kaydeder.

> [!NOTE]
> Bilinen bir Hive yolu sorun yoktur. Bu sorunla Oozie iş gönderirken çalışır. Merhaba yönergeleri hello sorunu düzeltme hello TechNet Wiki üzerinde bulunabilir: [Hdınsight Hive hata: oluşturulamıyor toorename][technetwiki-hive-error].

**Merhaba akışı tarafından çağırılan toodefine hello HiveQL komut dosyası toobe**

1. Bir metin dosyası aşağıdaki hello ile içerik oluşturun:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Merhaba komut dosyasında kullanılan üç değişkenleri şunlardır:

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     Merhaba iş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu değerleri toothis HiveQL betiğini çalışma zamanında geçer.
2. Merhaba dosyası olarak kaydetmeniz **C:\Tutorials\UseOozie\useooziewf.hql** ANSI (ASCII) kodlama kullanılarak. (Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.) Bu komut dosyası dağıtılan toohello Hdınsight kümesi daha sonra hello öğreticide olacaktır.

**toodefine bir iş akışı**

1. Bir metin dosyası aşağıdaki hello ile içerik oluşturun:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    Merhaba iş akışında tanımlanan iki eylemler vardır. Merhaba start-tooaction olan *RunHiveScript*. Merhaba eylem çalıştırıyorsa *Tamam*, hello İleri eylem *RunSqoopExport*.

    Merhaba RunHiveScript birkaç değişkeni yok. Azure PowerShell kullanarak hello Oozie iş istasyonunuzdan gönderdiğinizde hello değerler geçer.

    İş akışı değişkenleri

    <table border = "1">
    <tr><th>İş akışı değişkenleri</th><th>Açıklama</th></tr>
    <tr><td>${Jobtracker'a}</td><td>Merhaba Hadoop işi İzleyicisi Merhaba URL'sini belirtin. Kullanım <strong>jobtrackerhost:9010</strong> Hdınsight sürüm 3.0 ve 2.0 küme.</td></tr>
    <tr><td>${İş}</td><td>Merhaba Hadoop adı düğümü Hello URL'sini belirtin. Merhaba varsayılan dosya sistemi wasb kullanın: / / adres, örneğin, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
    <tr><td>${queueName}</td><td>İş hello hello sıra adı için gönderilen belirtir. Kullanım <strong>varsayılan</strong>.</td></tr>
    </table>

    Hive eylem değişkenleri

    <table border = "1">
    <tr><th>Eylem değişkeni yığını</th><th>Açıklama</th></tr>
    <tr><td>${hiveDataFolder}</td><td>Merhaba Hive Create Table komutu için kaynak dizini Hello.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>Merhaba Ekle üzerine deyimi için Hello çıkış klasörü.</td></tr>
    <tr><td>${hiveTableName}</td><td>Merhaba log4j veri dosyalarına başvuran hello Hive tablosu Hello adı.</td></tr>
    </table>

    Sqoop eylem değişkenleri

    <table border = "1">
    <tr><th>Sqoop eylem değişkeni</th><th>Açıklama</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>SQL veritabanı bağlantı dizesi.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>Hello Azure SQL veritabanı tablosu toowhere hello verileri dışarı aktarılır.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>Merhaba Hive Ekle üzerine deyimi için Hello çıkış klasörü. Merhaba budur aynı klasöre hello Sqoop verme (verme-dir).</td></tr>
    </table>

    Oozie iş akışı ve hello iş akışı eylemlerinin kullanma hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (için Hdınsight kümesi sürüm 3.0) veya [Apache Oozie 3.3.2 Belge] [ apache-oozie-332] (için Hdınsight kümesi sürüm 2.1).

1. Merhaba dosyası olarak kaydetmeniz **C:\Tutorials\UseOozie\workflow.xml** ANSI (ASCII) kodlama kullanılarak. (Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.)

**toodefine Düzenleyicisi**

1. Bir metin dosyası aşağıdaki hello ile içerik oluşturun:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Merhaba tanım dosyasında kullanılan beş değişkenleri şunlardır:

   | Değişken | Açıklama |
   | --- | --- |
   | ${coordFrequency} |İş duraklatma süresi. Sıklık, her zaman dakika cinsinden ifade edilir. |
   | ${coordStart} |İş başlangıç zamanı. |
   | ${coordEnd} |İş bitiş saati. |
   | ${coordTimezone} |Oozie Düzenleyicisi işleri sabit bir saat diliminde hiçbir gün ışığından yararlanma saati (UTC kullanarak tipik olarak gösterilir) ile işler. Bu saat dilimi hello "Oozie işleme saat dilimi." olarak adlandırılır |
   | ${wfPath} |Merhaba workflow.xml Hello yolu.  Merhaba iş akışı dosyası adı hello varsayılan dosya adı (workflow.xml) değilse, belirtmeniz gerekir. |
2. Merhaba dosyası olarak kaydetmeniz **C:\Tutorials\UseOozie\coordinator.xml** ANSI (ASCII) hello kodlama kullanılarak. (Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Merhaba Oozie projesini dağıtma ve hello öğretici hazırlama
Bir Azure PowerShell komut dosyası tooperform hello aşağıdaki çalışır:

* Kopya hello HiveQL betiğini (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.
* Workflow.XML toowasb:///tutorials/useoozie/workflow.xml kopyalayın.
* Coordinator.XML toowasb:///tutorials/useoozie/coordinator.xml kopyalayın.
* Kopya hello veri dosyası (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Sqoop verme verileri depolamak için bir Azure SQL veritabanı tablosu oluşturun. Merhaba tablo adı *log4jLogCount*.

**Hdınsight depolama anlama**

Hdınsight Azure Blob Depolama, veri depolaması için kullanır. wasb: / / Azure Blob depolamada hello Hadoop dağıtılmış dosya sistemi (HDFS) Microsoft uygulamasıdır. Daha fazla bilgi için bkz: [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].

Hdınsight kümesi sağladığınızda, Azure Blob Depolama hesabı ve bu hesaptan belirli bir kapsayıcıya tasarlanmış hello varsayılan dosya sistemi olarak gibi HDFS'de. Ayrıca toothis depolama hesabı, ek depolama hesapları hello aynı ekleyebileceğiniz Azure aboneliği ya da farklı Azure aboneliklerinden hello sağlama işlemi sırasında. Ek depolama hesapları ekleme hakkında yönergeler için bkz: [Hdınsight kümeleri hazırlama][hdinsight-provision]. Bu öğreticide kullanılan toosimplify hello Azure PowerShell Betiği, tüm dosyaları hello varsayılan dosya sistemi kapsayıcısında depolanır hello bulunan */öğreticileri/useoozie*. Varsayılan olarak, bu kapsayıcı hello aynı hello Hdınsight küme adı vardır.
Merhaba sözdizimi aşağıdaki gibidir:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Yalnızca hello *wasb: / /* söz dizimi Hdınsight kümesi sürüm 3.0 desteklenir. Merhaba eski *asv: / /* söz dizimi Hdınsight 2.1 ve 1.6 kümeleri desteklenir, ancak Hdınsight 3.0 kümelerinde desteklenmez.
>
> Merhaba wasb: / / yolu olan bir sanal yol. Daha fazla bilgi için bkz: [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].

Merhaba varsayılan dosya sistemi kapsayıcısında depolanır bir dosya (workflow.xml örnek olarak kullanıyorum) URI'ler aşağıdaki hello birini kullanarak Hdınsight'ta erişilebilir:

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Tooaccess hello dosyanın hello depolama hesabından doğrudan istiyorsanız hello blob hello dosya adıdır:

    tutorials/useoozie/workflow.xml

**Hive iç ve dış tablolar anlama**

Hive iç ve dış tablolar hakkında tooknow gereken birkaç nokta vardır:

* Merhaba CREATE TABLE komutu bir iç tablosu olarak da bilinen yönetilen bir tablo oluşturur. Merhaba veri dosyası hello varsayılan kapsayıcısında bulunması gerekir.
* Merhaba CREATE TABLE komutu taşır hello veri toohello dosya / / ambarı/hive<TableName> hello varsayılan kapsayıcı klasöründe.
* Merhaba dış tablo oluşturma komut bir dış tablo oluşturur. Merhaba veri dosyası hello varsayılan kapsayıcı bulunabilir.
* Merhaba dış tablo oluşturma komut hello veri dosyası taşımaz.
* Merhaba dış tablo oluşturma komut hello konumu yan tümcesinde belirtilen hello klasörü altındaki tüm alt izin vermez. Neden hello öğretici hello sample.log dosyasının bir kopyasını yapar hello nedeni budur.

Daha fazla bilgi için bkz: [Hdınsight: Hive iç ve dış tablolar giriş][cindygross-hive-tables].

**tooprepare başlangıç Öğreticisi**

1. Açık hello Windows PowerShell ISE (Merhaba ekranında Windows 8 Başlat, yazın **PowerShell_ISE**ve ardından **Windows PowerShell ISE**. Daha fazla bilgi için bkz: [Başlat Windows PowerShell Windows 8 ve Windows][powershell-start]).
2. Merhaba alt bölmede komutu tooconnect tooyour Azure aboneliği aşağıdaki hello çalıştırın:

    ```powershell
    Add-AzureAccount
    ```

    Azure hesabı kimlik bilgileriniz istendiğinde tooenter olacaktır. Bu yöntem bir abonelik bağlantısı ekleme zaman aşımına uğradı ve 12 saat sonra toorun hello cmdlet'ini yeniden sahip olur.

   > [!NOTE]
   > Birden çok Azure aboneliğiniz varsa ve hello varsayılan abonelik hello toouse istediğiniz değil, hello kullan <strong>Select-AzureSubscription</strong> cmdlet tooselect bir abonelik.

3. Merhaba betik bölmesine komut dosyası izleyen hello kopyalayın ve ardından hello ilk altı değişkenleri ayarlayın:

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    Merhaba hello değişkenleri daha fazla açıklamaları için bkz [Önkoşullar](#prerequisites) Bu öğretici bölümünde.

4. Toohello betik hello betik bölmesinde aşağıdaki hello ekleyin:

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. Tıklatın **komut dosyasını Çalıştır** veya basın **F5** toorun hello komut dosyası. Merhaba çıktı şuna benzeyecektir:

    ![Eğitmen hazırlık çıktı][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Merhaba Oozie projesi çalıştırma
Azure PowerShell cmdlet'lerin Oozie işleri tanımlamak için şu anda sağlamaz. Merhaba kullanabilirsiniz **Invoke-RestMethod** cmdlet tooinvoke Oozie web hizmetleri. bir HTTP REST JSON API Hello Oozie web hizmetleri API'si var. Merhaba Oozie web hizmetleri API'si hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (için Hdınsight kümesi sürüm 3.0) veya [Apache Oozie 3.3.2 belgelerine] [ apache-oozie-332] (için Hdınsight kümesi sürüm 2.1).

**toosubmit Oozie işi**

1. Açık hello Windows PowerShell ISE (Windows 8 Başlat ekranında, yazın **PowerShell_ISE**ve ardından **Windows PowerShell ISE**. Daha fazla bilgi için bkz: [Başlat Windows PowerShell Windows 8 ve Windows][powershell-start]).
2. Kopya hello aşağıdaki betiği hello betik bölmesine ve ardından kümesi hello ilk on dört değişkenleri (ancak, atla **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    Merhaba hello değişkenleri daha fazla açıklamaları için bkz [Önkoşullar](#prerequisites) Bu öğretici bölümünde.

    $coordstart ve $coordend hello iş akışı başlangıç ve bitiş saati ' dir. toofind hello UTC/GMT zaman aşımına uğrar aratıp "utc saat" araması yapın. Merhaba $coordFrequency toorun hello iş akışının istediğiniz sıklıkta dakikadır.
3. Toohello komut dosyası izleyen hello ekleyin. Bu bölümü hello Oozie yükünü tanımlar:

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > Merhaba kıyasla önemli fark toohello iş akışı gönderme yükü dosyası hello değişkenidir **oozie.coord.application.path**. İş akışının gönderdiğinizde, kullandığınız **oozie.wf.application.path** yerine.

4. Toohello komut dosyası izleyen hello ekleyin. Bu bölümü hello Oozie web hizmetinin durumunu denetler:

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Toohello komut dosyası izleyen hello ekleyin. Bu bölümü Oozie işi oluşturur:

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > İş akışının gönderdiğinizde hello işi oluşturulduktan sonra başka bir web hizmeti çağrısı toostart hello işi olmanız gerekir. Bu durumda, hello Düzenleyicisi işi zaman tarafından tetiklenir. Merhaba iş otomatik olarak başlatılacak.

6. Toohello komut dosyası izleyen hello ekleyin. Bu bölümü hello Oozie iş durumunu denetler:

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (İsteğe bağlı) Toohello komut dosyası izleyen hello ekleyin.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Toohello komut dosyası izleyen hello ekleyin:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Toorun hello ek işlevler istiyorsanız hello # işareti kaldırın.
9. Hdınsight kümesi sürüm 2.1 ise "https://$clusterName.azurehdinsight.net:443/oozie/v2/" "https://$clusterName.azurehdinsight.net:443/oozie/v1/" ile değiştirin. Hdınsight kümesi sürüm 2.1 değil destekler 2 hello web hizmetlerini desteklemiyor.
10. Tıklatın **komut dosyasını Çalıştır** veya basın **F5** toorun hello komut dosyası. Merhaba çıktı şuna benzeyecektir:

     ![İş akışı çıkış öğreticisini çalıştırma][img-runworkflow-output]
11. SQL veritabanı toosee dışarı hello veri tooyour bağlayın.

**toocheck hello iş hatası günlüğü**

tootroubleshoot bir iş akışı, hello Oozie günlük dosyası hello küme headnode C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log bulunabilir. RDP hakkında daha fazla bilgi için bkz: [kullanarak yönetme Hdınsight kümelerini hello Azure portal][hdinsight-admin-portal].

**toorerun başlangıç Öğreticisi**

toorerun hello iş akışı, hello aşağıdaki görevleri gerçekleştirmeniz gerekir:

* Merhaba Hive betiği çıktı dosyasını silin.
* Merhaba log4jLogsCount tablosunda Hello veri silin.

Kullanabileceğiniz örnek Windows PowerShell betiğini şöyledir:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl öğrenilen toodefine Oozie iş akışı ve Oozie Düzenleyicisi ve nasıl toorun Oozie Düzenleyicisi iş Azure PowerShell kullanarak. toolearn daha makaleler hello bakın:

* [Hdınsight kullanmaya başlama][hdinsight-get-started]
* [Hdınsight ile Azure Blob storage kullanma][hdinsight-storage]
* [Hdınsight Azure PowerShell kullanarak yönetme][hdinsight-admin-powershell]
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
