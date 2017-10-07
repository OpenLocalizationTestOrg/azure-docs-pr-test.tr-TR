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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="e6b6a-103">Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek</span><span class="sxs-lookup"><span data-stu-id="e6b6a-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="e6b6a-104">Bilgi nasıl toouse Apache Maven toocreate Java tabanlı MapReduce uygulama çalıştırın Hadoop ile Azure Hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="e6b6a-105">Bu örnekte, en son Hdınsight 3.6 üzerinde test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="e6b6a-106"><a name="prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e6b6a-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="e6b6a-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 veya sonraki (veya eşdeğeri, OpenJDK gibi bir).</span><span class="sxs-lookup"><span data-stu-id="e6b6a-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e6b6a-108">Hdınsight sürüm 3.4 ve önceki Java 7 kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="e6b6a-109">Hdınsight 3.5 ve büyük Java 8 kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="e6b6a-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="e6b6a-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="e6b6a-111">Geliştirme ortamını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e6b6a-111">Configure development environment</span></span>

<span data-ttu-id="e6b6a-112">Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="e6b6a-113">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="e6b6a-114">`JAVA_HOME`-hello Java Çalışma zamanı ortamı (JRE) yüklü olduğu toohello dizin işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="e6b6a-115">Örneğin, OS X, UNIX veya Linux bir sistemde, benzer bir değer çok olmalıdır`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="e6b6a-116">Windows'da onu benzeri bir değer çok gerekir`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="e6b6a-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="e6b6a-117">`PATH`-yolları aşağıdaki hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="e6b6a-118">`JAVA_HOME`(veya eşdeğer yolu hello)</span><span class="sxs-lookup"><span data-stu-id="e6b6a-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="e6b6a-119">`JAVA_HOME\bin`(veya eşdeğer yolu hello)</span><span class="sxs-lookup"><span data-stu-id="e6b6a-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="e6b6a-120">Maven'ın yüklendiği hello dizini</span><span class="sxs-lookup"><span data-stu-id="e6b6a-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="e6b6a-121">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="e6b6a-121">Create a Maven project</span></span>

