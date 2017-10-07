---
title: "aaaApache örnek Java topolojisi - Azure Hdınsight Storm | Microsoft Docs"
description: "Bir örnek sözcük oluşturarak toocreate Apache Storm topolojilerini Java topolojisi nasıl saymak öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Apache storm, apache storm örnek, storm java, storm topoloji örneği"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Apache Storm topolojisini Java oluşturma

Bilgi nasıl toocreate Apache Storm için Java tabanlı bir topolojiyi. Word-count uygulama uygulayan bir Storm topolojisinin oluşturun. Maven toobuild ve paket hello proje kullanın. Daha sonra nasıl toodefine hello topolojisi kullanarak izin ver hello Flux framework öğrenin.

> [!NOTE]
> Merhaba Flux Storm 0.10.0 veya sonraki sürümlerinde çerçevedir. Storm 0.10.0 Hdınsight 3.3 ve 3.4 ile kullanılabilir.

Bu belgedeki Hello adımları tamamladıktan sonra hello topoloji tooApache Hdınsight üzerinde Storm dağıtabilirsiniz.

> [!NOTE]
> Bu belgede oluşturulan hello Storm topolojisini örnekler tamamlanmış bir sürümünü şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Ön koşullar

* [Java Geliştirme Seti (JDK) sürüm 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven Java projeleri için bir proje derleme sistemidir.

* Bir metin düzenleyicisi veya IDE.

## <a name="configure-environment-variables"></a>Ortam değişkenleri yapılandırın

Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir. Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.

* **JAVA_HOME** -hello Java Çalışma zamanı ortamı (JRE) yüklü olduğu toohello dizin işaret etmelidir. Örneğin, bir UNIX veya Linux dağıtımlarında benzeri bir değer çok olması gereken`/usr/lib/jvm/java-7-oracle`. Windows'da onu benzeri bir değer çok gerekir`c:\Program Files (x86)\Java\jre1.7`

* **YOL** -yolları aşağıdaki hello içermelidir:

  * **JAVA_HOME** (veya hello eşdeğer yolu)

  * **JAVA_HOME\bin** (veya hello eşdeğer yolu)

  * Maven'ın yüklendiği hello dizini

## <a name="create-a-maven-project"></a>Bir Maven projesi oluşturun

Merhaba komut satırından kullanma hello aşağıdaki toocreate adlı bir Maven projesi komutu **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> PowerShell kullanıyorsanız, çevreleyen gerekir`-D` çift tırnak işareti parametrelerle.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Bu komut adlı bir dizin oluşturur `WordCount` hello geçerli konumda içeren temel bir Maven projesi. Merhaba `WordCount` dizini aşağıdaki öğelerindeki hello içerir:

* `pom.xml`: Merhaba Maven projesine ayarlarını içerir.
* `src\main\java\com\microsoft\example`: Uygulama kodunuz içerir.
* `src\test\java\com\microsoft\example`: Uygulamanız için testleri içerir. 

### <a name="remove-hello-generated-example-code"></a>Merhaba oluşturulan örnek kodu kaldırın

Oluşturulan hello test ve hello uygulama dosyaları silin:

* **src\test\java\com\microsoft\example\AppTest.Java**
* **src\main\java\com\microsoft\example\App.Java**

## <a name="add-maven-repositories"></a>Maven depoları ekleme

Hdınsight üzerinde hello Hortonworks veri Platformu (HDP) dayalı, bu yüzden hello Hortonworks depo toodownload bağımlılıkları Apache Storm projeleriniz için kullanmanızı öneririz. Merhaba, __pom.xml__ dosya, XML hello sonra aşağıdaki hello eklemek `<url>http://maven.apache.org</url>` satır:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Özellikler ekleme

Maven özellikleri olarak adlandırılan toodefine proje düzeyi değerlere izin verir. Merhaba, __pom.xml__, metin hello sonra aşağıdaki hello eklemek `</repositories>` satır:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

Bu değer hello diğer bölümlerinde artık kullanabilirsiniz `pom.xml`. Örneğin, Storm bileşenleri hello sürümü belirtirken kullanabileceğiniz `${storm.version}` sabit bir değer kodlama yerine.

## <a name="add-dependencies"></a>Bağımlılıkları ekleyin.

Storm bileşenleri için bağımlılık ekleyin. Açık hello `pom.xml` dosya ve hello kodda aşağıdaki hello ekleyin `<dependencies>` bölümü:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

Bu bilgi toolook Maven derleme zamanında kullanan `storm-core` hello Maven deposundaki. Yerel bilgisayarınızda hello deposundaki İlk bakar. Merhaba dosyaları yoksa, Maven hello ortak Maven depodan indirir ve hello yerel depoda depolar.

> [!NOTE]
> Bildirim hello `<scope>provided</scope>` bu bölümdeki satır. Bu ayar Maven tooexclude söyler **storm çekirdek** hello sistem tarafından sağlanan bulunduğundan, oluşturulan JAR dosyalarını.

## <a name="build-configuration"></a>Derleme yapılandırması

Maven eklentileri toocustomize hello derleme aşamaları hello projesinin izin verin. Örneğin, nasıl hello Proje derlenir veya nasıl toopackage JAR dosyasını içine. Açık hello `pom.xml` dosya ve doğrudan hello yukarıdaki kodu aşağıdaki hello ekleyin `</project>` satır.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Bu bölümde kullanılan tooadd eklentileri, kaynakları ve diğer yapı yapılandırma seçenekleri ' dir. Merhaba, tam başvuru için **pom.xml** dosya için bkz: [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Eklentiler

Java'da uygulanan Apache Storm topolojilerini için hello [Exec Maven eklentisi](http://www.mojohaus.org/exec-maven-plugin/) hello topolojisi geliştirme ortamınızı yerel olarak çalıştırma tooeasily izin verdiği için kullanışlıdır. Toohello aşağıdaki hello eklemek `<plugins>` hello bölümünü `pom.xml` tooinclude hello Exec Maven eklenti dosyası:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Başka yararlı hello eklentidir [Apache Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/), hangi derleme seçenekleri kullanılan toochange değil. Merhaba değişiklikleri hello kaynak ve hedef uygulamanız için Maven kullanımları Java sürümü hello.

* Hdınsight için __3.4 veya önceki__hello kaynak ayarlamak ve Java Sürüm too__1.7__ hedef.

* Hdınsight için __3.5__hello kaynak ayarlamak ve Java Sürüm too__1.8__ hedef.

Merhaba metinde aşağıdaki hello eklemek `<plugins>` hello bölümünü `pom.xml` tooinclude hello Apache Maven derleyici eklentisi dosya. Merhaba hedef Hdınsight sürüm 3.5 olması için bu örnek 1.8, belirtir.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Kaynaklarını yapılandırma

Merhaba kaynakları bölümü hello topolojisinde bileşenleri tarafından gereken yapılandırma dosyaları gibi tooinclude kod olmayan kaynakları sağlar. Bu örnekte, hello metinde aşağıdaki hello eklemek `<resources>` hello bölümünü ' pom.xml dosyasını.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

Bu örnek hello kaynakları dizin hello hello proje kök dizininde ekler (`${basedir}`) kaynaklar içeriyor ve adlı hello dosya içeren bir konum olarak `log4j2.xml`. Bu dosya kullanılan tooconfigure hello topolojisi tarafından hangi bilgilerin oturum açmış durumda.

## <a name="create-hello-topology"></a>Merhaba topolojisi oluştur

Java tabanlı Apache Storm topolojisini bağımlılık olarak yazmanız gerekir üç bileşeni (veya başvuru) oluşur.

* **Spout'lar**: dış veri kaynakları ve veri akışları hello topoloji yayar okur.

* **Cıvatalar**: spout'lar veya diğer Cıvatalar tarafından gösterilen akışları üzerinde işlemeyi gerçekleştirir ve bir veya daha fazla akışları yayar.

* **Topoloji**: nasıl hello spout'lar ve Cıvatalar düzenlenir ve hello giriş noktası için hello topolojisi sunar tanımlar.

### <a name="create-hello-spout"></a>Merhaba spout oluşturma

Dış veri kaynakları için tooreduce gereksinimler hello aşağıdaki spout yalnızca rastgele cümleleri yayar. Merhaba ile sağlanan bir spout değiştirilmiş bir sürümünü olan [Storm Starter örnekleri](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Bir dış veri kaynağından okur spout bir örnek için örnek hello birine bakın:
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): Twitter'dan okuyan bir örnek spout
> * [Storm Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): Kafka okur spout

Merhaba spout için adlı bir dosya oluşturun `RandomSentenceSpout.java` hello içinde `src\main\java\com\microsoft\example` hello içeriği Java kod aşağıdaki dizin ve kullanım hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Bu topoloji yalnızca bir spout kullansa da, diğerlerinin hello topoloji farklı kaynaklardan veri akışı birkaç olabilir.

### <a name="create-hello-bolts"></a>Merhaba Cıvatalar oluşturma

Cıvatalar hello veri işleme işleyin. Bu topoloji iki Cıvatalar kullanır:

* **SplitSentence**: böler tarafından gösterilen hello cümleleri **RandomSentenceSpout** ayrı sözcükleri içine.

* **WordCount**: her sözcüğün oluştu kaç kez sayar.

> [!NOTE]
> Cıvatalar hiçbir şey, örneğin, hesaplama, sürdürme veya tooexternal bileşenleri Konuşmayı yapabilirsiniz.

İki yeni dosyalar oluşturma `SplitSentence.java` ve `WordCount.java` hello içinde `src\main\java\com\microsoft\example` dizin. Metin olarak hello içeriği hello dosyaları için aşağıdaki hello kullan:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Merhaba topolojisi tanımlayın

Merhaba topolojisi hello spout'lar bağlar ve hello bileşenler arasında veri akışını tanımlayan bir grafik içine birlikte Cıvatalar. Ayrıca, Storm hello bileşenleri hello küme içinde örneklerini oluştururken kullandığı paralellik ipuçlarını sağlar.

Merhaba aşağıdaki temel bir hello grafik bu topoloji bileşenleri diyagramı görüntüdür.

![Diyagram gösteren hello spout'lar ve düzenlemeyi Cıvatalar](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement topoloji Merhaba, adlı bir dosya oluşturun `WordCountTopology.java` hello içinde `src\main\java\com\microsoft\example` dizin. Java kod hello dosyasının Merhaba içeriğine aşağıdaki hello kullan:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Günlük tutmayı yapılandırma

Storm Apache Log4j toolog bilgileri kullanır. Günlük kaydını yapılandırmazsanız hello topoloji tanılama bilgisi yayar. ne kaydedilir, toocontrol adlı bir dosya oluşturun `log4j2.xml` hello içinde `resources` dizin. XML hello hello dosyasının içeriğini aşağıdaki hello kullanın.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Yeni bir Günlükçü hello için bu XML yapılandırır `com.microsoft.example` Bu örnek topolojide hello bileşenleri içeren sınıf. Merhaba düzeyi tootrace bu topolojide bileşenleri tarafından gösterilen tüm günlük bilgilerini yakalar bu Günlükçü için ayarlanır.

Merhaba `<Root level="error">` bölüm günlük hello kök düzeyi yapılandırır (içinde değil her şeyi `com.microsoft.example`) tooonly günlük hata bilgileri.

Log4j için günlüğe kaydetmeyi yapılandırma hakkında daha fazla bilgi için bkz: [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> Storm sürüm 0.10.0 ve daha yüksek kullanım Log4j 2.x. Storm eski sürümlerinde kullanılan Log4j günlük yapılandırması için farklı bir biçim kullanılan 1.x. Merhaba eski yapılandırması hakkında daha fazla bilgi için bkz: [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Yerel olarak test hello topolojisi

Merhaba dosyaları kaydettikten sonra yerel olarak komut tootest hello topolojisi aşağıdaki hello kullanın.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Çalışırken, hello topolojisini başlangıç bilgileri görüntüler. Merhaba aşağıdaki metni hello word sayısı çıkış örneğidir:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Bu örnek günlük dosyası bu hello sözcüğü gösterir ' ve ' 113 kez yayılan. Merhaba spout sürekli hello yayar çünkü hello topoloji çalıştığı sürece hello sayısı toogo yukarı devam aynı cümleleri.

Sözcükler yayımlanmasını ve sayılar arasında 5 saniye aralığını yoktur. Merhaba **WordCount** bileşen yapılandırılmış değer çizgisi tanımlama grubu geldiğinde tooonly yayma bilgi. Diziler yalnızca beş saniyede teslim edilir, onay ister.

## <a name="convert-hello-topology-tooflux"></a>Merhaba topoloji tooFlux Dönüştür

Flux uygulama tooseparate yapılandırmasından sağlayan bir yeni kullanılabilir Storm 0.10.0 veya üzeri bir çerçevedir. Bileşenlerinizi Java'da tanımlanmış olan ancak hello topoloji YAML dosyası kullanılarak tanımlanır. Projenizi ile varsayılan topoloji tanımı paketini veya tek başına dosya hello topoloji gönderirken kullanın. Merhaba topoloji tooStorm gönderirken hello YAML topoloji tanımı ortam değişkenleri veya yapılandırma dosyaları toopopulate değerlerini kullanabilirsiniz.

Merhaba YAML dosyası hello bileşenleri toouse hello topolojisi ve aralarındaki hello veri akışı için tanımlar. Bir YAML dosyası hello jar dosyasını bir parçası olarak ekleyebilirsiniz veya dış YAML dosyası kullanabilirsiniz.

Flux hakkında daha fazla bilgi için bkz: [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Son tooa [hata (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) Storm 1.0.1 tooinstall gerekebilir bir [Storm geliştirme ortamı](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux yerel olarak topolojileri.

1. Merhaba taşıma `WordCountTopology.java` dosya hello proje dışında. Daha önce bu dosyayı hello topoloji tanımlı, ancak Flux ile gerekli değildir.

2. Merhaba, `resources` dizin adlı bir dosya oluşturun `topology.yaml`. Bu dosyanın içeriğini hello metin aşağıdaki hello kullanın.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Değişiklikleri toohello aşağıdaki hello olun `pom.xml` dosya.
   
   * Yeni bağımlılık hello olarak aşağıdaki hello eklemek `<dependencies>` bölümü:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Eklenti toohello aşağıdaki hello eklemek `<plugins>` bölümü. Bu eklenti hello proje için bir paket (jar dosyasını) hello oluşturulmasını işler ve bazı dönüşümleri belirli tooFlux hello paket oluştururken uygular.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * Merhaba, **exec maven eklentisi** `<configuration>` bölümünde, hello değerini değiştirmek `<mainClass>` çok`org.apache.storm.flux.Flux`. Bu ayar hello topolojisi geliştirme yerel olarak çalışan Flux toohandle sağlar.

   * Merhaba, `<resources>` bölümünde, toohello aşağıdaki hello eklemek `<includes>`. Bu XML hello topoloji hello projesinin bir parçası tanımlayan hello YAML dosyası içerir.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Yerel olarak test hello flux topolojisi

1. Maven kullanarak hello Flux topolojisi yürütün ve toocompile aşağıdaki hello kullanın:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    PowerShell kullanıyorsanız, hello aşağıdaki komutu kullanın:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Topolojiniz Storm 1.0.1 BITS kullanıyorsa, bu komut başarısız olur. Bu hatanın nedeni [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). Bunun yerine, [geliştirme ortamınızda Storm yüklemek](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) ve kullanım hello aşağıdaki bilgileri.

    Varsa [Storm geliştirme ortamınızda yüklü](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), komutları bunun yerine aşağıdaki hello kullanabilirsiniz:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Merhaba `--local` parametre yerel modda hello topolojisi geliştirme ortamınızı çalıştırır. Merhaba `-R /topology.yaml` parametresini kullanır hello `topology.yaml` hello jar dosyasını toodefine hello topoloji kaynak dosya.

    Çalışırken, hello topolojisini başlangıç bilgileri görüntüler. metin aşağıdaki hello hello çıkış örneğidir:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Günlüğe kaydedilen bilgileri toplu işlemleri arasında 10 saniye gecikme olur.

2. Merhaba kopyası `topology.yaml` hello proje dosyasından. Ad hello yeni dosya `newtopology.yaml`. Merhaba, `newtopology.yaml` dosya, hello aşağıdaki bölümünde ve hello değerini değiştirme Bul `10` çok`5`. Word'ün toplu yayma arasındaki bu değişikliği değişiklikleri hello aralığı 10 saniye too5 sayar.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    Veya, geliştirme ortamınızı Storm varsa:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Değişiklik hello `/path/to/newtopology.yaml` hello önceki adımda oluşturduğunuz toohello yolu toohello newtopology.yaml dosyası. Bu komut hello newtopology.yaml hello topoloji tanımı olarak kullanır. Biz hello eklemediniz beri `compile` parametresi, Maven önceki adımlarda kurulu hello proje hello sürümünü kullanır.

    Bir kez hello topolojisini başlatır ve verilmiş toplu işlemleri arasındaki hello süre tooreflect hello newtopology.yaml değerinde değiştiğine dikkat edin. Bu nedenle, yapılandırmanızı YAML dosyası aracılığıyla toorecompile hello topoloji gerek kalmadan değiştirebileceğiniz olduğunu görebilirsiniz.

Bunlar ve diğer özellikler hello Flux framework'ün hakkında daha fazla bilgi için bkz: [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident Storm tarafından sağlanan üst düzey bir soyutlamadır. Durum bilgisi olan işlemeyi destekler. Trident birincil avantajı Hello hello topoloji girer her ileti yalnızca bir kez işlenir garanti edebilir sağlamasıdır. Trident kullanmadan topolojinizi yalnızca iletileri en az bir kez işlenir garanti edebilir. Cıvatalar oluşturmak yerine kullanılabilir yerleşik bileşenleri gibi diğer farklar vardır. Aslında, Cıvatalar filtreleri, tahminleri ve işlevleri gibi daha az genel bileşenler tarafından değiştirilir.

Trident uygulamaları Maven projelerini kullanarak oluşturulabilir. Hello kullandığınız aynı temel adımlar bu makalenin önceki bölümlerinde sunulan — yalnızca hello kodu farklı. Trident de (şu anda) hello Flux framework ile kullanılamaz.

Trident hakkında daha fazla bilgi için bkz: Merhaba [Trident API genel bakış](http://storm.apache.org/documentation/Trident-API-Overview.html).

Trident uygulama örneği için bkz: [hdınsight'ta Apache Storm oluşturan eğilim konuları Twitter](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Sonraki Adımlar

Öğrendiğiniz nasıl toocreate Java kullanarak bir Storm topolojisinin. Daha fazla bilgi nasıl yapılır:

* [Dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology.md)

* [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Daha fazla örnek Storm topolojileri ziyaret ederek bulabileceğiniz [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).

