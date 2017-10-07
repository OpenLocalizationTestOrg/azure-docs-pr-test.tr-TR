---
title: "Event Hubs Java kullanarak Hdınsight üzerinde Storm ile aaaProcess olaylarından | Microsoft Docs"
description: "Maven ile tooprocess bir Storm Java topolojisi ile Event Hubs verilerini nasıl oluşturulacağını öğrenin."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Azure Event hubs'tan (Java) hdınsight'ta Storm işlem olayları

Bilgi nasıl toouse Azure Event Hubs Hdınsight üzerinde Storm ile. Bu örnek, Azure Event Hubs Java tabanlı bileşenler tooread ve yazma verileri kullanır.

Azure Event Hubs, Web siteleri, uygulamaları ve cihazları verilerini oldukça büyük miktardaki tooprocess sağlar. Merhaba olay hub'ı spout kolay toouse kolaylaştırır Apache Storm Hdınsight tooanalyze üzerinde gerçek zamanlı bu verileri. Olay hub'ları Cıvata hello kullanarak Storm veri tooEvent hub de yazabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight küme sürümü 3.6 üzerinde Apache Storm. Daha fazla bilgi için bkz: [Hdınsight kümesinde Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Bir [Azure olay hub'ı](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Oracle Java Geliştirme Seti (JDK) sürüm 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) veya eşdeğer gibi [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): Maven Java projeleri için bir proje derleme sistemidir.

* Bir metin düzenleyicisi veya tümleşik geliştirme ortamı (IDE).

    > [!NOTE]
    > Bu belgede ele Maven çalışmak için belirli işlevleri Düzenleyicisi veya IDE olabilir. Düzenleme ortamınızı hello özellikleri hakkında daha fazla bilgi için kullanmakta olduğunuz hello ürününün hello belgelerine bakın.

    * Bir SSH istemcisi. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

* Merhaba `ssh` ve `scp` komutları. Kullanılan toocopy dosyaları toohello Hdınsight kümesi bunlar. Windows, bunlar Bash Windows 10 aracılığıyla elde edebilirsiniz.

## <a name="understanding-hello-example"></a>Anlama Merhaba örneği

Merhaba [hdınsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) örnek, iki topoloji içerir:

Merhaba `resources/writer.yaml` topoloji rastgele veri tooan Azure olay hub'ı yazar. Merhaba veri hello tarafından oluşturulan `DeviceSpout` bileşeni ve rastgele cihaz kimliği ve cihaz değer. Bu nedenle dize kimliği ve bir sayısal değer yayar bazı donanım benzetimi.

Üç `resources/reader.yaml` topoloji okur olay hub'ı (Merhaba veri EventHubWriter tarafından yazılan) verileri hello JSON verilerini ayrıştırır ve ardından günlükleri hello `deviceId` ve `deviceValue` veri.

Veri Merhaba biçimlendirilmiş onu tooEvent Hub yazılmış ve ne zaman hello okuyucu tarafından okuma önce bir JSON belgesi olarak, JSON dışında ve diziler olarak ayrıştırılır. Merhaba JSON biçimi aşağıdaki gibidir:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Proje yapılandırması

Merhaba `POM.xml` dosyası bu bir Maven projesi için yapılandırma bilgilerini içerir. Merhaba ilginç parça şunlardır:

#### <a name="event-hub-components"></a>Olay hub'ı bileşenleri

okuyan ve yazan tooAzure olay hub'ları hello bileşen hello bulunan [Hdınsight depo](https://github.com/hdinsight/mvn-rep). Merhaba hello bölümlerde aşağıdaki `POM.xml` bu depodan yük hello bileşenleri dosya

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Merhaba EventHubs Storm Spout bağımlılık

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Bu xml hem spout Event hubs'dan okumak için hem de tooit yazmak için bir Cıvata içeren hello eventhubs paket için bağımlılık tanımlar.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Bu xml hello proje toogenerate çıktısı Hdınsight 3.5 veya daha yüksek kullanılan 8, Java için yapılandırır.

#### <a name="hello-maven-shade-plugin"></a>maven gölge eklentisi hello

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

Bu xml hello çözüm toopackage hello çıktı uber jar yapılandırır. Merhaba jar hello proje kodunu ve gerekli bağımlılıkları içerir. İçin de kullanılır:

* Merhaba bağımlılıklar için lisans dosyalarını yeniden adlandırın.
* Güvenlik/imzaları hariç tutun.
* Birden çok uygulamaları aynı hello olun arabirimi, tek bir giriş olarak birleştirilir.

Bu yapılandırma ayarları çalışma zamanı hataları engeller.

#### <a name="topology-definitions"></a>Topoloji tanımları

Bu örnek hello kullanır [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework. Bu çerçeve YAML toodefine hello topolojileri kullanır. Merhaba birincil avantajı, Java kod hello topolojisinde kodlama sabit olmayan ' dir. Merhaba tanımı YAML olduğundan, toorecompile her şeyi gerek kalmadan hello topoloji, göndermeden önce değiştirebilirsiniz.

__Writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__Reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Olay hub'ı hakkında Hello topoloji söyleyin

Çalışma zamanında hello `dev.properties` kullanılan toopass hello olay hub'ı yapılandırma toohello topoloji bir dosyadır. Merhaba aşağıdaki hello varsayılan hello dosyasının içeriğini örnektir:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Ortam değişkenleri yapılandırın

Geliştirme iş istasyonunuza Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir. Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.

* **JAVA_HOME** -hello Java Çalışma zamanı ortamı (JRE) yüklü olduğu toohello dizin işaret etmelidir. Örneğin, bir UNIX veya Linux dağıtımlarında benzeri bir değer çok olması gereken`/usr/lib/jvm/java-7-oracle`. Windows'da onu benzeri bir değer çok gerekir`c:\Program Files (x86)\Java\jre1.7`
* **YOL** -yolları aşağıdaki hello içermelidir:

  * **JAVA_HOME** (veya hello eşdeğer yolu)
  * **JAVA_HOME\bin** (veya hello eşdeğer yolu)
  * Maven'ın yüklendiği hello dizini

## <a name="configure-event-hub"></a>Olay hub'ı yapılandırma

Bu örnek için hello veri kaynağı olay hub ' dir. Merhaba aşağıdaki adımları toocreate bir olay hub'ı kullanın.

1. Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com)seçin **yeni** > **Service Bus** > **olay hub'ı**  >  **Özel Oluştur**.

2. Merhaba üzerinde **yeni bir olay hub'ı eklemek** ekranında, girin bir **olay hub'ı adı**. Select hello **bölge** toocreate Merhaba, hub ve ad alanı oluşturma veya varolan bir tanesini seçin. Son olarak, hello tıklatın **ok** toocontinue.

    ![Sihirbaz sayfası 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Select hello aynı **konumu** Hdınsight sunucu tooreduce gecikme süresi ve maliyetleri üzerinde Storm'a olarak.

3. Merhaba üzerinde **Event Hub'ı yapılandırma** ekranında, hello girin **bölüm sayısı** ve **ileti bekletme** değerleri. Bu örnekte, bir bölüm sayısı 10 ve 1 ileti bekletilmesini kullanın. Bu değer daha sonra gerektiğinden hello bölüm sayısı unutmayın.

    ![Sihirbaz sayfası 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Merhaba olay hub'ı oluşturulan, select hello ad alanı sağlandıktan sonra seçin **olay hub'ları**ve ardından daha önce oluşturduğunuz hello olay hub'ı seçin.
5. Seçin **yapılandırma**, sonra aşağıdaki bilgilerle hello kullanarak iki yeni erişim ilkeleri oluşturun:

    <table>
    <tr><th>Ad</th><th>İzinler</th></tr>
    <tr><td>Yazıcı</td><td>Gönder</td></tr>
    <tr><td>Okuyucu</td><td>Dinleme</td></tr>
    </table>

    Merhaba izinleri oluşturduktan sonra hello seçin **kaydetmek** hello sayfanın hello simgesine tıklayın. Bu paylaşılan erişim ilkeleri kullanılan tooread ve tooEvent Hub yazma.

    ![ilkeleri](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Merhaba ilkeleri kaydettikten sonra hello kullan **paylaşılan erişim anahtarı Oluşturucu** hello sayfası tooretrieve hello anahtarını hello hello sonundaki **yazan** ve **okuyucu** ilkeleri. Bu anahtarları kaydedin.

## <a name="download-and-build-hello-project"></a>Karşıdan yükle ve Merhaba projeyi derleme

1. Merhaba projeyi Github'dan indirin: [hdınsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Zip arşivini olarak hello paketini indirin veya kullanmak [git](https://git-scm.com/) tooclone hello projesini yerel olarak.

2. Merhaba değiştirme `dev.properties` olay Hub'ınız için hello yapılandırma dosyasıyla.

3. Toobuild ve paket hello proje aşağıdaki hello kullan:

        mvn package

    Bu komut gerekli bağımlılıkları, derlemeleri, yükler ve ardından paketler proje hello. Merhaba çıktı hello depolanan **/target** olarak dizin **EventHubExample 1.0 SNAPSHOT.jar**.

## <a name="test-locally"></a>Yerel olarak test etme

Bu topolojileri yalnızca okuma ve tooEvent hub'ları yazma olduğundan, yerel olarak varsa, bunları test edebilirsiniz bir [Storm geliştirme ortamı](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Aşağıdaki adımları toorun hello geliştirme ortamında yerel olarak hello kullan:

1. Merhaba yazan çalıştırın:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Merhaba okuyucu çalıştırın:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Hello topoloji yerel modda (dağıtılmış olmayan) çalıştırın.
> * `-R /writer.yaml`: Hello hello topoloji tanımı yük `resources` hello jar paketlenir. Merhaba topoloji hello yerel dosya sistemindeki bir dosyaya ise hello yolu tooit hello son parametre olarak bunun yerine belirtin.
> * `--filter dev.properties`: Kullanın Merhaba içeriğine `dev.properties` toofill hello topoloji tanımlarında hello değerleri. Örneğin, `${eventhub.read.policy.name}`.

Çıktı oturum toohello yerel olarak çalıştırırken konsoludur. Kullanım __Ctrl + C__ toostop hello topolojisi.

## <a name="deploy-hello-topologies"></a>Merhaba topolojilerini dağıtma

1. SCP toocopy hello jar paket tooyour Hdınsight kümesi kullanın. Merhaba SSH kullanıcı kümeniz için kullanıcı adını değiştirin. CLUSTERNAME hello Hdınsight kümenizin adıyla değiştirin:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    SSH hesabınız için parola kullandıysanız, istendiğinde tooenter hello parola olur. Merhaba hesabıyla bir SSH anahtarı kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yol toohello anahtar dosyası. Örneğin, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Bu komut hello dosya toohello giriş dizinine hello kümede SSH kullanıcı kopyalar.

2. Merhaba dosya karşıya yükleme tamamlandıktan sonra SSH tooconnect toohello Hdınsight kümesi kullanın. Değiştir **kullanıcıadı** SSH oturumunuzla hello adı. Değiştir **CLUSTERNAME** Hdınsight küme adıyla:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > SSH hesabınız için parola kullandıysanız, istendiğinde tooenter hello parola olur. Merhaba hesabıyla bir SSH anahtarı kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yol toohello anahtar dosyası. Merhaba aşağıdaki örnek yükler hello özel anahtarı `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Komut toostart hello topolojileri aşağıdaki hello kullan:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Hello topoloji toohello hello kümesindeki hello alt düğümlerinde başlatır Nimbus hizmet gönderir.

4. tooview hello günlüğe kaydedilen veri, Git toohttps://CLUSTERNAME.azurehdinsight.net/stormui, burada __CLUSTERNAME__ Hdınsight kümenize hello adıdır. Hello topolojileri seçin ve toohello bileşenleri ayrıntıya gidin. Select hello __bağlantı noktası__ bileşen tooview örneği için girişi günlüğe bilgi.

5. Aşağıdaki komutları toostop hello topolojileri hello kullan:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Kümenizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Sonraki adımlar

* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)
