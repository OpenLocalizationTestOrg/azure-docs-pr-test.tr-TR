---
title: "Linux tabanlı Hdınsight'ta Hadoop Oozie iş akışlarını kullanın | Microsoft Docs"
description: "Linux tabanlı Hdınsight'ta Hadoop Oozie kullanın. Oozie iş akışı tanımlamak ve Oozie işi göndermek öğrenin."
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a>Oozie Hadoop ile tanımlamak ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırmak için kullanın.

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Hdınsight'ta Hadoop ile Apache Oozie kullanmayı öğrenin. Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir. Oozie Hadoop yığını ile tümleştirilir ve aşağıdaki işleri destekler:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie, Java programları veya kabuk betikleri gibi sisteme özel işleri planlamak için de kullanılabilir

> [!NOTE]
> Hdınsight iş akışlarıyla tanımlamak için başka bir Azure Data Factory seçenektir. Azure Data Factory hakkında daha fazla bilgi için bkz: [kullanım Pig ve Hive Data Factory ile][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.

## <a name="prerequisites"></a>Ön koşullar

* **Hdınsight kümesi**: bkz [Linux'ta Hdınsight ile çalışmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Örnek iş akışı

Bu belgede kullanılan iş akışı iki eylemleri içerir. Hive, Sqoop, MapReduce veya başka bir işlemin çalıştırma gibi görevler için tanımları eylemler şunlardır:

![İş akışı diyagramı][img-workflow-diagram]

1. Hive eylem kayıtları ayıklamak için HiveQL betiğini çalıştırır **hivesampletable** Hdınsight ile dahil. Her veri satırının belirli bir mobil CİHAZDAN ziyaret açıklar. Kayıt biçimi aşağıdakine benzer görünür:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Bu belgede kullanılan Hive betiğini (örneğin, Android veya iPhone) her platform için toplam ziyaret sayar ve yeni bir Hive tablosu için sayıları depolar.

    Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].

2. Sqoop eylem yeni Hive tablosu içeriğini bir Azure SQL veritabanındaki bir tablo dışa aktarır. Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hadoop Sqoop][hdinsight-use-sqoop].

> [!NOTE]
> Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler][hdinsight-versions].

## <a name="create-the-working-directory"></a>Çalışma dizini oluşturma

Oozie aynı dizinde depolanması bir iş için gereken kaynakları bekliyor. Bu örnekte **wasb: / / / öğreticileri/useoozie**. Bu dizin ve bu iş akışı tarafından oluşturulan yeni Hive tablosu tutan veri dizini oluşturmak için aşağıdaki komutu kullanın:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> `-p` Parametresi oluşturulacak yolunda tüm dizinleri neden olur. **Veri** dizini tarafından kullanılan verileri depolamak için kullanılan **useooziewf.hql** komut dosyası.

Ayrıca Oozie, kullanıcı hesabınızın Hive ve Sqoop işleri çalıştırırken bürünebileceğini sağlar aşağıdaki komutu çalıştırın. Değiştir **kullanıcıadı** oturum açma adınız ile:

```
sudo adduser USERNAME users
```

> [!NOTE]
> Kullanıcı zaten bir üyesidir hataları yoksayabilirsiniz `users` grubu.

## <a name="add-a-database-driver"></a>Bir veritabanı sürücüsü Ekle

Bu iş akışı SQL veritabanına veri vermek için Sqoop kullandığından, SQL veritabanı ile iletişim için kullanılan JDBC sürücüsü kopyasını sağlamanız gerekir. Çalışma dizini kopyalamak için aşağıdaki komutu kullanın:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

İş akışınızı bir MapReduce uygulaması içeren jar gibi diğer kaynaklar kullandıysanız, bu kaynakları de eklemeniz gerekir.

## <a name="define-the-hive-query"></a>Hive sorgusunu tanımlayın

Bu belgenin sonraki bölümlerinde bir Oozie akışında kullanılan bir sorguyu tanımlayan bir HiveQL betiği oluşturmak için aşağıdaki adımları kullanın.

