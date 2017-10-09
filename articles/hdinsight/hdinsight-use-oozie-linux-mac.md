---
title: "Linux tabanlı Hdınsight Hadoop Oozie akışlarında aaaUse | Microsoft Docs"
description: "Linux tabanlı Hdınsight'ta Hadoop Oozie kullanın. Bilgi nasıl toodefine bir Oozie iş akışı ve Oozie işi gönderin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Oozie Hadoop toodefine ile kullanın ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırma

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Bilgi nasıl toouse hdınsight'ta Hadoop ile Apache Oozie. Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir. Oozie hello Hadoop yığını ile tümleştirilir ve işleri aşağıdaki hello destekler:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie de Java programları veya kabuk betikleri gibi belirli tooa sistem kullanılan tooschedule işler olabilir

> [!NOTE]
> Hdınsight iş akışlarıyla tanımlamak için başka bir Azure Data Factory seçenektir. Azure Data Factory hakkında daha fazla toolearn bkz [kullanım Pig ve Hive Data Factory ile][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.

## <a name="prerequisites"></a>Ön koşullar

* **Hdınsight kümesi**: bkz [Linux'ta Hdınsight ile çalışmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Örnek iş akışı

Bu belgede kullanılan hello iş akışı iki eylemleri içerir. Hive, Sqoop, MapReduce veya başka bir işlemin çalıştırma gibi görevler için tanımları eylemler şunlardır:

![İş akışı diyagramı][img-workflow-diagram]

1. Bir Hive eylem HiveQL betiğini tooextract kayıtları hello çalıştırır **hivesampletable** Hdınsight ile dahil. Her veri satırının belirli bir mobil CİHAZDAN ziyaret açıklar. Merhaba kayıt biçimi metin aşağıdaki benzer toohello görünür:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Bu belgede kullanılan Hive betiğini Hello hello toplam ziyaretleriniz (örneğin, Android veya iPhone) her platform için sayar ve hello sayıları tooa yeni Hive tablosu depolar.

    Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].

2. Sqoop eylemin hello yeni Hive tablosu tooa tabloda bir Azure SQL veritabanı Merhaba içeriğine dışa aktarır. Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hadoop Sqoop][hdinsight-use-sqoop].

