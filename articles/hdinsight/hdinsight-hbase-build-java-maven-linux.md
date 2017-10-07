---
title: "aaaJava HBase istemci - Azure Hdınsight | Microsoft Docs"
description: "Bilgi nasıl toouse Apache Maven toobuild Java tabanlı Apache HBase uygulama, dağıtmanıza, Azure hdınsight'ta tooHBase."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="41210-103">Apache HBase için Java uygulamaları derleme</span><span class="sxs-lookup"><span data-stu-id="41210-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="41210-104">Bilgi nasıl toocreate bir [Apache HBase](http://hbase.apache.org/) Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="41210-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="41210-105">Daha sonra Azure hdınsight'ta HBase ile Merhaba uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="41210-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="41210-106">Merhaba adımları bu belgenin kullanımı [Maven](http://maven.apache.org/) toocreate ve yapı hello projesi.</span><span class="sxs-lookup"><span data-stu-id="41210-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="41210-107">Maven yazılım proje yönetimi ve, toobuild yazılım, belge ve Java projeleri için raporlar sağlar kavrama Aracı ' dir.</span><span class="sxs-lookup"><span data-stu-id="41210-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="41210-108">Merhaba bu belgedeki adımlar en son Hdınsight 3.6 sınanmıştır.</span><span class="sxs-lookup"><span data-stu-id="41210-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41210-109">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41210-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="41210-110">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="41210-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="41210-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="41210-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="41210-112">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="41210-112">Requirements</span></span>

* <span data-ttu-id="41210-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="41210-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="41210-114">Hdınsight 3.5 ve büyük Java 8 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41210-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="41210-115">Hdınsight'ın önceki sürümlerini Java 7 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41210-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="41210-116">Maven</span><span class="sxs-lookup"><span data-stu-id="41210-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="41210-117">HBase ile Linux tabanlı Azure Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="41210-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="41210-118">Bu belgedeki Hello adımlar 3.4 ve 3.5 Hdınsight küme sürümleri ile test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="41210-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="41210-119">örneklerde sağlanan hello varsayılan bir Hdınsight 3.5 küme için değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="41210-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="41210-120">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="41210-120">Create hello project</span></span>

