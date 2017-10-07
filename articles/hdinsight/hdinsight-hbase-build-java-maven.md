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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Windows tabanlı Hdınsight (Hadoop) ile HBase kullanan Maven toobuild Java uygulamaları kullanın
Bilgi nasıl toocreate ve yapı bir [Apache HBase](http://hbase.apache.org/) Apache Maven kullanarak Java uygulaması. Daha sonra Azure Hdınsight (Hadoop) ile Merhaba uygulaması kullanın.

[Maven](http://maven.apache.org/) toobuild yazılım, belge ve Java projeleri için raporlar sağlayan bir yazılım proje yönetimi ve kavrama aracıdır. Bu makalede, bilgi nasıl toouse, toocreate oluşturur, sorgular ve bir HBase siler Azure Hdınsight kümesinde tablo bir temel Java uygulaması.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Windows kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Gereksinimler
* [Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 veya üzeri
* [Maven](http://maven.apache.org/)
* HBase ile Windows tabanlı Hdınsight kümesi

    > [!NOTE]
    > Bu belgedeki Hello adımlar Hdınsight kümesi sürüm 3.2 ve 3.3 ile test edilmiştir. örneklerde sağlanan hello varsayılan bir Hdınsight 3.3 küme için değerlerdir.

## <a name="create-hello-project"></a>Başlangıç projesi oluşturma
1. Merhaba komut satırından geliştirme ortamınızda toocreate hello proje, örneğin, dizinleri toohello konumu değiştirme `cd code\hdinsight`.
2. Kullanım hello **mvn** Maven toogenerate hello hello projesi için iskele ile yüklenen komutu.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Bu komut bir dizin hello tarafından belirtilen hello adıyla hello geçerli konumda oluşturur **Artifactıd** parametre (**hbaseapp** Bu örnekte.) Bu dizin hello aşağıdaki öğeleri içerir:

   * **pom.xml**: Proje nesne modeli hello ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) bilgilerini ve yapılandırma kullanılan ayrıntılarını toobuild hello projesi içerir.
   * **src**: hello içeren hello dizini **main\java\com\microsoft\examples** burada yazarın hello uygulama dizini.
3. Merhaba silme **src\test\java\com\microsoft\examples\apptest.java** Bu örnekte kullanılmadığı için dosya.

## <a name="update-hello-project-object-model"></a>Güncelleştirme hello projesi nesne modeli
1. Merhaba Düzenle **pom.xml** dosya ve hello içindeki kodu aşağıdaki hello ekleyin `<dependencies>` bölümü:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    Bu bölümde proje hello Maven gerektirir söyler **hbase istemci** sürüm **1.1.2**. Derleme zamanında bu bağımlılığı hello varsayılan Maven deposundan yüklenir. Merhaba kullanabilirsiniz [Maven merkezi deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn bu bağımlılığı hakkında daha fazla bilgi.

   > [!IMPORTANT]
   > Merhaba sürüm numarası Hdınsight kümenizle sağlanan HBase hello sürümü aynı olmalıdır. Aşağıdaki tabloda toofind hello doğru sürüm numarası hello kullanın.
   >
   >

   | Hdınsight küme sürümü | HBase sürüm toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Hdınsight sürümleri ve bileşenleri hakkında daha fazla bilgi için bkz: [hello farklı Hadoop bileşenleri Hdınsight ile kullanılabilir nelerdir](hdinsight-component-versioning.md).
2. Bir Hdınsight 3.3 kümesi kullanıyorsanız, toohello aşağıdaki hello da eklemelisiniz `<dependencies>` bölümü:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Bu bağımlılık Hbase sürümü tarafından kullanılan hello phoenix çekirdek bileşenlerini yükler 1.1.x.
3. Aşağıdaki kodu toohello hello eklemek **pom.xml** dosya. Bu bölümde hello içinde olmalıdır `<project>...</project>` hello etiketlerinde dosya, örneğin, arasında `</dependencies>` ve `</project>`.

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

    Merhaba `<resources>` bölüm kaynak yapılandırır (**conf\hbase-site.xml**) HBase için yapılandırma bilgilerini içerir.

   > [!NOTE]
   > Kod aracılığıyla yapılandırma değerlerini de ayarlayabilirsiniz. Merhaba Hello açıklamaları görmek **CreateTable** hakkında bilgi için aşağıdaki örnek toodo bu.
   >
   >

    Bu `<plugins>` bölüm yapılandırır hello [Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/) ve [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/). Merhaba derleyici eklenti kullanılan toocompile hello topolojidir. Merhaba gölge eklenti kullanılan tooprevent lisans çoğaltma Maven tarafından oluşturulmuş hello JAR paketinde ' dir. Bu kullanılır hello hello yinelenen lisans dosyaları hello Hdınsight kümesi üzerinde çalışma zamanında bir hataya neden nedenidir. Maven gölge eklentisi ile hello kullanarak `ApacheLicenseResourceTransformer` uygulama bu hatayı önler.

    Merhaba maven gölge eklentisi ayrıca bir uber jar (veya fat jar) üreten hello uygulama tarafından istenen tüm hello bağımlılıkları içerir.
4. Merhaba Kaydet **pom.xml** dosya.
5. Adlı yeni bir dizin oluşturun **conf** hello içinde **hbaseapp** dizini. Merhaba, **conf** dizin adlı bir dosya oluşturun **hbase-site.xml**. Merhaba aşağıdaki hello dosyasının Merhaba içeriğine kullanın:

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

    Bu dosya, Hdınsight kümesi için kullanılan tooload hello HBase yapılandırma olacaktır.

   > [!NOTE]
   > Bu en az hbase-site.xml bir dosyadır ve hello hello Hdınsight kümesi için tam minimum ayarları içerir.

6. Merhaba Kaydet **hbase-site.xml** dosya.

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
1. Toohello Git **hbaseapp\src\main\java\com\microsoft\examples** dizin ve yeniden adlandırma hello app.java dosyasını çok**CreateTable.java**.
2. Açık hello **CreateTable.java** dosya ve hello varolan içeriği koddan hello ile değiştirin:

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

    Merhaba budur **CreateTable** adlı bir tablo oluşturacaksınız sınıfı **kişiler** ve önceden tanımlanmış bazı kullanıcılar ile doldurabilirsiniz.
3. Merhaba Kaydet **CreateTable.java** dosya.
4. Merhaba, **hbaseapp\src\main\java\com\microsoft\examples** dizin adlı yeni bir dosya oluşturun **SearchByEmail.java**. Bu dosyanın içeriğini hello koddan hello kullan:

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

    Merhaba **SearchByEmail** sınıfı, e-posta adresine göre satırlar için kullanılan tooquery olabilir. Normal ifade filtresi kullandığından, hello sınıfı kullanırken bir dize veya normal bir ifade belirtebilirsiniz.
5. Merhaba Kaydet **SearchByEmail.java** dosya.
6. Merhaba, **hbaseapp\src\main\hava\com\microsoft\examples** dizin adlı yeni bir dosya oluşturun **DeleteTable.java**. Bu dosyanın içeriğini hello koddan hello kullan:

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

    Devre dışı bırakarak bu örnek temizleme işlemi için bu sınıf, ve hello tablo bırakma hello tarafından oluşturulan **CreateTable** sınıfı.
7. Merhaba Kaydet **DeleteTable.java** dosya.

## <a name="build-and-package-hello-application"></a>Derleme ve paket Merhaba uygulaması
1. Bir komut istemi açın ve dizinleri toohello değiştirme **hbaseapp** dizini.
2. Komut toobuild Merhaba uygulaması içeren JAR dosyasını aşağıdaki hello kullan:

        mvn clean package

    Bu önceki yapı yapıtların temizler, zaten yüklü tüm bağımlılıkları indirir, ardından oluşturur ve hello uygulama paketleri.
3. Merhaba komutu tamamlandığında, hello **hbaseapp\target** dizini içeren adlı bir dosya **hbaseapp 1.0 SNAPSHOT.jar**.

   > [!NOTE]
   > Merhaba **hbaseapp 1.0 SNAPSHOT.jar** dosyasıdır bir uber tüm hello bağımlılıkları içeren (fat jar de denir) jar toorun Merhaba uygulaması gereklidir.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Merhaba JAR dosyasını karşıya yükleyin ve bir işi Başlat
Birçok yolu tooupload bir dosya tooyour Hdınsight kümesi açıklandığı gibi vardır [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md). Merhaba aşağıdaki adımları Azure PowerShell kullanın.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Yükleme ve Azure PowerShell, yapılandırma oluşturduktan sonra adlı yeni bir dosya **hbase runner.psm1**. Bu dosyanın içeriğini hello Hello aşağıdakileri kullanın:

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

    Bu dosya iki modülleri içerir:

   * **Ekleme HDInsightFile** -tooupload dosyaları tooHDInsight kullanılan
   * **Başlangıç HBaseExample** -kullanılan daha önce oluşturduğunuz toorun hello sınıflar
2. Merhaba Kaydet **hbase runner.psm1** dosya.
3. Yeni bir Azure PowerShell penceresi açın, dizinleri toohello değiştirme **hbaseapp** dizin, ve ardından çalışma hello aşağıdaki komutu.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Merhaba yolu toohello hello konumunu değiştirme **hbase runner.psm1** daha önce oluşturduğunuz dosya. Bu, bu Azure PowerShell oturumu için hello modülü kaydeder.
4. Kullanım hello şu komutu tooupload hello **hbaseapp 1.0 SNAPSHOT.jar** tooyour Hdınsight kümesi.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Değiştir **hdinsightclustername** Hdınsight kümenize hello adı. Merhaba komutu yükler hello **hbaseapp 1.0 SNAPSHOT.jar** toohello **örnek/Kavanoz** Hdınsight kümenizin hello birincil depolama konumu.
5. Merhaba dosyalarını karşıya yükledikten sonra kullanım hello aşağıdaki hello kullanarak tablo toocreate kod **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.

    Bu komut adlı yeni bir tablo oluşturur **kişiler** Hdınsight kümenizdeki. Bu komut, hello konsol penceresinde herhangi bir çıktı göstermez.
6. toosearch hello tablosundaki kullanım hello komutu aşağıdaki girişleri için:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.

    Bu komut, hello kullanır **SearchByEmail** hello burada toosearch herhangi bir satır için sınıf **contactinformation** sütun ailesi ve hello **e-posta** sütun hello dize içerir **contoso.com**. Sonuçları aşağıdaki hello almanız gerekir:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Kullanarak **fabrikam.com** hello için `-emailRegex` değeri döndürür hello kullanıcıların **fabrikam.com** hello e-posta alanında. Bu arama normal ifade tabanlı filtre kullanarak uygulandığından da normal ifadeler gibi girebilirsiniz **^ r**, hello e-posta hello harf 'r' ile başladığı hangi döndürür girişleri.

## <a name="delete-hello-table"></a>Merhaba tablo silme
Hello örnekle tamamladığınızda, kullanım hello aşağıdaki hello Azure PowerShell oturumu toodelete hello komutu **kişiler** Bu örnekte kullanılan tablo:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Değiştir **hdinsightclustername** Hdınsight kümenize hello adı.

## <a name="troubleshooting"></a>Sorun giderme
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Hiçbir sonuçları veya başlangıç HBaseExample kullanırken beklenmeyen sonuçlar
Kullanım hello `-showErr` parametresi tooview hello standart çalışan hello işi sırasında üretilen hata (STDERR).