> [!NOTE]
> Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [hello Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Merhaba çalışma dizini oluşturulamadı

Oozie iş toobe hello aynı depolanan için gereken kaynakları bekliyor dizin. Bu örnekte **wasb: / / / öğreticileri/useoozie**. Komut toocreate aşağıdaki hello bu dizini ve bu iş akışı tarafından oluşturulan hello yeni Hive tablosu tutan hello veri dizini kullanın:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Merhaba `-p` parametresi hello yolu toobe oluşturulan tüm dizinleri neden olur. Merhaba **veri** dizindir hello tarafından kullanılan kullanılan toohold verileri **useooziewf.hql** komut dosyası.

Ayrıca Oozie, kullanıcı hesabınızın Hive ve Sqoop işleri çalıştırırken bürünebileceğini sağlar komutu aşağıdaki hello çalıştırın. Değiştir **kullanıcıadı** oturum açma adınız ile:

```
sudo adduser USERNAME users
```

> [!NOTE]
> Hataları yoksayma hello kullanıcı zaten hello üyesi olan `users` grubu.

## <a name="add-a-database-driver"></a>Bir veritabanı sürücüsü Ekle

Bu iş akışı Sqoop tooexport veri tooSQL veritabanı kullandığından, tootalk tooSQL veritabanının bir kopyasını hello JDBC sürücüsü kullanılan sağlamanız gerekir. Kullanım hello komut toocopy, toohello çalışma dizini:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

İş akışınızı bir MapReduce uygulaması içeren jar gibi diğer kaynaklar kullandıysanız, bu kaynakları da tooadd gerekir.

## <a name="define-hello-hive-query"></a>Merhaba Hive sorgusunu tanımlama

Aşağıdaki adımları toocreate bir Oozie iş akışında bu belgenin sonraki bölümlerinde kullanılan bir sorguyu tanımlayan bir HiveQL betiğini hello kullanın.

1. SSH kullanarak toohello kümesine bağlanın. Merhaba aşağıdaki komutu hello kullanarak bir örnektir `ssh` komutu. Değiştir __kullanıcıadı__ hello SSH kullanıcıyla hello küme. Değiştir __CLUSTERNAME__ hello Hdınsight kümesi hello adı.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH bağlantısı Hello komutu toocreate bir dosya aşağıdaki hello kullanın:

    ```
    nano useooziewf.hql
    ```

3. Merhaba nano düzenleyici açılır olduktan sonra sorgu hello dosyasının Merhaba içeriğine aşağıdaki hello kullanın:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Merhaba komut dosyasında kullanılan iki değişkenleri şunlardır:

    * **${hiveTableName}**: hello tablo toobe oluşturulan hello adını içerir

    * **${hiveDataFolder}**: hello tablo için hello konumu toostore hello veri dosyalarını içerir

    Merhaba iş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu değerleri toothis HiveQL betiğini çalışma zamanında geçirir.

4. tooexit hello Düzenleyici, Ctrl-X tuşlarına basın. İstendiğinde, seçin **Y** toosave hello dosyasını yeniden kullanın **Enter** toouse hello **useooziewf.hql** dosya adı.

5. Kullanım hello aşağıdaki komutları toocopy **useooziewf.hql** çok**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Bu komutlar hello depolamak **useooziewf.hql** hello küme için hello HDFS uyumlu depolama dosyası.

## <a name="define-hello-workflow"></a>Merhaba iş akışı tanımlama

Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır. Aşağıdaki adımları toodefine hello iş akışı hello kullan:

1. Deyimi toocreate aşağıdaki hello kullanın ve yeni dosyasını düzenleyin:

    ```
    nano workflow.xml
    ```

2. Bir kez hello nano Düzenleyici açıldığında, XML hello dosya içeriğini aşağıdaki hello girin:

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
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
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

    Merhaba iş akışında tanımlanan iki eylem vardır:

   * **RunHiveScript**: Bu eylem hello başlangıç eylemdir ve çalışan hello **useooziewf.hql** Hive betiği

   * **RunSqoopExport**: Bu eylem hello Hive betiği tooSQL oluşturulmuş hello veri aktarır Sqoop kullanarak veritabanı. Bu eylem yalnızca hello çalıştırır **RunHiveScript** eylem başarılı olur.

     Merhaba iş akışı sahip birden çok girişi gibi `${jobTracker}`. Bu girişler hello iş tanımında kullandığınız değerler değiştirilir. Merhaba iş tanımı, bu belgenin sonraki bölümlerinde oluşturulur.

     Ayrıca Not hello `<archive>sqljdbc4.jar</arcive>` hello Sqoop bölüm girişi. Bu eylem çalıştırıldığında bu girişi Oozie toomake Sqoop için kullanılabilir bu arşiv bildirir.

3. CTRL-X, daha sonra kullanmak **Y** ve **Enter** toosave hello dosya.

4. Kullanım hello şu komutu toocopy hello **workflow.xml** çok dosya**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Merhaba veritabanı oluşturma

toocreate bir Azure SQL veritabanı izleyin hello hello adımlarda [bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md) belge. Merhaba veritabanı oluştururken `oozietest` hello veritabanı adı. Ayrıca hello hello veritabanı sunucusunun adını not edin.

### <a name="create-hello-table"></a>Merhaba tablosu oluşturma

> [!NOTE]
> Birçok yolu tooconnect tooSQL veritabanı toocreate bir tablo yok. Aşağıdaki adımları kullan hello [ücretsiz](http://www.freetds.org/) hello Hdınsight kümesine ait.


1. Komut tooinstall ücretsiz hello Hdınsight kümesinde aşağıdaki hello kullan:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Ücretsiz yüklendikten sonra daha önce oluşturulan komutu tooconnect toohello SQL veritabanı sunucusu aşağıdaki hello kullan:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Metin aşağıdaki çıktı benzer toohello alırsınız:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. Merhaba, `1>` isteminde, aşağıdaki satırları hello girin:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Ne zaman hello `GO` deyimi girilir, hello önceki deyimleri değerlendirilir. Bu ifadeler adlı bir tablo oluşturmak **mobiledata** hello iş akışı tarafından kullanılır.

    Tablo hello tooverify aşağıdaki kullanım hello oluşturuldu:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Metin aşağıdaki çıktı benzer toohello bakın:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Girin `exit` hello adresindeki `1>` sor tooexit hello tsql yardımcı programı.

## <a name="create-hello-job-definition"></a>Merhaba iş tanımı oluştur

Merhaba iş tanımı burada toofind hello workflow.xml açıklar. Ayrıca nerede tanımlar toofind (örneğin, useooziewf.hql.) hello iş akışı tarafından kullanılan diğer dosyaları Özellikler hello iş akışı içinde kullanılan ve dosyalar ilişkili ayrıca hello değerleri tanımlar.

1. Kullanım hello aşağıdaki tooget hello tam adresini hello varsayılan depolama komutu. Bu adres hello yapılandırma dosyasında birazdan kullanılır:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Bu komut, XML aşağıdaki bilgileri benzer toohello döndürür:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Merhaba Hdınsight küme hello varsayılan depolama alanı olarak Azure Storage kullanıyorsa, hello `<value>` öğenin içeriği ile başlar `wasb://`. Azure Data Lake Store yerine kullanılırsa, ile başlayan `adl://`.

    Merhaba Hello içeriğini kaydetme `<value>` şekliyle öğe hello sonraki adımda kullanılır.

2. Komut tooget hello küme headnode FQDN'si aşağıdaki hello kullanın. Bu bilgiler hello hello küme için Jobtracker'a adresi için kullanılır:

    ```
    hostname -f
    ```

    Bu metin aşağıdaki bilgileri benzer toohello döndürür:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Merhaba tam adresi toouse hello Jobtracker'a için olacak şekilde hello Jobtracker'a hello için kullanılan bağlantı noktası 8050, olan `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Toocreate hello Oozie iş tanımı yapılandırması aşağıdaki hello kullan:

    ```
    nano job.xml
    ```

4. Merhaba nano düzenleyici açılır sonra XML hello hello dosyasının içeriğini aşağıdaki hello kullanın:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
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
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * Tüm örneklerinin yerine  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  aldığınız önceki sürümleri için varsayılan depolama hello değerine sahip.

     > [!WARNING]
     > Merhaba yol ise bir `wasb` yolu hello tam yolunu kullanmanız gerekir. Toojust kısaltın değil `wasb:///`.

   * Değiştir **JOBTRACKERADDRESS** hello daha önce aldığınız Jobtracker'a/ResourceManager adresine sahip.
   * Değiştir **adınız** hello Hdınsight kümesi için oturum açma adınızı ile.
   * Değiştir **serverName**, **adminLogin**, ve **Admınpassword** Azure SQL veritabanınıza ilişkin hello bilgiler.

     Bu dosyadaki hello bilgilerin çoğunu olduğu (örneğin, ${iş}.) hello workflow.xml veya ooziewf.hql dosyalarında kullanılan kullanılan toopopulate hello değerleri

     > [!NOTE]
     > Hello **oozie.wf.application.path** girdi tanımlar where hello iş akışı içeren toofind hello workflow.xml dosyasını bu iş tarafından çalıştı.

5. CTRL-X, daha sonra kullanmak **Y** ve **Enter** toosave hello dosya.

## <a name="submit-and-manage-hello-job"></a>Gönderme ve hello işi yönetme

Merhaba aşağıdaki adımları hello Oozie komutu toosubmit kullanın ve Oozie iş akışları hello kümede yönetin. Merhaba Oozie komutu olan kullanıcı dostu bir arabirim hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Merhaba Oozie komutunu kullanırken, hello Hdınsight headnode hello FQDN kullanmanız gerekir. Bu FQDN yalnızca hello kümeden erişilebilir olduğunu veya hello küme hello üzerindeki diğer makinelerden bir Azure sanal ağda ise aynı ağ.


1. Tooobtain hello URL toohello Oozie hizmeti aşağıdaki hello kullan:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Bu bilgi benzer toohello XML aşağıdaki döndürür:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Merhaba `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` hello URL toouse hello Oozie komutu sahip bölümüdür.

2. Tootype aktarıp toocreate bir ortam değişkeni hello URL'sini aşağıdaki kullanım hello her komut için:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Merhaba URL hello biri daha önce aldığınız değiştirin.
3. Toosubmit hello işi aşağıdaki hello kullan:

    ```
    oozie job -config job.xml -submit
    ```

    Bu komut hello iş bilgilerini yükler **job.xml** ve tooOozie, ancak bunu çalışmıyor mu gönderir.

    Merhaba komutu tamamlandığında hello işin hello kimliği döndürmelidir. Örneğin, `0000005-150622124850154-oozie-oozi-W`. Kullanılan toomanage hello iş kimliğidir.

4. Komutu aşağıdaki hello kullanarak hello işi Hello durumunu görüntüleyin:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Değiştir `<JOBID>` ile Merhaba hello önceki adımda döndürülen kimliği.

    Bu metin aşağıdaki bilgileri benzer toohello döndürür:

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    Bu iş durumuna sahip `PREP`. Bu durum, bu hello iş oluşturuldu, ancak henüz başlatılmamış gösterir.

5. Komut toostart hello işi aşağıdaki hello kullan:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Değiştir `<JOBID>` hello ile döndürülen kimliği daha önce.

    Bu komutun ardından hello durumunu denetlemek, çalışır durumda olduğundan ve bilgi hello işindeki hello eylemler için döndürülür.

6. Merhaba görev başarıyla tamamlandıktan sonra hello veri oluşturuldu ve toohello SQL veritabanı tablosu hello aşağıdaki komutları kullanarak dışa aktarılan doğrulayabilirsiniz:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    Merhaba, `1>` isteminde, sorgu aşağıdaki hello girin:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    döndürülen hello bilgi metnini izleyen benzer toohello şöyledir:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Merhaba Oozie komut hakkında daha fazla bilgi için bkz: [Oozie komut satırı aracı](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>Oozie REST API'si

Merhaba Oozie REST API toobuild verir Oozie ile iş kendi araçları. Merhaba, Hdınsight hello Oozie REST API kullanımı hakkında belirli bilgiler şunlardır:

* **URI**: REST API erişilebilir dış hello kümeden hello`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Kimlik doğrulama**: toohello API hello küme HTTP hesabı (Yönetici) ve parola kullanarak kimlik doğrulaması. Örneğin:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Merhaba Oozie REST API kullanma hakkında daha fazla bilgi için bkz: [Oozie Web Hizmetleri API'si](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Oozie Web kullanıcı Arabirimi

Merhaba Oozie Web kullanıcı arabirimini hello Oozie işlerin durumunu web tabanlı bir görünüme hello kümede sağlar. Merhaba web kullanıcı Arabirimi aşağıdaki bilgilerle tooview hello sağlar:

* İş durumu
* İş tanımı
* Yapılandırma
* Merhaba işteki hello eylemlerin bir grafik
* Merhaba işi için kayıtlar

Ayrıca bir işi içinde eylemler ayrıntılarını görüntüleyebilirsiniz.

tooaccess Oozie Web kullanıcı arabirimini Merhaba, hello aşağıdaki adımları kullanın:

1. SSH tüneli toohello Hdınsight kümesi oluşturun. Bilgi için bkz: Merhaba [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.

2. Bir tünel oluşturulduktan sonra hello Ambari web kullanıcı Arabirimi, web tarayıcınızda açın. Merhaba URI hello Ambari site için olan **https://CLUSTERNAME.azurehdinsight.net**. Değiştir **CLUSTERNAME** Linux tabanlı Hdınsight kümenize hello adı.

3. Yan hello sayfasının sol hello seçin **Oozie**, ardından **hızlı bağlantılar**ve son olarak **Oozie Web kullanıcı arabirimini**.

    ![Merhaba menü görüntüsü](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Merhaba Oozie Web kullanıcı arabirimini Varsayılanları toodisplaying iş akışı işleri çalıştırma. tüm iş akışı işleri toosee seçin **tüm işleri**.

    ![Görüntülenen tüm işleri](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Bir iş tooview hello işi hakkında daha fazla bilgi seçin.

    ![İş bilgileri](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Merhaba iş bilgileri sekmesinden temel iş bilgilerini ve hello ayrı Eylemler hello işindeki görebilirsiniz. Merhaba sekmelerini kullanarak görüntüleyebileceğiniz hello üstünde iş tanımı, iş yapılandırması, erişim hello iş günlüğü hello veya yönlendirilmiş Çevrimsiz grafik (DAG) hello işin görüntüleyin.

   * **İş günlüğü**: Select hello **GetLogs** tooget hello işi için tüm günlükleri düğmesine veya hello kullan **girin arama filtresi** alan toofilter günlükleri

       ![İş günlüğü](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: Merhaba DAG olan hello akışı gerçekleştirilecek hello veri yolları grafik bir genel bakış

       ![İş DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Hello hello eylemlerden birini seçerek **iş bilgileri** sekmesini hello eylemi için bilgileri getirir. Örneğin, hello seçin **RunHiveScript** eylem.

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Bir bağlantı toohello gibi hello eylem ayrıntılarını görebilirsiniz **Konsolu URL'si**. Bu bağlantıyı hello işi için kullanılan tooview Jobtracker'a bilgileri olabilir.

## <a name="scheduling-jobs"></a>İşlerini zamanlama

Merhaba Düzenleyicisi toospecify işleri için bir başlangıç, bitiş ve geçişi sıklık sağlar. Merhaba iş akışı, aşağıdaki adımları kullanın hello için bir zamanlama toodefine:

1. Toocreate adlı bir dosya aşağıdaki kullanım hello **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    XML hello hello dosyasının içeriğini aşağıdaki hello kullan:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > Merhaba `${...}` değişkenleri, çalışma zamanında hello iş tanımında değerlere göre değiştirilir. Merhaba değişkenleri şunlardır:
    >
    > * `${coordFrequency}`: Çalışan hello iş örneklerini arasındaki süre.
    > ** `${coordStart}`: hello iş başlangıç zamanı.
    > * `${coordEnd}`: hello iş bitiş saati.
    > * `${coordTimezone}`: Sabit bir saat diliminde (genellikle UTC ile gösterilir) hiçbir gün ışığından yararlanma saatine sahip olan düzenleyici işleri. Bu saat dilimi hello "Oozie işleme saat dilimi." olarak adlandırılır
    > * `${wfPath}`: yolu toohello workflow.xml hello.

2. toosave hello dosya, Ctrl-X, kullanmak **Y**, ve **Enter**.

3. Bu iş için komut toocopy hello dosya toohello çalışma dizini aşağıdaki hello kullan:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Kullanım hello toomodify hello aşağıdaki **job.xml** dosyası:

    ```
    nano job.xml
    ```

    Aşağıdaki değişiklikler hello olun:

   * Merhaba iş akışı, değişiklik yerine tooinstruct oozie toorun hello Düzenleyici dosyasında `<name>oozie.wf.application.path</name>` çok`<name>oozie.coord.application.path</name>`.

   * tooset hello `workflowPath` hello Düzenleyicisi tarafından kullanılan değişken XML aşağıdaki hello ekleyin:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Hello yerine `wasb://mycontainer@mystorageaccount.blob.core.windows` diğer giriş hello job.xml dosyası kullanılan hello değeri olan metin.

   * toodefine hello başlangıç, bitiş ve sıklığı hello Düzenleyicisi için XML aşağıdaki hello ekleyin:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       Merhaba başlangıç saati too12 bu değerleri ayarlayın: 00 PM 10 May 2017 üzerinde hello bitiş saati tooMay 12, 2017. Bu işi her gün için başlangıç aralığı. Merhaba sıklığıdır dakika içinde bu nedenle 1440 dakika 24 saat x 60 dakika =. Son olarak, hello saat dilimi tooUTC ayarlanır.

5. CTRL-X, daha sonra kullanmak **Y** ve **Enter** toosave hello dosya.

6. toorun hello iş, komutu aşağıdaki kullanım hello:

    ```
    oozie job -config job.xml -run
    ```

    Bu komut gönderir ve hello işini başlatır.

7. Merhaba Oozie Web kullanıcı arabirimini ziyaret ederek seçin hello **Düzenleyicisi işleri** sekmesine, görüntü aşağıdaki bilgileri benzer toohello bakın:

    ![Düzenleyici işler sekmesi](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Merhaba **sonraki Materialization** giriş İş çalıştırmaları hello bir sonraki başlatılışında hello içerir.

8. Benzer toohello hello proje girişi hello web kullanıcı arabirimini seçerek önceki iş akışı işini hello işinde bilgileri görüntüler:

    ![Düzenleyici iş bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Bu görüntü yalnızca başarılı çalıştırır hello zamanlanmış iş akışı içinde bireysel Eylemler hello işin gösterir. Merhaba birini seçin, toosee **eylem** girişleri.

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Sorun giderme

Merhaba Oozie UI tooview Oozie günlükleri sağlar. Ayrıca, MapReduce görevlerin hello iş akışı tarafından başlatılan bağlantıları tooJobTracker günlükleri içerir. sorun giderme için hello düzeni olmalıdır:

1. Oozie Web kullanıcı arabirimini hello işi görüntüle.

2. Bir hata veya belirli bir eylemi için hatası ise, select hello varsa, eylem toosee hello **hata iletisi** alan hello hatada daha fazla bilgi sağlar.

3. Varsa, hello eylem tooview hello URL'den hello eylem için daha fazla ayrıntı (örneğin, Jobtracker'a günlükleri) kullanın.

Merhaba karşılaşabileceğiniz, belirli hataları verilmiştir ve nasıl tooresolve bunları.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: küme başlatılamıyor

**Belirtiler**: İş durumu değiştiğinde çok hello**ASKIYA**. Merhaba işe yönelik ayrıntıları göster hello RunHiveScript durumu olarak **START_MANUAL**. Merhaba eylem seçildikten hello aşağıdaki hata iletisini görüntüler:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Neden**: Merhaba hello kullanılan WASB adresleri **job.xml** dosya hello depolama kapsayıcısı veya depolama hesabı adı içermiyor. Merhaba WASB adres biçimini olmalıdır `wasb://containername@storageaccountname.blob.core.windows.net`.

**Çözümleme**: hello iş tarafından kullanılan hello WASB adreslerini değiştirin.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Tooimpersonate Oozie izin verilmiyor &lt;kullanıcı >

**Belirtiler**: İş durumu değiştiğinde çok hello**ASKIYA**. Merhaba işe yönelik ayrıntıları göster hello RunHiveScript durumu olarak **START_MANUAL**. Merhaba eylem seçmek aşağıdaki hata iletisini hello gösterir:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Neden**: Geçerli izin ayarlarını Oozie izin vermez tooimpersonate hello belirtilen kullanıcı hesabı.

**Çözümleme**: Oozie hello tooimpersonate kullanıcılar izin **kullanıcılar** grubu. Kullanım hello `groups USERNAME` kullanıcı hesabı hello toosee hello gruplarının bir üyesidir. Merhaba kullanıcı hello üyesi değilse **kullanıcılar** grup, komut tooadd hello kullanıcı toohello grubu aşağıdaki hello kullanın:

    sudo adduser USERNAME users

> [!NOTE]
> Merhaba kullanıcı toohello Grup eklenen Hdınsight algılamasından önce birkaç dakika sürebilir.

### <a name="launcher-error-sqoop"></a>Başlatıcı hata (Sqoop)

**Belirtiler**: İş durumu değiştiğinde çok hello**KILLED**. Merhaba işe yönelik ayrıntıları göster hello RunSqoopExport durumu olarak **hata**. Merhaba eylem seçmek aşağıdaki hata iletisini hello gösterir:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Neden**: Sqoop veritabanıdır oluşturulamıyor tooload hello veritabanı sürücüsü gerekli tooaccess hello.

**Çözümleme**: Sqoop, Oozie işten kullanırken, hello veritabanı sürücüsünü hello ile Merhaba iş tarafından kullanılan diğer kaynakları (örneğin, hello workflow.xml) içermelidir. Ayrıca hello hello veritabanı sürücüsünü içeren hello arşiv başvuru `<sqoop>...</sqoop>` hello workflow.xml bölümü.

Örneğin, bu belgedeki hello işi için aşağıdaki adımları hello kullanırsınız:

1. Merhaba sqljdbc4.1.jar dosyası toohello /tutorials/useoozie dizinine kopyalayın:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Yeni bir satıra yukarıdaki XML aşağıdaki hello workflow.xml tooadd hello değiştirme `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl öğrenilen toodefine Oozie iş akışı ve nasıl toorun Oozie işi. Hdınsight ile çalışma hakkında daha fazla toolearn makaleler hello bakın:

* [Hdınsight ile zamana dayalı Oozie düzenleyicisi kullanın][hdinsight-oozie-coordinator-time]
* [Hdınsight'ta Hadoop işleri için verileri karşıya yükleme][hdinsight-upload-data]
* [Hdınsight'ta Hadoop ile Sqoop kullanma][hdinsight-use-sqoop]
* [Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]
* [Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]
* [Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
