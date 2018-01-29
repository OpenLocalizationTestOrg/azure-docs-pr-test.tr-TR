---
title: "Java MapReduce, Hadoop - Azure Hdınsight oluşturma | Microsoft Docs"
description: "Apache Maven bir Java tabanlı MapReduce uygulaması oluşturun, sonra Azure Hdınsight'ta Hadoop ile çalıştırmak için nasıl kullanılacağını öğrenin."
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
ms.date: 01/25/2018
ms.author: larryfr
ms.openlocfilehash: 16cb62c95784d7c8b284e03f0759028038af7f0a
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek

Apache Maven bir Java tabanlı MapReduce uygulaması oluşturun, sonra Azure Hdınsight'ta Hadoop ile çalıştırmak için nasıl kullanılacağını öğrenin.

> [!NOTE]
> Bu örnekte, en son Hdınsight 3.6 üzerinde test edilmiştir.

## <a name="prerequisites"></a>Önkoşullar

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 veya sonraki (veya eşdeğeri, OpenJDK gibi bir).
    
    > [!NOTE]
    > Hdınsight sürüm 3.4 ve önceki Java 7 kullanın. Hdınsight 3.5 ve büyük Java 8 kullanır.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Geliştirme ortamını yapılandırma

Java ve JDK yüklediğinizde aşağıdaki ortam değişkenleri ayarlayabilirsiniz. Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri içerdikleri denetlemeniz gerekir.

* `JAVA_HOME`-Java Çalışma zamanı ortamı (JRE) yüklü olduğu dizine işaret etmelidir. Örneğin, OS X, UNIX veya Linux bir sistemde, benzeri bir değer olmalıdır `/usr/lib/jvm/java-7-oracle`. Windows'da benzeri bir değer gerekir`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-aşağıdaki yolları içermelidir:
  
  * `JAVA_HOME`(veya eşdeğer yolu)

  * `JAVA_HOME\bin`(veya eşdeğer yolu)

  * Maven'ın yüklendiği dizin

## <a name="create-a-maven-project"></a>Bir Maven projesi oluşturun

1. Bir terminal oturumu veya geliştirme ortamınızı komut satırında, dizinleri, bu proje depolamak istediğiniz konuma değiştirin.

2. Kullanım `mvn` proje için askılamayı oluşturmak için Maven ile yüklü komutu.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > PowerShell kullanıyorsanız, almalısınız `-D` çift tırnak işareti parametreleri.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Bu komut tarafından belirtilen ada sahip bir dizin oluşturur `artifactID` parametre (**wordcountjava** Bu örnekte.) Bu dizin, aşağıdaki öğeleri içerir:

   * `pom.xml`- [Proje nesne modeli (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) Projeyi derlemek için kullanılan bilgileri ve yapılandırma ayrıntılarını içerir.

   * `src`-Uygulamayı içeren dizin.

3. Silme `src/test/java/org/apache/hadoop/examples/apptest.java` dosya. Bu örnekte kullanılmaz.

## <a name="add-dependencies"></a>Bağımlılıkları ekleyin.

1. Düzen `pom.xml` dosya ve aşağıdaki metni içine ekleyin `<dependencies>` bölümü:
   
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

    Bu gerekli kitaplıklar tanımlar (içinde listelenen &lt;Artifactıd\>) belirli bir sürümle (içinde listelenen &lt;sürüm\>). Derleme zamanında varsayılan Maven depodan bu bağımlılıkları indirilir. Kullanabileceğiniz [Maven deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) daha fazla bilgi görüntülemek için.
   
    `<scope>provided</scope>` Çalışma zamanında Hdınsight küme tarafından sağlanan Maven Bu bağımlılıklar uygulama ile paketlenmesi değil olduğunu bildirir.

    > [!IMPORTANT]
    > Kullanılan sürüm Hadoop kümenizde mevcut sürümüyle eşleşmelidir. Sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](../hdinsight-component-versioning.md) belge.

2. Aşağıdakileri ekleyin `pom.xml` dosya. Bu metin içinde olmalıdır `<project>...</project>` etiketleri dosya; Örneğin, arasında `</dependencies>` ve `</project>`.

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

    İlk eklentisi yapılandırır [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/), uygulama tarafından gerekli bağımlı içeren (bazen bir fatjar olarak da adlandırılır) bir uberjar oluşturmak için kullanılır. Ayrıca, bazı sistemlerde sorunlara yol açabilir jar paketin içinde lisansları yinelenmesini önler.

    İkinci eklentisi hedef Java sürümü yapılandırır.

    > [!NOTE]
    > Hdınsight 3.4 ve Java 7 önceki kullanın. Hdınsight 3.5 ve büyük Java 8 kullanır.

3. `pom.xml` dosyasını kaydedin.

## <a name="create-the-mapreduce-application"></a>MapReduce uygulaması oluşturma

1. Git `wordcountjava/src/main/java/org/apache/hadoop/examples` dizin ve yeniden adlandırma `App.java` dosyasını `WordCount.java`.

2. Açık `WordCount.java` dosyasını bir metin düzenleyicisinde açın ve içeriği aşağıdaki metinle değiştirin:
   
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
   
    Paket adı olduğuna dikkat edin `org.apache.hadoop.examples` ve sınıf adı `WordCount`. MapReduce işi gönderdiğinizde bu adları kullanın.

3. Dosyayı kaydedin.

## <a name="build-the-application"></a>Uygulama oluşturma

1. Dönüştür `wordcountjava` , zaten orada değilseniz dizin.

2. Uygulamayı içeren JAR dosyasını oluşturmak için aşağıdaki komutu kullanın:

   ```
   mvn clean package
   ```

    Bu komut, önceki yapı yapıtların temizler, paket uygulama ve sonra yapılar ve zaten yüklü, bağımlılıkları indirir.

3. Komut bittikten sonra `wordcountjava/target` dizini içeren adlı bir dosya `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > `wordcountjava-1.0-SNAPSHOT.jar` Yalnızca WordCount işi, aynı zamanda çalışma zamanında iş gerektiren bağımlılıklar içeren bir uberjar bir dosyadır.

## <a id="upload"></a>Jar karşıya yükle

Hdınsight headnode jar dosyasını karşıya yüklemek için aşağıdaki komutu kullanın:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

Bu komut dosyaları, yerel sistemden baş düğüme kopyalar. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](../hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Hadoop MapReduce işi çalıştırma

1. SSH kullanarak Hdınsight bağlayın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](../hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH oturumundan MapReduce uygulamayı çalıştırmak için aşağıdaki komutu kullanın:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Bu komut WordCount MapReduce uygulamayı başlatır. Giriş dosyası `/example/data/gutenberg/davinci.txt`, ve çıktı dizinine `/example/data/wordcountout`. Giriş dosyası ve çıktı için kümenin varsayılan depolama alanına depolanır.

3. İş tamamlandığında, sonuçları görüntülemek için aşağıdaki komutu kullanın:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Sözcükler ve sayılarıyla değerleri aşağıdakine benzer bir liste almanız gerekir:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Sonraki adımlar

Bu belgede, bir Java MapReduce işi geliştirmek öğrendiniz. Hdınsight ile çalışmak diğer yolları için aşağıdaki belgelere bakın.

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Daha fazla bilgi için Ayrıca bkz. [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]:hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]:apache-hadoop-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-power-query]:apache-hadoop-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