1. <span data-ttu-id="e6b6a-122">Bir terminal oturumu veya komut satırından geliştirme ortamında, bu proje toostore istediğiniz dizinleri toohello konumunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="e6b6a-123">Kullanım hello `mvn` Maven toogenerate hello hello projesi için iskele ile yüklenen komutu.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="e6b6a-124">PowerShell kullanıyorsanız, hello almalısınız `-D` çift tırnak işareti parametreleri.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="e6b6a-125">Bu komut, hello tarafından belirtilen hello ada sahip bir dizin oluşturur. `artifactID` parametre (**wordcountjava** Bu örnekte.) Bu dizin hello aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="e6b6a-126">`pom.xml`-hello [proje nesne modeli (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) bilgileri içeren ve yapılandırma ayrıntılarını kullanılan toobuild hello projesi.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="e6b6a-127">`src`-Merhaba uygulaması içeren başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="e6b6a-128">Merhaba silme `src/test/java/org/apache/hadoop/examples/apptest.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="e6b6a-129">Bu örnekte kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="e6b6a-130">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-130">Add dependencies</span></span>

1. <span data-ttu-id="e6b6a-131">Merhaba Düzenle `pom.xml` dosya ve metin hello içinde aşağıdaki hello ekleyin `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="e6b6a-132">Bu gerekli kitaplıklar tanımlar (içinde listelenen &lt;Artifactıd\>) belirli bir sürümle (içinde listelenen &lt;sürüm\>).</span><span class="sxs-lookup"><span data-stu-id="e6b6a-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="e6b6a-133">Derleme zamanında hello varsayılan Maven depodan bu bağımlılıkları indirilir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="e6b6a-134">Merhaba kullanabilirsiniz [Maven deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview daha fazla.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="e6b6a-135">Merhaba `<scope>provided</scope>` hello Hdınsight kümesi çalışma zamanında tarafından sağlanan Maven Bu bağımlılıklar hello uygulamayla paketlenmesi değil olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e6b6a-136">kullanılan hello sürümü Hadoop kümenizde mevcut hello sürümüyle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="e6b6a-137">Merhaba sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="e6b6a-138">Toohello aşağıdaki hello eklemek `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="e6b6a-139">Bu metin hello içinde olmalıdır `<project>...</project>` etiketleri hello dosya; Örneğin, arasında `</dependencies>` ve `</project>`.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="e6b6a-140">Merhaba ilk eklentisi yapılandırır hello [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/), hangi kullanılan toobuild hello uygulama tarafından gerekli bağımlı içeren (bazen bir fatjar olarak da adlandırılır) bir uberjar değil.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="e6b6a-141">Ayrıca, bazı sistemlerde sorunlara yol açabilir hello jar paketin içinde lisansları yinelenmesini önler.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="e6b6a-142">Merhaba ikinci eklentisi hello hedef Java sürümü yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e6b6a-143">Hdınsight 3.4 ve Java 7 önceki kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="e6b6a-144">Hdınsight 3.5 ve büyük Java 8 kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="e6b6a-145">Merhaba Kaydet `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="e6b6a-146">Merhaba MapReduce uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6b6a-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="e6b6a-147">Toohello Git `wordcountjava/src/main/java/org/apache/hadoop/examples` dizin ve yeniden adlandırma hello `App.java` çok dosya`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="e6b6a-148">Açık hello `WordCount.java` dosyasını bir metin düzenleyicisinde ve hello içeriği metin aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="e6b6a-149">Bildirim hello bir paket adı `org.apache.hadoop.examples` ve hello sınıfı adı `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="e6b6a-150">Merhaba MapReduce işi gönderdiğinizde bu adları kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="e6b6a-151">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="e6b6a-152">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6b6a-152">Build hello application</span></span>

1. <span data-ttu-id="e6b6a-153">Değiştirme toohello `wordcountjava` , zaten orada değilseniz dizin.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="e6b6a-154">Toobuild bir JAR dosyasını içeren Merhaba uygulaması komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="e6b6a-155">Bu komut önceki yapı yapıtların temizler, paket hello uygulama ve sonra yapılar ve zaten yüklü, bağımlılıkları indirir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="e6b6a-156">Merhaba komutu, hello tamamlandıktan sonra `wordcountjava/target` dizini içeren adlı bir dosya `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e6b6a-157">Merhaba `wordcountjava-1.0-SNAPSHOT.jar` dosyasıdır değil yalnızca hello WordCount iş içeren bir uberjar ancak iş hello bağımlılıkları çalışma zamanında de gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="e6b6a-158"><a id="upload"></a>Merhaba jar karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e6b6a-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="e6b6a-159">Komut tooupload hello jar dosyasını toohello Hdınsight headnode aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="e6b6a-160">Bu komut hello yerel sistem toohello baş düğümünden hello dosyalarını kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="e6b6a-161">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e6b6a-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="e6b6a-162"><a name="run"></a>Hadoop'ta Hello MapReduce işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e6b6a-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="e6b6a-163">SSH kullanarak tooHDInsight bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="e6b6a-164">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e6b6a-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e6b6a-165">Merhaba SSH oturumundan komutu toorun Merhaba MapReduce uygulaması aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="e6b6a-166">Bu komut hello WordCount MapReduce uygulama başlatır.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="e6b6a-167">Merhaba giriş dosyası `/example/data/gutenberg/davinci.txt`, ve hello çıktı dizini `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="e6b6a-168">Merhaba giriş dosyası ve çıktı saklı toohello varsayılan depolama hello kümesi için ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="e6b6a-169">Merhaba işi tamamlandıktan sonra komut tooview hello sonuçları aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="e6b6a-170">Sözcükler ve sayıları, bir liste değerleri benzer toohello metnini izleyen ile almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6b6a-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="e6b6a-171"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6b6a-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e6b6a-172">Bu belgede, öğrendiğiniz nasıl toodevelop bir Java MapReduce işi.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="e6b6a-173">Hdınsight ile diğer yolları toowork belgeleri aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e6b6a-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="e6b6a-174">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e6b6a-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e6b6a-175">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e6b6a-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="e6b6a-176">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="e6b6a-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="e6b6a-177">Daha fazla bilgi için hello Ayrıca bkz. [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="e6b6a-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