1. SSH kullanarak kümeye bağlanın. Aşağıdaki komutu kullanarak, bir örnek verilmiştir `ssh` komutu. Değiştir __kullanıcıadı__ SSH kullanıcı kümesi için. Değiştir __CLUSTERNAME__ Hdınsight kümesi adı.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH bağlantısı, bir dosya oluşturmak için aşağıdaki komutu kullanın:

    ```
    nano useooziewf.hql
    ```

3. Nano Düzenleyici açar sonra dosyanın içeriğini aşağıdaki sorguyu kullanın:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Komut dosyasında kullanılan iki değişkenleri şunlardır:

    * **${hiveTableName}**: Oluşturulacak tablonun adını içerir

    * **${hiveDataFolder}**: Tablo için veri dosyalarının depolanacağı konumu içerir

    İş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu HiveQL betiğini bu değerleri, çalışma zamanında geçirir.

4. Düzenleyiciden çıkmak için Ctrl-X tuşlarına basın. İstendiğinde, seçin **Y** dosyayı kaydetmek için daha sonra kullanmak **Enter** kullanmak için **useooziewf.hql** dosya adı.

5. Kopyalamak için aşağıdaki komutları kullanın **useooziewf.hql** için **wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Bu komutlar depolamak **useooziewf.hql** HDFS uyumlu depolama biriminde bir dosya kümesi için.

## <a name="define-the-workflow"></a>İş akışı tanımlama

Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır. İş akışını tanımlamak için aşağıdaki adımları kullanın:

1. Oluşturun ve yeni bir dosya düzenlemek için şu deyimi kullanın:

    ```
    nano workflow.xml
    ```

2. Nano Düzenleyici açar sonra aşağıdaki XML dosya içeriklerini girin:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    İş akışında tanımlanan iki eylem vardır:

   * **RunHiveScript**: Bu eylem başlangıç eylemdir ve çalışan **useooziewf.hql** Hive betiği

   * **RunSqoopExport**: Bu eylem Sqoop kullanarak SQL veritabanına Hive komut dosyasından oluşturulan veri aktarır. Bu eylem yalnızca çalıştırır **RunHiveScript** eylem başarılı olur.

     İş akışı gibi birden çok girişi sahip `${jobTracker}`. Bu girişler iş tanımında kullandığınız değerler değiştirilir. İş tanımı, bu belgenin sonraki bölümlerinde oluşturulur.

     Ayrıca unutmayın `<archive>sqljdbc4.jar</arcive>` Sqoop bölümünde girişi. Bu giriş, bu eylem çalıştırıldığında bu arşiv Sqoop için kullanılabilmesi için Oozie bildirir.

3. CTRL-X, daha sonra kullanmak **Y** ve **Enter** dosyayı kaydetmek için.

4. Kopyalamak için aşağıdaki komutu kullanın **workflow.xml** dosya **/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a>Veritabanı oluşturma

Bir Azure SQL veritabanı oluşturmak için adımları [bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md) belge. Veritabanı oluştururken `oozietest` veritabanı adı. Ayrıca veritabanı sunucusunun adını not edin.

### <a name="create-the-table"></a>Tablo oluşturma