1. <span data-ttu-id="41210-121">Merhaba komut satırından geliştirme ortamınızda toocreate hello proje, örneğin, dizinleri toohello konumu değiştirme `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="41210-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="41210-122">Kullanım hello **mvn** Maven toogenerate hello hello projesi için iskele ile yüklenen komutu.</span><span class="sxs-lookup"><span data-stu-id="41210-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="41210-123">PowerShell kullanıyorsanız, hello almalısınız `-D` çift tırnak işareti parametreleri.</span><span class="sxs-lookup"><span data-stu-id="41210-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="41210-124">Bu komut, aynı ad hello hello ile bir dizin oluşturur. **Artifactıd** parametre (**hbaseapp** Bu örnekte.) Bu dizin hello aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="41210-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="41210-125">**pom.xml**: Proje nesne modeli hello ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) bilgilerini ve yapılandırma kullanılan ayrıntılarını toobuild hello projesi içerir.</span><span class="sxs-lookup"><span data-stu-id="41210-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="41210-126">**src**: hello içeren hello dizini **main/java/com/microsoft/örnekler** Yazar burada hello uygulama dizini.</span><span class="sxs-lookup"><span data-stu-id="41210-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="41210-127">Merhaba silme `src/test/java/com/microsoft/examples/apptest.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="41210-128">Değil Bu örnekte, kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="41210-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="41210-129">Güncelleştirme hello projesi nesne modeli</span><span class="sxs-lookup"><span data-stu-id="41210-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="41210-130">Merhaba Düzenle `pom.xml` dosya ve hello içindeki kodu aşağıdaki hello ekleyin `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="41210-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="41210-131">Bu bölümde hello proje gerektiğini gösterir **hbase istemci** ve **phoenix çekirdek** bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="41210-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="41210-132">Derleme zamanında hello varsayılan Maven depodan bu bağımlılıkları indirilir.</span><span class="sxs-lookup"><span data-stu-id="41210-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="41210-133">Merhaba kullanabilirsiniz [Maven merkezi deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn bu bağımlılığı hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="41210-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="41210-134">Merhaba hbase-istemci Hello sürüm numarasını Hdınsight kümenizle sağlanan HBase hello sürümü aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="41210-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="41210-135">Aşağıdaki tabloda toofind hello doğru sürüm numarası hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="41210-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="41210-136">Hdınsight küme sürümü</span><span class="sxs-lookup"><span data-stu-id="41210-136">HDInsight cluster version</span></span> | <span data-ttu-id="41210-137">HBase sürüm toouse</span><span class="sxs-lookup"><span data-stu-id="41210-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="41210-138">3.2</span><span class="sxs-lookup"><span data-stu-id="41210-138">3.2</span></span> |<span data-ttu-id="41210-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="41210-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="41210-140">3.3, 3.4, 3.5 ve 3.6</span><span class="sxs-lookup"><span data-stu-id="41210-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="41210-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="41210-141">1.1.2</span></span> |

    <span data-ttu-id="41210-142">Hdınsight sürümleri ve bileşenleri hakkında daha fazla bilgi için bkz: [hello farklı Hadoop bileşenleri Hdınsight ile kullanılabilir nelerdir](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="41210-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="41210-143">Aşağıdaki kodu toohello hello eklemek **pom.xml** dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="41210-144">Bu metin hello içinde olmalıdır `<project>...</project>` hello etiketlerinde dosya, örneğin, arasında `</dependencies>` ve `</project>`.</span><span class="sxs-lookup"><span data-stu-id="41210-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
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
        </plugins>
    </build>
   ```

    <span data-ttu-id="41210-145">Bu bölümde bir kaynak yapılandırır (`conf/hbase-site.xml`) HBase için yapılandırma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="41210-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41210-146">Kod aracılığıyla yapılandırma değerlerini de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41210-146">You can also set configuration values via code.</span></span> <span data-ttu-id="41210-147">Merhaba Hello açıklamaları görmek `CreateTable` örnek.</span><span class="sxs-lookup"><span data-stu-id="41210-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="41210-148">Bu bölümde ayrıca hello yapılandırır [Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/) ve [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="41210-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="41210-149">Merhaba derleyici eklenti kullanılan toocompile hello topolojidir.</span><span class="sxs-lookup"><span data-stu-id="41210-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="41210-150">Merhaba gölge eklenti kullanılan tooprevent lisans çoğaltma Maven tarafından oluşturulmuş hello JAR paketinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="41210-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="41210-151">Bu eklenti kullanılan tooprevent bir "yinelenen lisans dosyaları" Merhaba Hdınsight kümesi üzerinde çalışma zamanında hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="41210-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="41210-152">Maven gölge eklentisi ile hello kullanarak `ApacheLicenseResourceTransformer` uygulama hello hata engeller.</span><span class="sxs-lookup"><span data-stu-id="41210-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="41210-153">Merhaba maven gölge eklentisi ayrıca hello uygulama tarafından istenen tüm hello bağımlılıkları içeren bir uber jar üretir.</span><span class="sxs-lookup"><span data-stu-id="41210-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="41210-154">Merhaba Kaydet `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="41210-155">Adlı bir dizin oluşturun `conf` hello içinde `hbaseapp` dizin.</span><span class="sxs-lookup"><span data-stu-id="41210-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="41210-156">TooHBase bağlanmak için kullanılan toohold yapılandırma bilgilerini dizindir.</span><span class="sxs-lookup"><span data-stu-id="41210-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="41210-157">Kullanım hello şu komutu toocopy hello HBase hello HBase kümesi toohello yapılandırmasından `conf` dizin.</span><span class="sxs-lookup"><span data-stu-id="41210-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="41210-158">Değiştir `USERNAME` SSH oturumunuzla hello adı.</span><span class="sxs-lookup"><span data-stu-id="41210-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="41210-159">Değiştir `CLUSTERNAME` Hdınsight küme adıyla:</span><span class="sxs-lookup"><span data-stu-id="41210-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="41210-160">Kullanma hakkında daha fazla bilgi için `ssh` ve `scp`, bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="41210-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="41210-161">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="41210-161">Create hello application</span></span>

1. <span data-ttu-id="41210-162">Toohello Git `hbaseapp/src/main/java/com/microsoft/examples` dizin ve yeniden adlandırma hello app.java dosyasını çok`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="41210-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="41210-163">Açık hello `CreateTable.java` dosya ve hello mevcut içeriklerini metin aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="41210-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="41210-164">Bu kodu hello **CreateTable** adlı bir tablo oluşturur sınıfı **kişiler** ve önceden tanımlanmış bazı kullanıcılar ile doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41210-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="41210-165">Merhaba Kaydet `CreateTable.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="41210-166">Merhaba, `hbaseapp/src/main/java/com/microsoft/examples` dizin adlı bir dosya oluşturun `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="41210-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="41210-167">Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41210-167">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="41210-168">Merhaba **SearchByEmail** sınıfı, e-posta adresine göre satırlar için kullanılan tooquery olabilir.</span><span class="sxs-lookup"><span data-stu-id="41210-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="41210-169">Normal ifade filtresi kullandığından, hello sınıfı kullanırken bir dize veya normal bir ifade belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41210-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="41210-170">Merhaba Kaydet `SearchByEmail.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="41210-171">Merhaba, `hbaseapp/src/main/hava/com/microsoft/examples` dizin adlı bir dosya oluşturun `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="41210-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="41210-172">Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41210-172">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="41210-173">Bu sınıf, devre dışı bırakarak bu örnekte oluşturulan HBase tabloları hello temizler ve hello tablo bırakma hello tarafından oluşturulan `CreateTable` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="41210-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="41210-174">Merhaba Kaydet `DeleteTable.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="41210-175">Derleme ve paket Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="41210-175">Build and package hello application</span></span>

1. <span data-ttu-id="41210-176">Merhaba gelen `hbaseapp` dizin, kullanım hello şu komutu toobuild Merhaba uygulaması içeren JAR Dosyası:</span><span class="sxs-lookup"><span data-stu-id="41210-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="41210-177">Bu komut oluşturur ve .jar dosyasına uygulama paketleri hello.</span><span class="sxs-lookup"><span data-stu-id="41210-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="41210-178">Merhaba komutu tamamlandığında, hello `hbaseapp/target` dizini içeren adlı bir dosya `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="41210-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41210-179">Merhaba `hbaseapp-1.0-SNAPSHOT.jar` uber jar bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="41210-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="41210-180">Tüm hello bağımlılıkları gerekli toorun hello uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="41210-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="41210-181">Merhaba JAR karşıya yükleme ve işleri (SSH) çalıştırın</span><span class="sxs-lookup"><span data-stu-id="41210-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="41210-182">Aşağıdaki adımları kullan hello `scp` toocopy hello JAR toohello birincil baş düğümüne Hdınsight kümesinde, HBase.</span><span class="sxs-lookup"><span data-stu-id="41210-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="41210-183">Merhaba `ssh` komuttur tooconnect toohello küme tarafından kullanılan ve hello örnek doğrudan hello baş düğümü üzerinde çalışacak.</span><span class="sxs-lookup"><span data-stu-id="41210-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="41210-184">tooupload hello jar toohello küme, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="41210-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="41210-185">Değiştir `USERNAME` SSH oturumunuzla hello adı.</span><span class="sxs-lookup"><span data-stu-id="41210-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="41210-186">Değiştir `CLUSTERNAME` ile Hdınsight kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="41210-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="41210-187">tooconnect toohello HBase kümesi hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="41210-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="41210-188">Değiştir `USERNAME` SSH oturumunuzla hello adı.</span><span class="sxs-lookup"><span data-stu-id="41210-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="41210-189">Değiştir `CLUSTERNAME` ile Hdınsight kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="41210-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="41210-190">kullanarak bir HBase tablosu toocreate Java uygulaması, komutu aşağıdaki kullanım hello hello:</span><span class="sxs-lookup"><span data-stu-id="41210-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="41210-191">Bu komut adlı bir HBase tablosu oluşturur **kişiler**ve verileri ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="41210-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="41210-192">toosearch hello tabloda, komutu aşağıdaki kullanım hello depolanan e-posta adresleri için:</span><span class="sxs-lookup"><span data-stu-id="41210-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="41210-193">Sonuçları aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="41210-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="41210-194">toodelete hello tablo, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="41210-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="41210-195">Merhaba JAR karşıya yükleme ve işleri (PowerShell) çalıştırın</span><span class="sxs-lookup"><span data-stu-id="41210-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="41210-196">Aşağıdaki adımları hello Azure PowerShell tooupload hello JAR toohello varsayılan depolama HBase kümeniz için kullanın.</span><span class="sxs-lookup"><span data-stu-id="41210-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="41210-197">Kullanılan toorun hello sonra örnekler uzaktan Hdınsight cmdlet'leri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="41210-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="41210-198">Yükleme ve Azure PowerShell, yapılandırma oluşturduktan sonra adlı bir dosya `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="41210-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="41210-199">Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41210-199">Use hello following text as hello contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="41210-200">Bu dosya iki modülleri içerir:</span><span class="sxs-lookup"><span data-stu-id="41210-200">This file contains two modules:</span></span>

   * <span data-ttu-id="41210-201">**Ekleme HDInsightFile** - kullanılan tooupload dosyaları toohello küme</span><span class="sxs-lookup"><span data-stu-id="41210-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="41210-202">**Başlangıç HBaseExample** -kullanılan daha önce oluşturduğunuz toorun hello sınıflar</span><span class="sxs-lookup"><span data-stu-id="41210-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="41210-203">Merhaba Kaydet `hbase-runner.psm1` dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="41210-204">Yeni bir Azure PowerShell penceresi açın, dizinleri toohello değiştirmek `hbaseapp` dizin, ve ardından çalışma hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="41210-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="41210-205">Merhaba yolu toohello hello konumunu değiştirme `hbase-runner.psm1` daha önce oluşturduğunuz dosya.</span><span class="sxs-lookup"><span data-stu-id="41210-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="41210-206">Bu komut hello modülü Azure PowerShell ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="41210-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="41210-207">Kullanım hello şu komutu tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour küme.</span><span class="sxs-lookup"><span data-stu-id="41210-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="41210-208">Değiştir `hdinsightclustername` kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="41210-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="41210-209">Merhaba komutu yükler hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` hello kümeniz için birincil depolama konumu.</span><span class="sxs-lookup"><span data-stu-id="41210-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="41210-210">bir tabloyu kullanarak toocreate hello `hbaseapp`, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="41210-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="41210-211">Değiştir `hdinsightclustername` kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="41210-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="41210-212">Bu komut adlı bir tablo oluşturur **kişiler** HBase Hdınsight kümenizdeki içinde.</span><span class="sxs-lookup"><span data-stu-id="41210-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="41210-213">Bu komut, hello konsol penceresinde herhangi bir çıktı göstermez.</span><span class="sxs-lookup"><span data-stu-id="41210-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="41210-214">toosearch hello tablosundaki kullanım hello komutu aşağıdaki girişleri için:</span><span class="sxs-lookup"><span data-stu-id="41210-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="41210-215">Değiştir `hdinsightclustername` kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="41210-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="41210-216">Bu komut, hello kullanır `SearchByEmail` hello burada toosearch herhangi bir satır için sınıf `contactinformation` sütun ailesi ve hello `email` sütun içerir hello dize `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="41210-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="41210-217">Sonuçları aşağıdaki hello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="41210-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="41210-218">Kullanarak **fabrikam.com** hello için `-emailRegex` değeri döndürür hello kullanıcıların **fabrikam.com** hello e-posta alanında.</span><span class="sxs-lookup"><span data-stu-id="41210-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="41210-219">Merhaba arama terimi olarak normal ifadeler de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41210-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="41210-220">Örneğin, **^ r** döndürür, 'r' hello harfle başlayan adreslerini e-posta.</span><span class="sxs-lookup"><span data-stu-id="41210-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="41210-221">Hiçbir sonuçları veya başlangıç HBaseExample kullanırken beklenmeyen sonuçlar</span><span class="sxs-lookup"><span data-stu-id="41210-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="41210-222">Kullanım hello `-showErr` parametresi tooview hello standart çalışan hello işi sırasında üretilen hata (STDERR).</span><span class="sxs-lookup"><span data-stu-id="41210-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="41210-223">Merhaba tablo silme</span><span class="sxs-lookup"><span data-stu-id="41210-223">Delete hello table</span></span>

<span data-ttu-id="41210-224">Merhaba örnekle bittiğinde toodelete hello aşağıdaki hello kullanmak **kişiler** Bu örnekte kullanılan tablo:</span><span class="sxs-lookup"><span data-stu-id="41210-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="41210-225">__Gelen bir `ssh` oturum__:</span><span class="sxs-lookup"><span data-stu-id="41210-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="41210-226">__Azure PowerShell üzerinden__:</span><span class="sxs-lookup"><span data-stu-id="41210-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="41210-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41210-227">Next steps</span></span>

[<span data-ttu-id="41210-228">Bilgi nasıl toouse SQuirreL SQL HBase ile</span><span class="sxs-lookup"><span data-stu-id="41210-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
