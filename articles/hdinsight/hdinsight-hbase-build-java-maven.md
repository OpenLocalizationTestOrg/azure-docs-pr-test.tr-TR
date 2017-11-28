---
title: "Windows tabanlı Azure Hdınsight için Java HBase uygulama aaaBuild | Microsoft Docs"
description: "Bilgi nasıl toouse Apache Maven toobuild Java tabanlı Apache HBase uygulama dağıtırsınız bu tooa Windows tabanlı Azure Hdınsight kümesi."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="36253-103">Windows tabanlı Hdınsight (Hadoop) ile HBase kullanan Maven toobuild Java uygulamaları kullanın</span><span class="sxs-lookup"><span data-stu-id="36253-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="36253-104">Bilgi nasıl toocreate ve yapı bir [Apache HBase](http://hbase.apache.org/) Apache Maven kullanarak Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="36253-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="36253-105">Daha sonra Azure Hdınsight (Hadoop) ile Merhaba uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="36253-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="36253-106">[Maven](http://maven.apache.org/) toobuild yazılım, belge ve Java projeleri için raporlar sağlayan bir yazılım proje yönetimi ve kavrama aracıdır.</span><span class="sxs-lookup"><span data-stu-id="36253-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="36253-107">Bu makalede, bilgi nasıl toouse, toocreate oluşturur, sorgular ve bir HBase siler Azure Hdınsight kümesinde tablo bir temel Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="36253-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36253-108">Bu belgedeki Hello adımlar Windows kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="36253-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="36253-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="36253-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="36253-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="36253-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="36253-111">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="36253-111">Requirements</span></span>
* <span data-ttu-id="36253-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="36253-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="36253-113">Maven</span><span class="sxs-lookup"><span data-stu-id="36253-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="36253-114">HBase ile Windows tabanlı Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="36253-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="36253-115">Bu belgedeki Hello adımlar Hdınsight kümesi sürüm 3.2 ve 3.3 ile test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="36253-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="36253-116">örneklerde sağlanan hello varsayılan bir Hdınsight 3.3 küme için değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="36253-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="36253-117">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="36253-117">Create hello project</span></span>
1. <span data-ttu-id="36253-118">Merhaba komut satırından geliştirme ortamınızda toocreate hello proje, örneğin, dizinleri toohello konumu değiştirme `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="36253-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="36253-119">Kullanım hello **mvn** Maven toogenerate hello hello projesi için iskele ile yüklenen komutu.</span><span class="sxs-lookup"><span data-stu-id="36253-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="36253-120">Bu komut bir dizin hello tarafından belirtilen hello adıyla hello geçerli konumda oluşturur **Artifactıd** parametre (**hbaseapp** Bu örnekte.) Bu dizin hello aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="36253-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="36253-121">**pom.xml**: Proje nesne modeli hello ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) bilgilerini ve yapılandırma kullanılan ayrıntılarını toobuild hello projesi içerir.</span><span class="sxs-lookup"><span data-stu-id="36253-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="36253-122">**src**: hello içeren hello dizini **main\java\com\microsoft\examples** burada yazarın hello uygulama dizini.</span><span class="sxs-lookup"><span data-stu-id="36253-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="36253-123">Merhaba silme **src\test\java\com\microsoft\examples\apptest.java** Bu örnekte kullanılmadığı için dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="36253-124">Güncelleştirme hello projesi nesne modeli</span><span class="sxs-lookup"><span data-stu-id="36253-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="36253-125">Merhaba Düzenle **pom.xml** dosya ve hello içindeki kodu aşağıdaki hello ekleyin `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="36253-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="36253-126">Bu bölümde proje hello Maven gerektirir söyler **hbase istemci** sürüm **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="36253-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="36253-127">Derleme zamanında bu bağımlılığı hello varsayılan Maven deposundan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="36253-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="36253-128">Merhaba kullanabilirsiniz [Maven merkezi deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn bu bağımlılığı hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="36253-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="36253-129">Merhaba sürüm numarası Hdınsight kümenizle sağlanan HBase hello sürümü aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36253-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="36253-130">Aşağıdaki tabloda toofind hello doğru sürüm numarası hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="36253-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="36253-131">Hdınsight küme sürümü</span><span class="sxs-lookup"><span data-stu-id="36253-131">HDInsight cluster version</span></span> | <span data-ttu-id="36253-132">HBase sürüm toouse</span><span class="sxs-lookup"><span data-stu-id="36253-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="36253-133">3.2</span><span class="sxs-lookup"><span data-stu-id="36253-133">3.2</span></span> |<span data-ttu-id="36253-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="36253-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="36253-135">3.3</span><span class="sxs-lookup"><span data-stu-id="36253-135">3.3</span></span> |<span data-ttu-id="36253-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="36253-136">1.1.2</span></span> |

    <span data-ttu-id="36253-137">Hdınsight sürümleri ve bileşenleri hakkında daha fazla bilgi için bkz: [hello farklı Hadoop bileşenleri Hdınsight ile kullanılabilir nelerdir](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="36253-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="36253-138">Bir Hdınsight 3.3 kümesi kullanıyorsanız, toohello aşağıdaki hello da eklemelisiniz `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="36253-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="36253-139">Bu bağımlılık Hbase sürümü tarafından kullanılan hello phoenix çekirdek bileşenlerini yükler 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="36253-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="36253-140">Aşağıdaki kodu toohello hello eklemek **pom.xml** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="36253-141">Bu bölümde hello içinde olmalıdır `<project>...</project>` hello etiketlerinde dosya, örneğin, arasında `</dependencies>` ve `</project>`.</span><span class="sxs-lookup"><span data-stu-id="36253-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="36253-142">Merhaba `<resources>` bölüm kaynak yapılandırır (**conf\hbase-site.xml**) HBase için yapılandırma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="36253-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36253-143">Kod aracılığıyla yapılandırma değerlerini de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36253-143">You can also set configuration values via code.</span></span> <span data-ttu-id="36253-144">Merhaba Hello açıklamaları görmek **CreateTable** hakkında bilgi için aşağıdaki örnek toodo bu.</span><span class="sxs-lookup"><span data-stu-id="36253-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="36253-145">Bu `<plugins>` bölüm yapılandırır hello [Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/) ve [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="36253-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="36253-146">Merhaba derleyici eklenti kullanılan toocompile hello topolojidir.</span><span class="sxs-lookup"><span data-stu-id="36253-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="36253-147">Merhaba gölge eklenti kullanılan tooprevent lisans çoğaltma Maven tarafından oluşturulmuş hello JAR paketinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="36253-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="36253-148">Bu kullanılır hello hello yinelenen lisans dosyaları hello Hdınsight kümesi üzerinde çalışma zamanında bir hataya neden nedenidir.</span><span class="sxs-lookup"><span data-stu-id="36253-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="36253-149">Maven gölge eklentisi ile hello kullanarak `ApacheLicenseResourceTransformer` uygulama bu hatayı önler.</span><span class="sxs-lookup"><span data-stu-id="36253-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="36253-150">Merhaba maven gölge eklentisi ayrıca bir uber jar (veya fat jar) üreten hello uygulama tarafından istenen tüm hello bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="36253-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="36253-151">Merhaba Kaydet **pom.xml** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="36253-152">Adlı yeni bir dizin oluşturun **conf** hello içinde **hbaseapp** dizini.</span><span class="sxs-lookup"><span data-stu-id="36253-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="36253-153">Merhaba, **conf** dizin adlı bir dosya oluşturun **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="36253-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="36253-154">Merhaba aşağıdaki hello dosyasının Merhaba içeriğine kullanın:</span><span class="sxs-lookup"><span data-stu-id="36253-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="36253-155">Bu dosya, Hdınsight kümesi için kullanılan tooload hello HBase yapılandırma olacaktır.</span><span class="sxs-lookup"><span data-stu-id="36253-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36253-156">Bu en az hbase-site.xml bir dosyadır ve hello hello Hdınsight kümesi için tam minimum ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="36253-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="36253-157">Merhaba Kaydet **hbase-site.xml** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="36253-158">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="36253-158">Create hello application</span></span>
1. <span data-ttu-id="36253-159">Toohello Git **hbaseapp\src\main\java\com\microsoft\examples** dizin ve yeniden adlandırma hello app.java dosyasını çok**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="36253-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="36253-160">Açık hello **CreateTable.java** dosya ve hello varolan içeriği koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="36253-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="36253-161">Merhaba budur **CreateTable** adlı bir tablo oluşturacaksınız sınıfı **kişiler** ve önceden tanımlanmış bazı kullanıcılar ile doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36253-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="36253-162">Merhaba Kaydet **CreateTable.java** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="36253-163">Merhaba, **hbaseapp\src\main\java\com\microsoft\examples** dizin adlı yeni bir dosya oluşturun **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="36253-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="36253-164">Bu dosyanın içeriğini hello koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="36253-164">Use hello following code as hello contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="36253-165">Merhaba **SearchByEmail** sınıfı, e-posta adresine göre satırlar için kullanılan tooquery olabilir.</span><span class="sxs-lookup"><span data-stu-id="36253-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="36253-166">Normal ifade filtresi kullandığından, hello sınıfı kullanırken bir dize veya normal bir ifade belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36253-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="36253-167">Merhaba Kaydet **SearchByEmail.java** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="36253-168">Merhaba, **hbaseapp\src\main\hava\com\microsoft\examples** dizin adlı yeni bir dosya oluşturun **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="36253-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="36253-169">Bu dosyanın içeriğini hello koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="36253-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="36253-170">Devre dışı bırakarak bu örnek temizleme işlemi için bu sınıf, ve hello tablo bırakma hello tarafından oluşturulan **CreateTable** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="36253-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="36253-171">Merhaba Kaydet **DeleteTable.java** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="36253-172">Derleme ve paket Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="36253-172">Build and package hello application</span></span>
1. <span data-ttu-id="36253-173">Bir komut istemi açın ve dizinleri toohello değiştirme **hbaseapp** dizini.</span><span class="sxs-lookup"><span data-stu-id="36253-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="36253-174">Komut toobuild Merhaba uygulaması içeren JAR dosyasını aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="36253-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="36253-175">Bu önceki yapı yapıtların temizler, zaten yüklü tüm bağımlılıkları indirir, ardından oluşturur ve hello uygulama paketleri.</span><span class="sxs-lookup"><span data-stu-id="36253-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="36253-176">Merhaba komutu tamamlandığında, hello **hbaseapp\target** dizini içeren adlı bir dosya **hbaseapp 1.0 SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="36253-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36253-177">Merhaba **hbaseapp 1.0 SNAPSHOT.jar** dosyasıdır bir uber tüm hello bağımlılıkları içeren (fat jar de denir) jar toorun Merhaba uygulaması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="36253-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="36253-178">Merhaba JAR dosyasını karşıya yükleyin ve bir işi Başlat</span><span class="sxs-lookup"><span data-stu-id="36253-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="36253-179">Birçok yolu tooupload bir dosya tooyour Hdınsight kümesi açıklandığı gibi vardır [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="36253-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="36253-180">Merhaba aşağıdaki adımları Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="36253-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="36253-181">Yükleme ve Azure PowerShell, yapılandırma oluşturduktan sonra adlı yeni bir dosya **hbase runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="36253-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="36253-182">Bu dosyanın içeriğini hello Hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="36253-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="36253-183">Bu dosya iki modülleri içerir:</span><span class="sxs-lookup"><span data-stu-id="36253-183">This file contains two modules:</span></span>

   * <span data-ttu-id="36253-184">**Ekleme HDInsightFile** -tooupload dosyaları tooHDInsight kullanılan</span><span class="sxs-lookup"><span data-stu-id="36253-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="36253-185">**Başlangıç HBaseExample** -kullanılan daha önce oluşturduğunuz toorun hello sınıflar</span><span class="sxs-lookup"><span data-stu-id="36253-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="36253-186">Merhaba Kaydet **hbase runner.psm1** dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="36253-187">Yeni bir Azure PowerShell penceresi açın, dizinleri toohello değiştirme **hbaseapp** dizin, ve ardından çalışma hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="36253-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="36253-188">Merhaba yolu toohello hello konumunu değiştirme **hbase runner.psm1** daha önce oluşturduğunuz dosya.</span><span class="sxs-lookup"><span data-stu-id="36253-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="36253-189">Bu, bu Azure PowerShell oturumu için hello modülü kaydeder.</span><span class="sxs-lookup"><span data-stu-id="36253-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="36253-190">Kullanım hello şu komutu tooupload hello **hbaseapp 1.0 SNAPSHOT.jar** tooyour Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="36253-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="36253-191">Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="36253-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="36253-192">Merhaba komutu yükler hello **hbaseapp 1.0 SNAPSHOT.jar** toohello **örnek/Kavanoz** Hdınsight kümenizin hello birincil depolama konumu.</span><span class="sxs-lookup"><span data-stu-id="36253-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="36253-193">Merhaba dosyalarını karşıya yükledikten sonra kullanım hello aşağıdaki hello kullanarak tablo toocreate kod **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="36253-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="36253-194">Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="36253-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="36253-195">Bu komut adlı yeni bir tablo oluşturur **kişiler** Hdınsight kümenizdeki.</span><span class="sxs-lookup"><span data-stu-id="36253-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="36253-196">Bu komut, hello konsol penceresinde herhangi bir çıktı göstermez.</span><span class="sxs-lookup"><span data-stu-id="36253-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="36253-197">toosearch hello tablosundaki kullanım hello komutu aşağıdaki girişleri için:</span><span class="sxs-lookup"><span data-stu-id="36253-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="36253-198">Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="36253-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="36253-199">Bu komut, hello kullanır **SearchByEmail** hello burada toosearch herhangi bir satır için sınıf **contactinformation** sütun ailesi ve hello **e-posta** sütun hello dize içerir **contoso.com**. Sonuçları aşağıdaki hello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="36253-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="36253-200">Kullanarak **fabrikam.com** hello için `-emailRegex` değeri döndürür hello kullanıcıların **fabrikam.com** hello e-posta alanında.</span><span class="sxs-lookup"><span data-stu-id="36253-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="36253-201">Bu arama normal ifade tabanlı filtre kullanarak uygulandığından da normal ifadeler gibi girebilirsiniz **^ r**, hello e-posta hello harf 'r' ile başladığı hangi döndürür girişleri.</span><span class="sxs-lookup"><span data-stu-id="36253-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="36253-202">Merhaba tablo silme</span><span class="sxs-lookup"><span data-stu-id="36253-202">Delete hello table</span></span>
<span data-ttu-id="36253-203">Hello örnekle tamamladığınızda, kullanım hello aşağıdaki hello Azure PowerShell oturumu toodelete hello komutu **kişiler** Bu örnekte kullanılan tablo:</span><span class="sxs-lookup"><span data-stu-id="36253-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="36253-204">Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="36253-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="36253-205">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="36253-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="36253-206">Hiçbir sonuçları veya başlangıç HBaseExample kullanırken beklenmeyen sonuçlar</span><span class="sxs-lookup"><span data-stu-id="36253-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="36253-207">Kullanım hello `-showErr` parametresi tooview hello standart çalışan hello işi sırasında üretilen hata (STDERR).</span><span class="sxs-lookup"><span data-stu-id="36253-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
