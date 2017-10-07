---
title: "aaaApache Storm yazma tooStorage/Data Lake Store - Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse hello Apache Storm toowrite toohello HDFS uyumlu depolama Hdınsight için öğrenin. Azure Storage veya Azure Data Lake Store, Hdınsight için hello HDFS comptabile depolama sağlar. Bu belge ve hello ilişkili örnek hello HdfsBolt bileşeni kullanılan toowrite toohello varsayılan Hdınsight kümesinde bir Storm depolanmasını nasıl olabilir göstermektedir."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="b6cb1-105">Hdınsight üzerinde Apache Storm tooHDFS yazma</span><span class="sxs-lookup"><span data-stu-id="b6cb1-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="b6cb1-106">Hdınsight üzerinde Apache Storm nasıl toouse Storm toowrite veri toohello HDFS uyumlu depolama kullandığı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="b6cb1-107">Hdınsight kullanma her ikisi de Azure depolama ve Azure Data Lake depolama HDFS comptabile depolama.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="b6cb1-108">Storm sağlayan bir [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) veri tooHDFS Yazar bileşeni.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="b6cb1-109">Bu belge, depolama tooeither türü HdfsBolt hello yazma konusunda bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b6cb1-110">Hdınsight üzerinde Storm ile dahil olan bileşenleri topoloji bu belgede kullanılan Merhaba örneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="b6cb1-111">Diğer Apache Storm kümeleri ile kullanıldığında Azure Data Lake Store ile değiştirilmesi toowork gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="b6cb1-112">Merhaba kod alın</span><span class="sxs-lookup"><span data-stu-id="b6cb1-112">Get hello code</span></span>

