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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="15bb3-103">Azure Event hubs'tan (Java) hdınsight'ta Storm işlem olayları</span><span class="sxs-lookup"><span data-stu-id="15bb3-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="15bb3-104">Bilgi nasıl toouse Azure Event Hubs Hdınsight üzerinde Storm ile.</span><span class="sxs-lookup"><span data-stu-id="15bb3-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="15bb3-105">Bu örnek, Azure Event Hubs Java tabanlı bileşenler tooread ve yazma verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="15bb3-106">Azure Event Hubs, Web siteleri, uygulamaları ve cihazları verilerini oldukça büyük miktardaki tooprocess sağlar.</span><span class="sxs-lookup"><span data-stu-id="15bb3-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="15bb3-107">Merhaba olay hub'ı spout kolay toouse kolaylaştırır Apache Storm Hdınsight tooanalyze üzerinde gerçek zamanlı bu verileri.</span><span class="sxs-lookup"><span data-stu-id="15bb3-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="15bb3-108">Olay hub'ları Cıvata hello kullanarak Storm veri tooEvent hub de yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15bb3-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15bb3-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="15bb3-109">Prerequisites</span></span>

* <span data-ttu-id="15bb3-110">Hdınsight küme sürümü 3.6 üzerinde Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="15bb3-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="15bb3-111">Daha fazla bilgi için bkz: [Hdınsight kümesinde Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="15bb3-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="15bb3-112">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="15bb3-113">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="15bb3-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="15bb3-114">Bir [Azure olay hub'ı](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="15bb3-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="15bb3-115">[Oracle Java Geliştirme Seti (JDK) sürüm 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) veya eşdeğer gibi [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="15bb3-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="15bb3-116">[Maven](https://maven.apache.org/download.cgi): Maven Java projeleri için bir proje derleme sistemidir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="15bb3-117">Bir metin düzenleyicisi veya tümleşik geliştirme ortamı (IDE).</span><span class="sxs-lookup"><span data-stu-id="15bb3-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="15bb3-118">Bu belgede ele Maven çalışmak için belirli işlevleri Düzenleyicisi veya IDE olabilir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="15bb3-119">Düzenleme ortamınızı hello özellikleri hakkında daha fazla bilgi için kullanmakta olduğunuz hello ürününün hello belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="15bb3-120">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="15bb3-120">An SSH client.</span></span> <span data-ttu-id="15bb3-121">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="15bb3-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="15bb3-122">Merhaba `ssh` ve `scp` komutları.</span><span class="sxs-lookup"><span data-stu-id="15bb3-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="15bb3-123">Kullanılan toocopy dosyaları toohello Hdınsight kümesi bunlar.</span><span class="sxs-lookup"><span data-stu-id="15bb3-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="15bb3-124">Windows, bunlar Bash Windows 10 aracılığıyla elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15bb3-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="15bb3-125">Anlama Merhaba örneği</span><span class="sxs-lookup"><span data-stu-id="15bb3-125">Understanding hello example</span></span>

<span data-ttu-id="15bb3-126">Merhaba [hdınsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) örnek, iki topoloji içerir:</span><span class="sxs-lookup"><span data-stu-id="15bb3-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="15bb3-127">Merhaba `resources/writer.yaml` topoloji rastgele veri tooan Azure olay hub'ı yazar.</span><span class="sxs-lookup"><span data-stu-id="15bb3-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="15bb3-128">Merhaba veri hello tarafından oluşturulan `DeviceSpout` bileşeni ve rastgele cihaz kimliği ve cihaz değer.</span><span class="sxs-lookup"><span data-stu-id="15bb3-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="15bb3-129">Bu nedenle dize kimliği ve bir sayısal değer yayar bazı donanım benzetimi.</span><span class="sxs-lookup"><span data-stu-id="15bb3-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="15bb3-130">Üç `resources/reader.yaml` topoloji okur olay hub'ı (Merhaba veri EventHubWriter tarafından yazılan) verileri hello JSON verilerini ayrıştırır ve ardından günlükleri hello `deviceId` ve `deviceValue` veri.</span><span class="sxs-lookup"><span data-stu-id="15bb3-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="15bb3-131">Veri Merhaba biçimlendirilmiş onu tooEvent Hub yazılmış ve ne zaman hello okuyucu tarafından okuma önce bir JSON belgesi olarak, JSON dışında ve diziler olarak ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="15bb3-132">Merhaba JSON biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="15bb3-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="15bb3-133">Proje yapılandırması</span><span class="sxs-lookup"><span data-stu-id="15bb3-133">Project configuration</span></span>

<span data-ttu-id="15bb3-134">Merhaba `POM.xml` dosyası bu bir Maven projesi için yapılandırma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="15bb3-135">Merhaba ilginç parça şunlardır:</span><span class="sxs-lookup"><span data-stu-id="15bb3-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="15bb3-136">Olay hub'ı bileşenleri</span><span class="sxs-lookup"><span data-stu-id="15bb3-136">Event Hub components</span></span>

<span data-ttu-id="15bb3-137">okuyan ve yazan tooAzure olay hub'ları hello bileşen hello bulunan [Hdınsight depo](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="15bb3-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="15bb3-138">Merhaba hello bölümlerde aşağıdaki `POM.xml` bu depodan yük hello bileşenleri dosya</span><span class="sxs-lookup"><span data-stu-id="15bb3-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="15bb3-139">Merhaba EventHubs Storm Spout bağımlılık</span><span class="sxs-lookup"><span data-stu-id="15bb3-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="15bb3-140">Bu xml hem spout Event hubs'dan okumak için hem de tooit yazmak için bir Cıvata içeren hello eventhubs paket için bağımlılık tanımlar.</span><span class="sxs-lookup"><span data-stu-id="15bb3-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="15bb3-141">Bu xml hello proje toogenerate çıktısı Hdınsight 3.5 veya daha yüksek kullanılan 8, Java için yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="15bb3-142">maven gölge eklentisi hello</span><span class="sxs-lookup"><span data-stu-id="15bb3-142">hello maven-shade-plugin</span></span>

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

<span data-ttu-id="15bb3-143">Bu xml hello çözüm toopackage hello çıktı uber jar yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="15bb3-144">Merhaba jar hello proje kodunu ve gerekli bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="15bb3-145">İçin de kullanılır:</span><span class="sxs-lookup"><span data-stu-id="15bb3-145">It is also used to:</span></span>

* <span data-ttu-id="15bb3-146">Merhaba bağımlılıklar için lisans dosyalarını yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="15bb3-147">Güvenlik/imzaları hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="15bb3-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="15bb3-148">Birden çok uygulamaları aynı hello olun arabirimi, tek bir giriş olarak birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="15bb3-149">Bu yapılandırma ayarları çalışma zamanı hataları engeller.</span><span class="sxs-lookup"><span data-stu-id="15bb3-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="15bb3-150">Topoloji tanımları</span><span class="sxs-lookup"><span data-stu-id="15bb3-150">Topology definitions</span></span>

<span data-ttu-id="15bb3-151">Bu örnek hello kullanır [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="15bb3-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="15bb3-152">Bu çerçeve YAML toodefine hello topolojileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="15bb3-153">Merhaba birincil avantajı, Java kod hello topolojisinde kodlama sabit olmayan ' dir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="15bb3-154">Merhaba tanımı YAML olduğundan, toorecompile her şeyi gerek kalmadan hello topoloji, göndermeden önce değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15bb3-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="15bb3-155">__Writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="15bb3-155">__writer.yaml__:</span></span>

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

<span data-ttu-id="15bb3-156">__Reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="15bb3-156">__reader.yaml__:</span></span>

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

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="15bb3-157">Olay hub'ı hakkında Hello topoloji söyleyin</span><span class="sxs-lookup"><span data-stu-id="15bb3-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="15bb3-158">Çalışma zamanında hello `dev.properties` kullanılan toopass hello olay hub'ı yapılandırma toohello topoloji bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="15bb3-159">Merhaba aşağıdaki hello varsayılan hello dosyasının içeriğini örnektir:</span><span class="sxs-lookup"><span data-stu-id="15bb3-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="15bb3-160">Ortam değişkenleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="15bb3-160">Configure environment variables</span></span>

<span data-ttu-id="15bb3-161">Geliştirme iş istasyonunuza Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="15bb3-162">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="15bb3-163">**JAVA_HOME** -hello Java Çalışma zamanı ortamı (JRE) yüklü olduğu toohello dizin işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="15bb3-164">Örneğin, bir UNIX veya Linux dağıtımlarında benzeri bir değer çok olması gereken`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="15bb3-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="15bb3-165">Windows'da onu benzeri bir değer çok gerekir`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="15bb3-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="15bb3-166">**YOL** -yolları aşağıdaki hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="15bb3-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="15bb3-167">**JAVA_HOME** (veya hello eşdeğer yolu)</span><span class="sxs-lookup"><span data-stu-id="15bb3-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="15bb3-168">**JAVA_HOME\bin** (veya hello eşdeğer yolu)</span><span class="sxs-lookup"><span data-stu-id="15bb3-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="15bb3-169">Maven'ın yüklendiği hello dizini</span><span class="sxs-lookup"><span data-stu-id="15bb3-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="15bb3-170">Olay hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="15bb3-170">Configure Event Hub</span></span>

<span data-ttu-id="15bb3-171">Bu örnek için hello veri kaynağı olay hub ' dir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="15bb3-172">Merhaba aşağıdaki adımları toocreate bir olay hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="15bb3-173">Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com)seçin **yeni** > **Service Bus** > **olay hub'ı**  >  **Özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="15bb3-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="15bb3-174">Merhaba üzerinde **yeni bir olay hub'ı eklemek** ekranında, girin bir **olay hub'ı adı**.</span><span class="sxs-lookup"><span data-stu-id="15bb3-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="15bb3-175">Select hello **bölge** toocreate Merhaba, hub ve ad alanı oluşturma veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="15bb3-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="15bb3-176">Son olarak, hello tıklatın **ok** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="15bb3-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![Sihirbaz sayfası 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="15bb3-178">Select hello aynı **konumu** Hdınsight sunucu tooreduce gecikme süresi ve maliyetleri üzerinde Storm'a olarak.</span><span class="sxs-lookup"><span data-stu-id="15bb3-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="15bb3-179">Merhaba üzerinde **Event Hub'ı yapılandırma** ekranında, hello girin **bölüm sayısı** ve **ileti bekletme** değerleri.</span><span class="sxs-lookup"><span data-stu-id="15bb3-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="15bb3-180">Bu örnekte, bir bölüm sayısı 10 ve 1 ileti bekletilmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="15bb3-181">Bu değer daha sonra gerektiğinden hello bölüm sayısı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-181">Note hello partition count because you need this value later.</span></span>

    ![Sihirbaz sayfası 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="15bb3-183">Merhaba olay hub'ı oluşturulan, select hello ad alanı sağlandıktan sonra seçin **olay hub'ları**ve ardından daha önce oluşturduğunuz hello olay hub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="15bb3-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="15bb3-184">Seçin **yapılandırma**, sonra aşağıdaki bilgilerle hello kullanarak iki yeni erişim ilkeleri oluşturun:</span><span class="sxs-lookup"><span data-stu-id="15bb3-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="15bb3-185">Ad</span><span class="sxs-lookup"><span data-stu-id="15bb3-185">Name</span></span></th><th><span data-ttu-id="15bb3-186">İzinler</span><span class="sxs-lookup"><span data-stu-id="15bb3-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="15bb3-187">Yazıcı</span><span class="sxs-lookup"><span data-stu-id="15bb3-187">Writer</span></span></td><td><span data-ttu-id="15bb3-188">Gönder</span><span class="sxs-lookup"><span data-stu-id="15bb3-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="15bb3-189">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="15bb3-189">Reader</span></span></td><td><span data-ttu-id="15bb3-190">Dinleme</span><span class="sxs-lookup"><span data-stu-id="15bb3-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="15bb3-191">Merhaba izinleri oluşturduktan sonra hello seçin **kaydetmek** hello sayfanın hello simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="15bb3-192">Bu paylaşılan erişim ilkeleri kullanılan tooread ve tooEvent Hub yazma.</span><span class="sxs-lookup"><span data-stu-id="15bb3-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![ilkeleri](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="15bb3-194">Merhaba ilkeleri kaydettikten sonra hello kullan **paylaşılan erişim anahtarı Oluşturucu** hello sayfası tooretrieve hello anahtarını hello hello sonundaki **yazan** ve **okuyucu** ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="15bb3-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="15bb3-195">Bu anahtarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="15bb3-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="15bb3-196">Karşıdan yükle ve Merhaba projeyi derleme</span><span class="sxs-lookup"><span data-stu-id="15bb3-196">Download and build hello project</span></span>

1. <span data-ttu-id="15bb3-197">Merhaba projeyi Github'dan indirin: [hdınsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="15bb3-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="15bb3-198">Zip arşivini olarak hello paketini indirin veya kullanmak [git](https://git-scm.com/) tooclone hello projesini yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="15bb3-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="15bb3-199">Merhaba değiştirme `dev.properties` olay Hub'ınız için hello yapılandırma dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="15bb3-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="15bb3-200">Toobuild ve paket hello proje aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15bb3-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="15bb3-201">Bu komut gerekli bağımlılıkları, derlemeleri, yükler ve ardından paketler proje hello.</span><span class="sxs-lookup"><span data-stu-id="15bb3-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="15bb3-202">Merhaba çıktı hello depolanan **/target** olarak dizin **EventHubExample 1.0 SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="15bb3-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="15bb3-203">Yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="15bb3-203">Test locally</span></span>

<span data-ttu-id="15bb3-204">Bu topolojileri yalnızca okuma ve tooEvent hub'ları yazma olduğundan, yerel olarak varsa, bunları test edebilirsiniz bir [Storm geliştirme ortamı](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="15bb3-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="15bb3-205">Aşağıdaki adımları toorun hello geliştirme ortamında yerel olarak hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15bb3-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="15bb3-206">Merhaba yazan çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="15bb3-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="15bb3-207">Merhaba okuyucu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="15bb3-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="15bb3-208">`--local`: Hello topoloji yerel modda (dağıtılmış olmayan) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="15bb3-209">`-R /writer.yaml`: Hello hello topoloji tanımı yük `resources` hello jar paketlenir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="15bb3-210">Merhaba topoloji hello yerel dosya sistemindeki bir dosyaya ise hello yolu tooit hello son parametre olarak bunun yerine belirtin.</span><span class="sxs-lookup"><span data-stu-id="15bb3-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="15bb3-211">`--filter dev.properties`: Kullanın Merhaba içeriğine `dev.properties` toofill hello topoloji tanımlarında hello değerleri.</span><span class="sxs-lookup"><span data-stu-id="15bb3-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="15bb3-212">Örneğin, `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="15bb3-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="15bb3-213">Çıktı oturum toohello yerel olarak çalıştırırken konsoludur.</span><span class="sxs-lookup"><span data-stu-id="15bb3-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="15bb3-214">Kullanım __Ctrl + C__ toostop hello topolojisi.</span><span class="sxs-lookup"><span data-stu-id="15bb3-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="15bb3-215">Merhaba topolojilerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="15bb3-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="15bb3-216">SCP toocopy hello jar paket tooyour Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="15bb3-217">Merhaba SSH kullanıcı kümeniz için kullanıcı adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="15bb3-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="15bb3-218">CLUSTERNAME hello Hdınsight kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="15bb3-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="15bb3-219">SSH hesabınız için parola kullandıysanız, istendiğinde tooenter hello parola olur.</span><span class="sxs-lookup"><span data-stu-id="15bb3-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="15bb3-220">Merhaba hesabıyla bir SSH anahtarı kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yol toohello anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="15bb3-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="15bb3-221">Örneğin, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="15bb3-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="15bb3-222">Bu komut hello dosya toohello giriş dizinine hello kümede SSH kullanıcı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="15bb3-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="15bb3-223">Merhaba dosya karşıya yükleme tamamlandıktan sonra SSH tooconnect toohello Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="15bb3-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="15bb3-224">Değiştir **kullanıcıadı** SSH oturumunuzla hello adı.</span><span class="sxs-lookup"><span data-stu-id="15bb3-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="15bb3-225">Değiştir **CLUSTERNAME** Hdınsight küme adıyla:</span><span class="sxs-lookup"><span data-stu-id="15bb3-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="15bb3-226">SSH hesabınız için parola kullandıysanız, istendiğinde tooenter hello parola olur.</span><span class="sxs-lookup"><span data-stu-id="15bb3-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="15bb3-227">Merhaba hesabıyla bir SSH anahtarı kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yol toohello anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="15bb3-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="15bb3-228">Merhaba aşağıdaki örnek yükler hello özel anahtarı `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="15bb3-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="15bb3-229">Komut toostart hello topolojileri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15bb3-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="15bb3-230">`--remote`: Hello topoloji toohello hello kümesindeki hello alt düğümlerinde başlatır Nimbus hizmet gönderir.</span><span class="sxs-lookup"><span data-stu-id="15bb3-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="15bb3-231">tooview hello günlüğe kaydedilen veri, Git toohttps://CLUSTERNAME.azurehdinsight.net/stormui, burada __CLUSTERNAME__ Hdınsight kümenize hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="15bb3-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="15bb3-232">Hello topolojileri seçin ve toohello bileşenleri ayrıntıya gidin.</span><span class="sxs-lookup"><span data-stu-id="15bb3-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="15bb3-233">Select hello __bağlantı noktası__ bileşen tooview örneği için girişi günlüğe bilgi.</span><span class="sxs-lookup"><span data-stu-id="15bb3-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="15bb3-234">Aşağıdaki komutları toostop hello topolojileri hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15bb3-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="15bb3-235">Kümenizi Sil</span><span class="sxs-lookup"><span data-stu-id="15bb3-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="15bb3-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15bb3-236">Next steps</span></span>

* [<span data-ttu-id="15bb3-237">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="15bb3-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
