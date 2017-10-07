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
# <a name="build-java-applications-for-apache-hbase"></a>Apache HBase için Java uygulamaları derleme

Bilgi nasıl toocreate bir [Apache HBase](http://hbase.apache.org/) Java uygulaması. Daha sonra Azure hdınsight'ta HBase ile Merhaba uygulaması kullanın.

Merhaba adımları bu belgenin kullanımı [Maven](http://maven.apache.org/) toocreate ve yapı hello projesi. Maven yazılım proje yönetimi ve, toobuild yazılım, belge ve Java projeleri için raporlar sağlar kavrama Aracı ' dir.

> [!NOTE]
> Merhaba bu belgedeki adımlar en son Hdınsight 3.6 sınanmıştır.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Gereksinimler

* [Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 veya üzeri.

    > [!NOTE]
    > Hdınsight 3.5 ve büyük Java 8 gerektirir. Hdınsight'ın önceki sürümlerini Java 7 gerektirir.

* [Maven](http://maven.apache.org/)

* [HBase ile Linux tabanlı Azure Hdınsight kümesi](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > Bu belgedeki Hello adımlar 3.4 ve 3.5 Hdınsight küme sürümleri ile test edilmiştir. örneklerde sağlanan hello varsayılan bir Hdınsight 3.5 küme için değerlerdir.

## <a name="create-hello-project"></a>Başlangıç projesi oluşturma

1. Merhaba komut satırından geliştirme ortamınızda toocreate hello proje, örneğin, dizinleri toohello konumu değiştirme `cd code\hbase`.

2. Kullanım hello **mvn** Maven toogenerate hello hello projesi için iskele ile yüklenen komutu.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > PowerShell kullanıyorsanız, hello almalısınız `-D` çift tırnak işareti parametreleri.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Bu komut, aynı ad hello hello ile bir dizin oluşturur. **Artifactıd** parametre (**hbaseapp** Bu örnekte.) Bu dizin hello aşağıdaki öğeleri içerir:

   * **pom.xml**: Proje nesne modeli hello ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) bilgilerini ve yapılandırma kullanılan ayrıntılarını toobuild hello projesi içerir.
   * **src**: hello içeren hello dizini **main/java/com/microsoft/örnekler** Yazar burada hello uygulama dizini.

3. Merhaba silme `src/test/java/com/microsoft/examples/apptest.java` dosya. Değil Bu örnekte, kullanılabilir.

## <a name="update-hello-project-object-model"></a>Güncelleştirme hello projesi nesne modeli

1. Merhaba Düzenle `pom.xml` dosya ve hello içindeki kodu aşağıdaki hello ekleyin `<dependencies>` bölümü:

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

    Bu bölümde hello proje gerektiğini gösterir **hbase istemci** ve **phoenix çekirdek** bileşenleri. Derleme zamanında hello varsayılan Maven depodan bu bağımlılıkları indirilir. Merhaba kullanabilirsiniz [Maven merkezi deposu arama](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn bu bağımlılığı hakkında daha fazla bilgi.

   > [!IMPORTANT]
   > Merhaba hbase-istemci Hello sürüm numarasını Hdınsight kümenizle sağlanan HBase hello sürümü aynı olmalıdır. Aşağıdaki tabloda toofind hello doğru sürüm numarası hello kullanın.

   | Hdınsight küme sürümü | HBase sürüm toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 ve 3.6 |1.1.2 |

    Hdınsight sürümleri ve bileşenleri hakkında daha fazla bilgi için bkz: [hello farklı Hadoop bileşenleri Hdınsight ile kullanılabilir nelerdir](hdinsight-component-versioning.md).

3. Aşağıdaki kodu toohello hello eklemek **pom.xml** dosya. Bu metin hello içinde olmalıdır `<project>...</project>` hello etiketlerinde dosya, örneğin, arasında `</dependencies>` ve `</project>`.

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

    Bu bölümde bir kaynak yapılandırır (`conf/hbase-site.xml`) HBase için yapılandırma bilgilerini içerir.

   > [!NOTE]
   > Kod aracılığıyla yapılandırma değerlerini de ayarlayabilirsiniz. Merhaba Hello açıklamaları görmek `CreateTable` örnek.

    Bu bölümde ayrıca hello yapılandırır [Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/) ve [Maven gölge eklentisi](http://maven.apache.org/plugins/maven-shade-plugin/). Merhaba derleyici eklenti kullanılan toocompile hello topolojidir. Merhaba gölge eklenti kullanılan tooprevent lisans çoğaltma Maven tarafından oluşturulmuş hello JAR paketinde ' dir. Bu eklenti kullanılan tooprevent bir "yinelenen lisans dosyaları" Merhaba Hdınsight kümesi üzerinde çalışma zamanında hatasıdır. Maven gölge eklentisi ile hello kullanarak `ApacheLicenseResourceTransformer` uygulama hello hata engeller.

    Merhaba maven gölge eklentisi ayrıca hello uygulama tarafından istenen tüm hello bağımlılıkları içeren bir uber jar üretir.

4. Merhaba Kaydet `pom.xml` dosya.

5. Adlı bir dizin oluşturun `conf` hello içinde `hbaseapp` dizin. TooHBase bağlanmak için kullanılan toohold yapılandırma bilgilerini dizindir.

6. Kullanım hello şu komutu toocopy hello HBase hello HBase kümesi toohello yapılandırmasından `conf` dizin. Değiştir `USERNAME` SSH oturumunuzla hello adı. Değiştir `CLUSTERNAME` Hdınsight küme adıyla:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Kullanma hakkında daha fazla bilgi için `ssh` ve `scp`, bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma

1. Toohello Git `hbaseapp/src/main/java/com/microsoft/examples` dizin ve yeniden adlandırma hello app.java dosyasını çok`CreateTable.java`.

2. Açık hello `CreateTable.java` dosya ve hello mevcut içeriklerini metin aşağıdaki hello ile değiştirin:

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

    Bu kodu hello **CreateTable** adlı bir tablo oluşturur sınıfı **kişiler** ve önceden tanımlanmış bazı kullanıcılar ile doldurabilirsiniz.

3. Merhaba Kaydet `CreateTable.java` dosya.

4. Merhaba, `hbaseapp/src/main/java/com/microsoft/examples` dizin adlı bir dosya oluşturun `SearchByEmail.java`. Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:

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

    Merhaba **SearchByEmail** sınıfı, e-posta adresine göre satırlar için kullanılan tooquery olabilir. Normal ifade filtresi kullandığından, hello sınıfı kullanırken bir dize veya normal bir ifade belirtebilirsiniz.

5. Merhaba Kaydet `SearchByEmail.java` dosya.

6. Merhaba, `hbaseapp/src/main/hava/com/microsoft/examples` dizin adlı bir dosya oluşturun `DeleteTable.java`. Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:

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

    Bu sınıf, devre dışı bırakarak bu örnekte oluşturulan HBase tabloları hello temizler ve hello tablo bırakma hello tarafından oluşturulan `CreateTable` sınıfı.

7. Merhaba Kaydet `DeleteTable.java` dosya.

## <a name="build-and-package-hello-application"></a>Derleme ve paket Merhaba uygulaması

1. Merhaba gelen `hbaseapp` dizin, kullanım hello şu komutu toobuild Merhaba uygulaması içeren JAR Dosyası:

    ```bash
    mvn clean package
    ```

    Bu komut oluşturur ve .jar dosyasına uygulama paketleri hello.

2. Merhaba komutu tamamlandığında, hello `hbaseapp/target` dizini içeren adlı bir dosya `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Merhaba `hbaseapp-1.0-SNAPSHOT.jar` uber jar bir dosyadır. Tüm hello bağımlılıkları gerekli toorun hello uygulama içerir.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Merhaba JAR karşıya yükleme ve işleri (SSH) çalıştırın

Aşağıdaki adımları kullan hello `scp` toocopy hello JAR toohello birincil baş düğümüne Hdınsight kümesinde, HBase. Merhaba `ssh` komuttur tooconnect toohello küme tarafından kullanılan ve hello örnek doğrudan hello baş düğümü üzerinde çalışacak.

1. tooupload hello jar toohello küme, komutu aşağıdaki kullanım hello:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Değiştir `USERNAME` SSH oturumunuzla hello adı. Değiştir `CLUSTERNAME` ile Hdınsight kümenizin adıdır.

2. tooconnect toohello HBase kümesi hello aşağıdaki komutu kullanın:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Değiştir `USERNAME` SSH oturumunuzla hello adı. Değiştir `CLUSTERNAME` ile Hdınsight kümenizin adıdır.

3. kullanarak bir HBase tablosu toocreate Java uygulaması, komutu aşağıdaki kullanım hello hello:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    Bu komut adlı bir HBase tablosu oluşturur **kişiler**ve verileri ile doldurur.

4. toosearch hello tabloda, komutu aşağıdaki kullanım hello depolanan e-posta adresleri için:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Sonuçları aşağıdaki hello alırsınız:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. toodelete hello tablo, komutu aşağıdaki kullanım hello:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Merhaba JAR karşıya yükleme ve işleri (PowerShell) çalıştırın

Aşağıdaki adımları hello Azure PowerShell tooupload hello JAR toohello varsayılan depolama HBase kümeniz için kullanın. Kullanılan toorun hello sonra örnekler uzaktan Hdınsight cmdlet'leri şunlardır.

1. Yükleme ve Azure PowerShell, yapılandırma oluşturduktan sonra adlı bir dosya `hbase-runner.psm1`. Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:

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

    Bu dosya iki modülleri içerir:

   * **Ekleme HDInsightFile** - kullanılan tooupload dosyaları toohello küme
   * **Başlangıç HBaseExample** -kullanılan daha önce oluşturduğunuz toorun hello sınıflar

2. Merhaba Kaydet `hbase-runner.psm1` dosya.

3. Yeni bir Azure PowerShell penceresi açın, dizinleri toohello değiştirmek `hbaseapp` dizin, ve ardından çalışma hello aşağıdaki komutu:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Merhaba yolu toohello hello konumunu değiştirme `hbase-runner.psm1` daha önce oluşturduğunuz dosya. Bu komut hello modülü Azure PowerShell ile kaydeder.

4. Kullanım hello şu komutu tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour küme.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Değiştir `hdinsightclustername` kümenizin hello ada sahip. Merhaba komutu yükler hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` hello kümeniz için birincil depolama konumu.

5. bir tabloyu kullanarak toocreate hello `hbaseapp`, komutu aşağıdaki hello kullanın:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Değiştir `hdinsightclustername` kümenizin hello ada sahip.

    Bu komut adlı bir tablo oluşturur **kişiler** HBase Hdınsight kümenizdeki içinde. Bu komut, hello konsol penceresinde herhangi bir çıktı göstermez.

6. toosearch hello tablosundaki kullanım hello komutu aşağıdaki girişleri için:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Değiştir `hdinsightclustername` kümenizin hello ada sahip.

    Bu komut, hello kullanır `SearchByEmail` hello burada toosearch herhangi bir satır için sınıf `contactinformation` sütun ailesi ve hello `email` sütun içerir hello dize `contoso.com`. Sonuçları aşağıdaki hello almanız gerekir:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Kullanarak **fabrikam.com** hello için `-emailRegex` değeri döndürür hello kullanıcıların **fabrikam.com** hello e-posta alanında. Merhaba arama terimi olarak normal ifadeler de kullanabilirsiniz. Örneğin, **^ r** döndürür, 'r' hello harfle başlayan adreslerini e-posta.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Hiçbir sonuçları veya başlangıç HBaseExample kullanırken beklenmeyen sonuçlar

Kullanım hello `-showErr` parametresi tooview hello standart çalışan hello işi sırasında üretilen hata (STDERR).

## <a name="delete-hello-table"></a>Merhaba tablo silme

Merhaba örnekle bittiğinde toodelete hello aşağıdaki hello kullanmak **kişiler** Bu örnekte kullanılan tablo:

__Gelen bir `ssh` oturum__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Azure PowerShell üzerinden__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Sonraki adımlar

[Bilgi nasıl toouse SQuirreL SQL HBase ile](hdinsight-hbase-phoenix-squirrel-linux.md)