<span data-ttu-id="b6cb1-113">Bu topoloji içeren hello proje yükleme yoluyla kullanılabilir [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="b6cb1-114">toocompile bu proje için geliştirme ortamınızı yapılandırma aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="b6cb1-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="b6cb1-116">Java 8 Hdınsight 3.5 veya daha yükseğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="b6cb1-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="b6cb1-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="b6cb1-118">Geliştirme iş istasyonunuza Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="b6cb1-119">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="b6cb1-120">`JAVA_HOME`-hello JDK yüklendiği toohello dizin işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="b6cb1-121">`PATH`-yolları aşağıdaki hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="b6cb1-122">`JAVA_HOME`(veya eşdeğer yolu hello).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b6cb1-123">`JAVA_HOME\bin`(veya eşdeğer yolu hello).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b6cb1-124">Maven'ın yüklendiği başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="b6cb1-125">Nasıl toouse hello HdfsBolt Hdınsight ile</span><span class="sxs-lookup"><span data-stu-id="b6cb1-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6cb1-126">Hdınsight üzerinde Storm ile Merhaba HdfsBolt kullanmadan önce önce bir eylem gerekli toocopy jar betiklerinin hello kullanmanız gerekir `extpath` Storm için.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="b6cb1-127">Merhaba daha fazla bilgi için bkz: [yapılandırma hello küme](#configure) bölümü.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="b6cb1-128">Merhaba HdfsBolt toounderstand nasıl sağladığını hello dosyası şemasını kullanır toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="b6cb1-129">Hdınsight ile düzenleri aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="b6cb1-130">`wasb://`: Bir Azure depolama hesabıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="b6cb1-131">`adl://`: Azure Data Lake Store ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="b6cb1-132">Merhaba aşağıdaki tabloda farklı senaryolar için hello dosya düzeni kullanma örnekleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="b6cb1-133">Düzeni</span><span class="sxs-lookup"><span data-stu-id="b6cb1-133">Scheme</span></span> | <span data-ttu-id="b6cb1-134">Notlar</span><span class="sxs-lookup"><span data-stu-id="b6cb1-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="b6cb1-135">bir Azure depolama hesabı blob kapsayıcısında Hello varsayılan depolama hesabı değil</span><span class="sxs-lookup"><span data-stu-id="b6cb1-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="b6cb1-136">Merhaba varsayılan depolama hesabı, Azure Data Lake Store dizinindedir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="b6cb1-137">Küme oluşturma sırasında Data Lake Store'da hello kümenin HDFS hello köküdür hello dizinini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="b6cb1-138">Örneğin, hello `/clusters/myclustername/` dizin.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="b6cb1-139">Merhaba kümesi ile ilişkili bir varsayılan olmayan (ek) Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="b6cb1-140">Merhaba Data Lake Store hello küme tarafından kullanılan Hello kök dizini.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="b6cb1-141">Bu düzen hello küme dosya sistemi içeriyor hello dizininin dışında bulunan tooaccess verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="b6cb1-142">Daha fazla bilgi için bkz: Merhaba [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) Apache.org başvuru.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="b6cb1-143">Örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6cb1-143">Example configuration</span></span>

<span data-ttu-id="b6cb1-144">Merhaba aşağıdaki YAML olan hello yapılan bir alıntı `resources/writetohdfs.yaml` hello örnekte bulunan dosyası.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="b6cb1-145">Bu dosya hello kullanarak hello Storm topolojisini tanımlar [Flux](https://storm.apache.org/releases/1.1.0/flux.html) Apache Storm için çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="b6cb1-146">Bu YAML öğeleri aşağıdaki hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="b6cb1-147">`syncPolicy`: Dosyaları synched ve Temizlenen toohello dosya sistemi olduğunda tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="b6cb1-148">Bu örnekte, her 1000 diziler.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="b6cb1-149">`fileNameFormat`: Hello yolu ve dosya adı deseni toouse dosyaları yazılırken tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="b6cb1-150">Bu örnekte, bir filtre kullanarak çalışma zamanında hello yolu sağlanır ve hello dosya uzantısı `.txt`.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="b6cb1-151">`recordFormat`: Yazılmış hello dosyaları hello iç biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="b6cb1-152">Bu örnekte, alanlar hello tarafından sınırlandırılmıştır `|` karakter.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="b6cb1-153">`rotationPolicy`: Ne zaman tanımlar toorotate dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="b6cb1-154">Bu örnekte, hiçbir döndürme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="b6cb1-155">`hdfs-bolt`: Kullanır hello yapılandırma parametreleri olarak önceki bileşenleri hello `HdfsBolt` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="b6cb1-156">Merhaba Flux framework hakkında daha fazla bilgi için bkz: [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="b6cb1-157">Merhaba küme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6cb1-157">Configure hello cluster</span></span>

<span data-ttu-id="b6cb1-158">Varsayılan olarak, Hdınsight üzerinde Storm HdfsBolt toocommunicate Azure Storage veya Data Lake Store ile Storm'ın sınıf yolunda kullandığını hello bileşenleri içermez.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="b6cb1-159">Kullanım hello aşağıdaki komut dosyası eylemi tooadd bu bileşenleri toohello `extlib` kümenizdeki Storm için dizin:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="b6cb1-160">| Betik URI'si | Düğümleri tooapply kendisine | Parametreleri || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, yönetici | None |</span><span class="sxs-lookup"><span data-stu-id="b6cb1-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="b6cb1-161">Merhaba kümenizle bu komut dosyası kullanma hakkında daha fazla bilgi için bkz [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](./hdinsight-hadoop-customize-cluster-linux.md) belge.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="b6cb1-162">Derleme ve paket hello topolojisi</span><span class="sxs-lookup"><span data-stu-id="b6cb1-162">Build and package hello topology</span></span>

1. <span data-ttu-id="b6cb1-163">Merhaba örnek projesinden indirmeniz [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="b6cb1-164">Bir komut isteminden hello terminal veya kabuk oturumu değişiklik dizinleri toohello kök proje indirilir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="b6cb1-165">toobuild ve paket topoloji Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="b6cb1-166">Merhaba yapı ve paket oluşturma işlemi tamamlandıktan sonra adlı yeni bir dizin yok `target`, adlı bir dosyayı içeren `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="b6cb1-167">Bu dosya derlenmiş hello topoloji içerir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="b6cb1-168">Dağıtma ve çalıştırma hello topolojisi</span><span class="sxs-lookup"><span data-stu-id="b6cb1-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="b6cb1-169">Komut toocopy hello topoloji toohello Hdınsight kümesi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="b6cb1-170">Değiştir **kullanıcı** hello SSH kullanıcı adı ile Merhaba küme oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="b6cb1-171">Değiştir **CLUSTERNAME** hello küme hello adı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="b6cb1-172">İstendiğinde, hello SSH kullanıcı hello küme oluştururken kullanılan hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="b6cb1-173">Parola yerine bir ortak anahtar kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yolu toohello eşleşen özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b6cb1-174">Kullanma hakkında daha fazla bilgi için `scp` Hdınsight ile bkz [Hdınsight ile SSH kullanma](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b6cb1-175">Merhaba karşıya yükleme işlemi tamamlandıktan sonra SSH kullanarak tooconnect toohello Hdınsight kümesi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="b6cb1-176">Değiştir **kullanıcı** hello SSH kullanıcı adı ile Merhaba küme oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="b6cb1-177">Değiştir **CLUSTERNAME** hello küme hello adı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="b6cb1-178">İstendiğinde, hello SSH kullanıcı hello küme oluştururken kullanılan hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="b6cb1-179">Parola yerine bir ortak anahtar kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yolu toohello eşleşen özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="b6cb1-180">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="b6cb1-181">Bağlandıktan sonra kullanım hello aşağıdaki adlı bir dosya toocreate komut `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="b6cb1-182">Metin hello Merhaba içeriğine aşağıdaki kullanım hello `dev.properties` dosyası:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="b6cb1-183">Bu örnek, kümenizi hello varsayılan depolama alanı olarak Azure Storage hesabı kullandığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="b6cb1-184">Kümenizi Azure Data Lake Store kullanıyorsa kullanın `hdfs.url: adl:///` yerine.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="b6cb1-185">toosave hello dosya, kullanım __Ctrl + X__, ardından __Y__ve son olarak __Enter__.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="b6cb1-186">Bu dosyadaki Hello değerlerini hello Data Lake deposu URL'sini ve veri yazılır hello dizin adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="b6cb1-187">Komut toostart hello topolojisi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="b6cb1-188">Bu komut toohello Nimbus düğümü hello kümesinin göndererek hello Flux framework kullanarak hello topolojisi başlatır.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="b6cb1-189">Merhaba topoloji hello tarafından tanımlanan `writetohdfs.yaml` hello jar bulunan dosyası.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="b6cb1-190">Merhaba `dev.properties` dosya filtre olarak geçirilir ve hello dosyasında yer alan hello değerleri hello topolojisi tarafından okunur.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="b6cb1-191">Çıktı verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b6cb1-191">View output data</span></span>

<span data-ttu-id="b6cb1-192">tooview hello veri hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="b6cb1-193">Bu topoloji tarafından oluşturulan hello dosyaların listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="b6cb1-194">Merhaba aşağıdaki listede, hello önceki komutları tarafından döndürülen hello veri örneğidir:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="b6cb1-195">Merhaba topolojiyi durdurma</span><span class="sxs-lookup"><span data-stu-id="b6cb1-195">Stop hello topology</span></span>

<span data-ttu-id="b6cb1-196">Durdurulana kadar Storm topolojileri çalıştırmak veya hello kümesi silindi.</span><span class="sxs-lookup"><span data-stu-id="b6cb1-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="b6cb1-197">toostop topoloji Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b6cb1-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="b6cb1-198">Kümenizi Sil</span><span class="sxs-lookup"><span data-stu-id="b6cb1-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="b6cb1-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6cb1-199">Next steps</span></span>

<span data-ttu-id="b6cb1-200">Nasıl toouse Storm toowrite tooAzure depolama ve Azure Data Lake Store, Bul diğer öğrendiğinize göre [örnekler için Hdınsight Storm](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b6cb1-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