> [!NOTE]
> Bir tablo oluşturmak için SQL veritabanına bağlanmak için birçok yolu vardır. Aşağıdaki adımları kullanın [ücretsiz](http://www.freetds.org/) Hdınsight kümesine ait.


1. Ücretsiz Hdınsight kümesine yüklemek için aşağıdaki komutu kullanın:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Ücretsiz bir kez yüklenir, önceden oluşturduğunuz bir SQL veritabanı sunucusuna bağlanmak için aşağıdaki komutu kullanın:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Aşağıdakine benzer bir çıktı alırsınız:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. Konumundaki `1>` isteminde, aşağıdaki satırları girin:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Zaman `GO` deyimi girilir, önceki deyimleri değerlendirilir. Bu ifadeler adlı bir tablo oluşturmak **mobiledata** iş akışı tarafından kullanılır.

    Tablo oluşturulduğunu doğrulamak için aşağıdakileri kullanın:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Aşağıdakine benzer bir çıktı görürsünüz:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Girin `exit` adresindeki `1>` tsql yardımcı programı'ndan çıkmak komut istemi.

## <a name="create-the-job-definition"></a>İş tanımı oluştur

İş tanımı workflow.xml nerede bulacağını açıklar. Ayrıca (örneğin, useooziewf.hql.) iş akışı tarafından kullanılan diğer dosyaları nerede bulacağını açıklanır Özellikler iş akışı içinde kullanılan ve dosyalar ilişkili değerleri de tanımlar.

1. Varsayılan depolama tam adresini almak için aşağıdaki komutu kullanın. Bu adres yapılandırma dosyasında birazdan kullanılır:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Bu komut, bilgileri aşağıdaki XML benzer döndürür:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Hdınsight küme varsayılan depolama alanı olarak Azure Storage kullanıyorsa `<value>` öğenin içeriği ile başlar `wasb://`. Azure Data Lake Store yerine kullanılırsa, ile başlayan `adl://`.

    İçeriğini kaydetme `<value>` şekliyle öğe, sonraki adımlarda kullanılır.

2. Küme headnode FQDN'sini almak için aşağıdaki komutu kullanın. Bu bilgiler, küme için Jobtracker'a adresi için kullanılır:

    ```
    hostname -f
    ```

    Bu bilgiler aşağıdaki metni benzer döndürür:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Jobtracker'a için kullanılacak tam adresi 8050, Jobtracker'a için kullanılan bağlantı noktası olduğundan `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Oozie iş tanımı yapılandırması oluşturmak için aşağıdakileri kullanın:

    ```
    nano job.xml
    ```

4. Nano düzenleyici açılır olduktan sonra aşağıdaki XML dosyasının içeriği kullanın:

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

   * Tüm örneklerinin yerine  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  aldığınız önceki sürümleri için varsayılan depolama değerine sahip.

     > [!WARNING]
     > Yol ise bir `wasb` yolu, tam yolunu kullanmanız gerekir. Yalnızca kendisine kısaltın değil `wasb:///`.

   * Değiştir **JOBTRACKERADDRESS** daha önce aldığınız Jobtracker'a/ResourceManager adresine sahip.
   * Değiştir **adınız** Hdınsight kümesi için oturum açma adınızı ile.
   * Değiştir **serverName**, **adminLogin**, ve **Admınpassword** Azure SQL veritabanınıza ilişkin bilgiler.

     Bu dosyadaki bilgiler çoğunu (örneğin, ${iş}.) workflow.xml veya ooziewf.hql dosyalarında kullanılan değerleri doldurmak için kullanılır

     > [!NOTE]
     > **Oozie.wf.application.path** girdi tanımlar workflow.xml dosya nerede bulacağını bu iş tarafından çalıştırılan iş akışını içerir.

5. CTRL-X, daha sonra kullanmak **Y** ve **Enter** dosyayı kaydetmek için.

## <a name="submit-and-manage-the-job"></a>Gönderme ve iş yönetimi

Aşağıdaki adımlar Oozie komutunu göndermek ve küme Oozie iş akışlarında yönetmek için kullanın. Oozie kullanıcı dostu bir arabirim üzerinden komuttur [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Oozie komutunu kullanırken, FQDN için Hdınsight headnode kullanmanız gerekir. Bu FQDN yalnızca kümeden erişilebilir veya küme aynı ağdaki diğer makinelerden bir Azure sanal ağda ise.


1. Oozie hizmeti URL'sini almak için aşağıdakileri kullanın:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Bu bilgiler aşağıdaki XML benzer döndürür:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` Bölümüdür Oozie komutu ile kullanılacak URL.

2. Her komut için yazmak zorunda kalmamak için URL için bir ortam değişkeni oluşturmak için aşağıdakileri kullanın:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    URL, daha önce aldığınız adla değiştirin.
3. İşi göndermek için aşağıdakileri kullanın:

    ```
    oozie job -config job.xml -submit
    ```

    Bu komut iş bilgilerini yükler **job.xml** ve Oozie için gönderir, ancak değil çalıştırın.

    Komut tamamlandığında, iş kimliği döndürmelidir. Örneğin, `0000005-150622124850154-oozie-oozi-W`. Bu kimliği iş yönetmek için kullanılır.

4. Aşağıdaki komutu kullanarak iş durumunu görüntüleyin:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Değiştir `<JOBID>` önceki adımda döndürülen Kimliğine sahip.

    Bu bilgiler aşağıdaki metni benzer döndürür:

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

    Bu iş durumuna sahip `PREP`. Bu durum, iş oluşturuldu, ancak başlatılmamış olduğunu gösterir.

5. İşlemi başlatmak için aşağıdaki komutu kullanın:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Değiştir `<JOBID>` döndürülen Kimliğine sahip.

    Bu komutun sonraki durumunu denetlemek, çalışır durumda olduğundan ve iş içindeki eylemler için bilgi döndürülür.

6. Görev başarıyla tamamlandıktan sonra veri oluşturulur ve aşağıdaki komutları kullanarak SQL veritabanı tablosuna dışa aktarılan olduğunu doğrulayabilirsiniz:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    Konumundaki `1>` isteminde, aşağıdaki sorguyu girin:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    Döndürülen bilgi aşağıdakine benzer:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Oozie komutu hakkında daha fazla bilgi için bkz: [Oozie komut satırı aracı](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>Oozie REST API'si

Oozie REST API ile Oozie iş kendi araçları oluşturmanıza olanak sağlar. Hdınsight Oozie REST API kullanımı hakkında belirli bilgiler şunlardır:

* **URI**: REST API erişilebilir gelen küme dışındaki`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Kimlik doğrulama**: küme HTTP hesabı (Yönetici) ve parolayı kullanarak API kimlik doğrulaması. Örneğin:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Oozie REST API kullanarak daha fazla bilgi için bkz: [Oozie Web Hizmetleri API'si](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Oozie Web kullanıcı Arabirimi

Oozie Web kullanıcı arabirimini Oozie işlerin durumunu web tabanlı bir görünüme kümede sağlar. Web kullanıcı Arabirimi, aşağıdaki bilgileri görüntülemenizi sağlar:

* İş durumu
* İş tanımı
* Yapılandırma
* İşte eylemlerin bir grafik
* İşi için kayıtlar

Ayrıca bir işi içinde eylemler ayrıntılarını görüntüleyebilirsiniz.

Oozie Web kullanıcı arabirimini erişmek için aşağıdaki adımları kullanın:

1. Bir Hdınsight kümesine SSH tüneli oluşturma. Bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.

2. Bir tünel oluşturulduktan sonra Ambari web kullanıcı Arabirimi, web tarayıcınızda açın. Ambari site için bir URI **https://CLUSTERNAME.azurehdinsight.net**. Değiştir **CLUSTERNAME** Linux tabanlı Hdınsight kümenizin adıyla.

3. Sayfanın sol taraftan seçin **Oozie**, ardından **hızlı bağlantılar**ve son olarak **Oozie Web kullanıcı arabirimini**.

    ![görüntüsü menüler](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Oozie Web kullanıcı Arabirimi iş akışı işleri çalıştırma görüntüleme için varsayılan olarak ayarlanır. Tüm iş akışı işleri görmek için seçin **tüm işleri**.

    ![Görüntülenen tüm işleri](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. İş hakkında daha fazla bilgi görüntülemek için bir iş seçin.

    ![İş bilgileri](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. İş bilgileri sekmesinden temel iş bilgileri ve iş içindeki ayrı Eylemler görebilirsiniz. En üstte sekmeleri kullanarak iş tanımı, iş yapılandırması, erişim iş günlüğü görüntülemek veya yönlendirilmiş Çevrimsiz grafik (DAG) işin görüntüleyin.

   * **İş günlüğü**: seçin **GetLogs** iş için tüm günlükleri almak için düğmesini veya kullanmak **girin arama filtresi** günlükleri filtrelemek için alan

       ![İş günlüğü](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: DAG olan akışı gerçekleştirilecek veri yolları grafik bir genel bakış

       ![İş DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Eylemlerden birini seçerek **iş bilgileri** sekme eylemi için bilgileri getirir. Örneğin, seçin **RunHiveScript** eylem.

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Bir bağlantı gibi eylemin ayrıntılarını görebilirsiniz **Konsolu URL'si**. Bu bağlantı, iş Jobtracker'a bilgilerini görüntülemek için kullanılabilir.

## <a name="scheduling-jobs"></a>İşlerini zamanlama

Düzenleyici, başlangıç, bitiş ve işleri için oluşum sıklığını belirtmenizi sağlar. İş akışı için bir zamanlama tanımlamak için aşağıdaki adımları kullanın:

1. Adlı bir dosya oluşturmak için aşağıdakileri kullanın **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Aşağıdaki XML dosyasının içeriği kullanın:

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
    > `${...}` Değişkenleri, çalışma zamanında iş tanımında değerlere göre değiştirilir. Değişkenleri şunlardır:
    >
    > * `${coordFrequency}`: Çalışan iş örneklerini arasındaki süre.
    > ** `${coordStart}`: İş başlangıç zamanı.
    > * `${coordEnd}`: İş bitiş saati.
    > * `${coordTimezone}`: Sabit bir saat diliminde (genellikle UTC ile gösterilir) hiçbir gün ışığından yararlanma saatine sahip olan düzenleyici işleri. Bu saat dilimi "Oozie işleme saat dilimi." olarak adlandırılır
    > * `${wfPath}`: Workflow.xml yolu.

2. Dosyayı kaydetmek için Ctrl-X, kullanmak **Y**, ve **Enter**.

3. Bu proje için çalışma dizini dosyasını kopyalamak için aşağıdaki komutu kullanın:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Değiştirmek için aşağıdakileri kullanın **job.xml** dosyası:

    ```
    nano job.xml
    ```

    Aşağıdaki değişiklikleri yapın:

   * İş akışı yerine Düzenleyicisi dosyasını çalıştırmak için oozie istemek üzere değiştirme `<name>oozie.wf.application.path</name>` için `<name>oozie.coord.application.path</name>`.

   * Ayarlamak için `workflowPath` aşağıdaki XML ekleme Düzenleyicisi tarafından kullanılan değişkeni:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Değiştir `wasb://mycontainer@mystorageaccount.blob.core.windows` diğer giriş job.xml dosyası kullanılan değeri olan metin.

   * Başlangıç tanımlamak için aşağıdaki XML bitiş ve düzenleyici sıklığı ekleyin:

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

       Bu değerleri 10 May 2017'den itibaren 12 Mayıs 2017 için bitiş zamanı üzerinde 12:00 PM için başlangıç saatini ayarlayın. Bu işi her gün aralığı. Dakika cinsinden sıklığıdır 1440 dakika 24 saat x 60 dakika kadar =. Son olarak, saat dilimi UTC için ayarlanır.

5. CTRL-X, daha sonra kullanmak **Y** ve **Enter** dosyayı kaydetmek için.

6. İşi çalıştırmak için aşağıdaki komutu kullanın:

    ```
    oozie job -config job.xml -run
    ```

    Bu komut gönderir ve işini başlatır.

7. Oozie Web kullanıcı arabirimini ziyaret edin ve seçin, **Düzenleyicisi işleri** sekmesinde, aşağıdaki görüntüye benzer bilgileri görebilirsiniz:

    ![Düzenleyici işler sekmesi](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    **Sonraki Materialization** girişi, işin bir sonraki çalıştırmasında içeriyor.

8. Önceki iş akışının benzeyen, web kullanıcı Arabirimi iş girişine seçme bilgileri işinde görüntüler:

    ![Düzenleyici iş bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Bu görüntü yalnızca başarılı çalıştırır zamanlanmış iş akışı içinde bireysel Eylemler işinin gösterir. İçin bkz, aşağıdakilerden birini seçin **eylem** girişleri.

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Sorun giderme

Oozie UI Oozie günlükleri görüntülemenize izin verir. Ayrıca, iş akışı tarafından başlatılan MapReduce görevler için Jobtracker'a günlüklerini bağlantılar içerir. Sorun giderme için desen olmalıdır:

1. İşi Oozie Web Arabiriminde görüntüleyin.

2. Bir hata veya belirli bir eylemi için hatası ise, olmadığını görmek için bir eylem seçin **hata iletisi** alan hatada daha fazla bilgi sağlar.

3. Varsa, eyleminden URL eylemi için (örneğin, Jobtracker'a günlükleri) daha fazla ayrıntı görüntülemek için kullanın.

Karşılaşabileceğiniz belirli hataları ve bunların nasıl çözüleceği verilmiştir.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: küme başlatılamıyor

**Belirtiler**: İş durumu değişikliklerini **ASKIYA**. İşe yönelik ayrıntıları göster olarak RunHiveScript durumu **START_MANUAL**. Eylem seçildikten aşağıdaki hata iletisini görüntüler:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Neden**: kullanılan WASB adresleri **job.xml** dosya depolama kapsayıcısı veya depolama hesabı adı içermiyor. WASB adres biçimini olmalıdır `wasb://containername@storageaccountname.blob.core.windows.net`.

**Çözümleme**: İş tarafından kullanılan WASB adreslerini değiştirin.

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a>JA002: Oozie almasına izin verilmiyor &lt;kullanıcı >

**Belirtiler**: İş durumu değişikliklerini **ASKIYA**. İşe yönelik ayrıntıları göster olarak RunHiveScript durumu **START_MANUAL**. Eylem seçmek aşağıdaki hata iletisini gösterir:

    JA002: User: oozie is not allowed to impersonate <USER>

**Neden**: Geçerli izin ayarlarını Oozie belirtilen kullanıcı hesabı almasına izin vermez.

**Çözümleme**: Oozie izin verilir, kullanıcının kimliğine bürünmek için **kullanıcılar** grubu. Kullanım `groups USERNAME` kullanıcı hesabının bir üyesi olduğu grupların görmek için. Kullanıcı bir üyesi değilse **kullanıcılar** grup, kullanıcı grubuna eklemek için aşağıdaki komutu kullanın:

    sudo adduser USERNAME users

> [!NOTE]
> Kullanıcı grubuna eklenmiş olan Hdınsight algılamasından önce birkaç dakika sürebilir.

### <a name="launcher-error-sqoop"></a>Başlatıcı hata (Sqoop)

**Belirtiler**: İş durumu değişikliklerini **KILLED**. İşe yönelik ayrıntıları göster olarak RunSqoopExport durumu **hata**. Eylem seçmek aşağıdaki hata iletisini gösterir:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Neden**: Sqoop veritabanına erişmek için gerekli veritabanı sürücüsünü yükleyemiyor.

**Çözümleme**: Sqoop, Oozie işten kullanırken, iş tarafından kullanılan veritabanı sürücüsünü diğer kaynaklarla (örneğin, workflow.xml) içermelidir. Ayrıca veritabanı sürücüyü içeren arşiv başvuru `<sqoop>...</sqoop>` workflow.xml bölümü.

Örneğin, bu belgede proje için aşağıdaki adımları kullanırsınız:

1. Sqljdbc4.1.jar dosyasını /tutorials/useoozie dizinine kopyalayın:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Yeni bir satıra yukarıdaki aşağıdaki XML eklemek için workflow.xml değiştirmek `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Oozie iş akışı tanımlama ve Oozie işini çalıştır öğrendiniz. Hdınsight ile çalışma hakkında daha fazla bilgi edinmek için aşağıdaki makalelere bakın:

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
