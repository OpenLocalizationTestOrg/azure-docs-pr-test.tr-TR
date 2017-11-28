---
title: "aaaJava kullanıcı tanımlı işlev (UDF hdınsight'ta - Azure Hive ile) | Microsoft Docs"
description: "Öğrenin nasıl toocreate Java tabanlı kullanıcı tanımlı işlev (UDF), Hive ile çalışır. Bu örnek UDF metin dizelerini toolowercase tablosu dönüştürür."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="d721e-104">Bir Java kullanma UDF hdınsight'ta Hive ile</span><span class="sxs-lookup"><span data-stu-id="d721e-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="d721e-105">Öğrenin nasıl toocreate Java tabanlı kullanıcı tanımlı işlev (UDF), Hive ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="d721e-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="d721e-106">Bu örnekte Hello Java UDF metin dizelerini tooall küçük karakterden oluşan bir tablo dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d721e-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="d721e-107">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="d721e-107">Requirements</span></span>

* <span data-ttu-id="d721e-108">Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="d721e-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="d721e-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="d721e-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d721e-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d721e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="d721e-111">Bu belgedeki çoğu adımlar her iki Windows ve Linux tabanlı kümelerde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d721e-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="d721e-112">Ancak, hello kullanılan adımları tooupload hello UDF toohello küme ve belirli tooLinux tabanlı kümeler olan Çalıştır derlenmiş.</span><span class="sxs-lookup"><span data-stu-id="d721e-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="d721e-113">Windows tabanlı kümeler ile kullanılabilir tooinformation bağlantılar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d721e-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="d721e-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 veya sonraki (veya eşdeğeri, OpenJDK gibi bir)</span><span class="sxs-lookup"><span data-stu-id="d721e-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="d721e-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="d721e-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="d721e-116">Bir metin düzenleyicisi veya Java IDE</span><span class="sxs-lookup"><span data-stu-id="d721e-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d721e-117">Windows İstemcisi Python dosyalarda hello oluşturursanız, LF satır bitiş olarak kullanan bir Düzenleyicisi'ni kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d721e-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="d721e-118">Merhaba düzenleyicinizi LF veya CRLF kullanıp kullanmadığını emin değilseniz bkz [sorun giderme](#troubleshooting) CR karakteri kaldırma adımları hello için bölüm.</span><span class="sxs-lookup"><span data-stu-id="d721e-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="d721e-119">Java UDF örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="d721e-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="d721e-120">Bir komut satırından toocreate yeni bir Maven projesi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d721e-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="d721e-121">PowerShell kullanıyorsanız, hello parametreleri tırnak konulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d721e-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="d721e-122">Örneğin, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="d721e-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="d721e-123">Bu komut adlı bir dizin oluşturur **exampleudf**, hello Maven projesine içerir.</span><span class="sxs-lookup"><span data-stu-id="d721e-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="d721e-124">Merhaba Proje oluşturulduktan sonra hello silme **exampleudf/src/test** hello projesinin bir parçası oluşturulan dizini.</span><span class="sxs-lookup"><span data-stu-id="d721e-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="d721e-125">Açık hello **exampleudf/pom.xml**ve hello varolan `<dependencies>` XML aşağıdaki hello girişle:</span><span class="sxs-lookup"><span data-stu-id="d721e-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="d721e-126">Bu girişler Hadoop ve Hdınsight 3.5 ile birlikte dahil Hive hello sürümünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="d721e-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="d721e-127">Hadoop ve Hdınsight ile hello sağlanan Hive hello sürümleri hakkında bilgi bulabilirsiniz [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.</span><span class="sxs-lookup"><span data-stu-id="d721e-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="d721e-128">Ekleme bir `<build>` hello önce bölümdeki `</project>` hello hello dosyasının sonuna satırında.</span><span class="sxs-lookup"><span data-stu-id="d721e-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="d721e-129">Bu bölümde, XML aşağıdaki hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="d721e-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="d721e-130">Bu girişler nasıl toobuild hello proje tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d721e-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="d721e-131">Özellikle, hello sürümü proje kullanır hello Java ve nasıl toobuild dağıtım toohello küme için bir uberjar.</span><span class="sxs-lookup"><span data-stu-id="d721e-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="d721e-132">Merhaba değişiklikler yapıldıktan sonra hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d721e-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="d721e-133">Yeniden Adlandır **exampleudf/src/main/java/com/microsoft/examples/App.java** çok**ExampleUDF.java**ve düzenleyicinizde hello dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d721e-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="d721e-134">Merhaba Hello içeriğini değiştirin **ExampleUDF.java** dosya hello aşağıdakilerle sonra hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d721e-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="d721e-135">Bu kod bir dize değeri kabul eder ve hello dizeyi küçük harfli sürümünü döndüren bir UDF uygular.</span><span class="sxs-lookup"><span data-stu-id="d721e-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="d721e-136">Derleme ve hello UDF yükleyin</span><span class="sxs-lookup"><span data-stu-id="d721e-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="d721e-137">Merhaba UDF paketini ve komut toocompile aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="d721e-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="d721e-138">Bu komut oluşturur ve paket hello UDF hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` dosya.</span><span class="sxs-lookup"><span data-stu-id="d721e-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="d721e-139">Kullanım hello `scp` komutu toocopy hello dosya toohello Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="d721e-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="d721e-140">Değiştir `myuser` hello kümeniz için SSH kullanıcı hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="d721e-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="d721e-141">Değiştir `mycluster` hello küme adı ile.</span><span class="sxs-lookup"><span data-stu-id="d721e-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="d721e-142">Bir parola toosecure hello SSH hesabı kullandıysanız, istendiğinde tooenter hello parola olur.</span><span class="sxs-lookup"><span data-stu-id="d721e-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="d721e-143">Bir sertifika kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello özel anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="d721e-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="d721e-144">SSH kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d721e-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d721e-145">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d721e-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="d721e-146">Merhaba SSH oturumundan hello jar dosyasını tooHDInsight depolama kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d721e-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="d721e-147">Merhaba UDF kovanından kullanın</span><span class="sxs-lookup"><span data-stu-id="d721e-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="d721e-148">Toostart hello Beeline istemci hello SSH oturumundan aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d721e-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="d721e-149">Bu komut hello varsayılan kullanılan varsayar **yönetici** hello oturum açma hesabı kümeniz için.</span><span class="sxs-lookup"><span data-stu-id="d721e-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="d721e-150">Hello gelmesini sonra `jdbc:hive2://localhost:10001/>` sor, tooadd hello UDF tooHive aşağıdaki hello girin ve bir işlevi olarak kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="d721e-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="d721e-151">Bu örnek, Azure Storage hello kümesi için varsayılan depolama olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d721e-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="d721e-152">Bunun yerine, küme Data Lake Store kullanıyorsa, hello değiştirmek `wasb:///` çok değer`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="d721e-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="d721e-153">Tablo toolower servis talebi dizelerden alınan hello UDF tooconvert değerlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d721e-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="d721e-154">Merhaba tablosundan cihaz Platformu (Android, Windows, iOS, vb.) seçer hello bu sorgu, hello dize toolower durumda dönüştürmek ve bunları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d721e-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="d721e-155">Merhaba çıktı metin aşağıdaki benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="d721e-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="d721e-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d721e-156">Next steps</span></span>

<span data-ttu-id="d721e-157">Hive ile diğer yolları toowork için bkz: [Hdınsight ile Hive kullanma](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="d721e-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="d721e-158">Hive User-Defined işlevler hakkında daha fazla bilgi için bkz: [Hive işleçler ve kullanıcı tanımlı işlevler](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) hello Hive wiki Apache.org bölümü.</span><span class="sxs-lookup"><span data-stu-id="d721e-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
