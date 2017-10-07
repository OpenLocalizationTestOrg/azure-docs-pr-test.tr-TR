---
title: "aaaCreate Hadoop - Azure Hdınsight için Java MapReduce | Microsoft Docs"
description: "Bilgi nasıl toouse Apache Maven toocreate Java tabanlı MapReduce uygulama çalıştırın Hadoop ile Azure Hdınsight'ta."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek

Bilgi nasıl toouse Apache Maven toocreate Java tabanlı MapReduce uygulama çalıştırın Hadoop ile Azure Hdınsight'ta.

> [!NOTE]
> Bu örnekte, en son Hdınsight 3.6 üzerinde test edilmiştir.

## <a name="prerequisites"></a>Önkoşullar

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 veya sonraki (veya eşdeğeri, OpenJDK gibi bir).
    
    > [!NOTE]
    > Hdınsight sürüm 3.4 ve önceki Java 7 kullanın. Hdınsight 3.5 ve büyük Java 8 kullanır.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Geliştirme ortamını yapılandırma

Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir. Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.

* `JAVA_HOME`-hello Java Çalışma zamanı ortamı (JRE) yüklü olduğu toohello dizin işaret etmelidir. Örneğin, OS X, UNIX veya Linux bir sistemde, benzer bir değer çok olmalıdır`/usr/lib/jvm/java-7-oracle`. Windows'da onu benzeri bir değer çok gerekir`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-yolları aşağıdaki hello içermelidir:
  
  * `JAVA_HOME`(veya eşdeğer yolu hello)

  * `JAVA_HOME\bin`(veya eşdeğer yolu hello)

  * Maven'ın yüklendiği hello dizini

## <a name="create-a-maven-project"></a>Bir Maven projesi oluşturun

1. Bir terminal oturumu veya komut satırından geliştirme ortamında, bu proje toostore istediğiniz dizinleri toohello konumunu değiştirebilirsiniz.

2. Kullanım hello `mvn` Maven toogenerate hello hello projesi için iskele ile yüklenen komutu.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > PowerShell kullanıyorsanız, hello almalısınız `-D` çift tırnak işareti parametreleri.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Bu komut, hello tarafından belirtilen hello ada sahip bir dizin oluşturur. `artifactID` parametre (**wordcountjava** Bu örnekte.) Bu dizin hello aşağıdaki öğeleri içerir:

   * `pom.xml`-hello [proje nesne modeli (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) bilgileri içeren ve yapılandırma ayrıntılarını kullanılan toobuild hello projesi.

   * `src`-Merhaba uygulaması içeren başlangıç dizini.

3. Merhaba silme `src/test/java/org/apache/hadoop/examples/apptest.java` dosya. Bu örnekte kullanılmaz.

## <a name="add-dependencies"></a>Bağımlılıkları ekleyin.

1. Merhaba Düzenle `pom.xml` dosya ve metin hello içinde aşağıdaki hello ekleyin `<dependencies>` bölümü:
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    Bu gerekli kitaplıklar tanımlar (içinde listelenen &lt;Artifactıd\>) belirli bir sürümle (içinde listelenen &lt;sürüm\>). Derleme zamanında hello varsayılan Maven depodan bu bağımlılıkları indirilir. Merhaba kullanabilirsiniz [Maven deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview daha fazla.
   
    Merhaba `<scope>provided</scope>` hello Hdınsight kümesi çalışma zamanında tarafından sağlanan Maven Bu bağımlılıklar hello uygulamayla paketlenmesi değil olduğunu bildirir.

    > [!IMPORTANT]
    > kullanılan hello sürümü Hadoop kümenizde mevcut hello sürümüyle eşleşmelidir. Merhaba sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.

2. Toohello aşağıdaki hello eklemek `pom.xml` dosya. Bu metin hello içinde olmalıdır `<project>...</project>` etiketleri hello dosya; Örneğin, arasında `</dependencies>` ve `</project>`.

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    Merhaba ilk eklentisi yapılandırır hello [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/), hangi kullanılan toobuild hello uygulama tarafından gerekli bağımlı içeren (bazen bir fatjar olarak da adlandırılır) bir uberjar değil. Ayrıca, bazı sistemlerde sorunlara yol açabilir hello jar paketin içinde lisansları yinelenmesini önler.

    Merhaba ikinci eklentisi hello hedef Java sürümü yapılandırır.

    > [!NOTE]
    > Hdınsight 3.4 ve Java 7 önceki kullanın. Hdınsight 3.5 ve büyük Java 8 kullanır.

3. Merhaba Kaydet `pom.xml` dosya.

## <a name="create-hello-mapreduce-application"></a>Merhaba MapReduce uygulaması oluşturma

1. Toohello Git `wordcountjava/src/main/java/org/apache/hadoop/examples` dizin ve yeniden adlandırma hello `App.java` çok dosya`WordCount.java`.

2. Açık hello `WordCount.java` dosyasını bir metin düzenleyicisinde ve hello içeriği metin aşağıdaki hello ile değiştirin:
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    Bildirim hello bir paket adı `org.apache.hadoop.examples` ve hello sınıfı adı `WordCount`. Merhaba MapReduce işi gönderdiğinizde bu adları kullanın.

3. Merhaba dosyasını kaydedin.

## <a name="build-hello-application"></a>Merhaba uygulaması oluşturma

1. Değiştirme toohello `wordcountjava` , zaten orada değilseniz dizin.

2. Toobuild bir JAR dosyasını içeren Merhaba uygulaması komutu aşağıdaki hello kullan:

   ```
   mvn clean package
   ```

    Bu komut önceki yapı yapıtların temizler, paket hello uygulama ve sonra yapılar ve zaten yüklü, bağımlılıkları indirir.

3. Merhaba komutu, hello tamamlandıktan sonra `wordcountjava/target` dizini içeren adlı bir dosya `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Merhaba `wordcountjava-1.0-SNAPSHOT.jar` dosyasıdır değil yalnızca hello WordCount iş içeren bir uberjar ancak iş hello bağımlılıkları çalışma zamanında de gerektirir.

## <a id="upload"></a>Merhaba jar karşıya yükle

Komut tooupload hello jar dosyasını toohello Hdınsight headnode aşağıdaki hello kullan:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Bu komut hello yerel sistem toohello baş düğümünden hello dosyalarını kopyalar. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Hadoop'ta Hello MapReduce işi çalıştırma

1. SSH kullanarak tooHDInsight bağlayın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Merhaba SSH oturumundan komutu toorun Merhaba MapReduce uygulaması aşağıdaki hello kullan:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Bu komut hello WordCount MapReduce uygulama başlatır. Merhaba giriş dosyası `/example/data/gutenberg/davinci.txt`, ve hello çıktı dizini `/example/data/wordcountout`. Merhaba giriş dosyası ve çıktı saklı toohello varsayılan depolama hello kümesi için ' dir.

3. Merhaba işi tamamlandıktan sonra komut tooview hello sonuçları aşağıdaki hello kullanın:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Sözcükler ve sayıları, bir liste değerleri benzer toohello metnini izleyen ile almanız gerekir:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Sonraki adımlar

Bu belgede, öğrendiğiniz nasıl toodevelop bir Java MapReduce işi. Hdınsight ile diğer yolları toowork belgeleri aşağıdaki hello bakın.

* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Daha fazla bilgi için hello Ayrıca bkz. [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

