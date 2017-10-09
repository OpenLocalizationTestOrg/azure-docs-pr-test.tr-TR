---
title: "Azure Cosmos DB: Spark ve Apache TinkerPop Gremlin kullanarak grafik analiz gerçekleştirme | Microsoft Docs"
description: "Bu makalede ayarlama ve Azure Cosmos veritabanı Spark ve TinkerPop SparkGraphComputer grafik analizi ve Paralel hesaplama çalıştırmak için yönergeler sunar."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="a718e-103">Azure Cosmos DB: Spark ve Apache TinkerPop Gremlin kullanarak grafik analiz gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="a718e-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="a718e-104">[Azure Cosmos DB](introduction.md) olan hello Microsoft'un Genel dağıtılmış, birden çok model veritabanı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a718e-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="a718e-105">Oluşturma ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a718e-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="a718e-106">Azure Cosmos DB destekleyen kullanın (OLTP) grafik iş yükleri çevrimiçi işlem [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a718e-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="a718e-107">[Spark](http://spark.apache.org/) üzerinde genel amaçlı çevrimiçi analitik işlem (OLAP) veri işleme odaklanan bir Apache Software Foundation projesidir.</span><span class="sxs-lookup"><span data-stu-id="a718e-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="a718e-108">Spark benzer toohello Hadoop MapReduce modeli olan bir karma içinde bellek/disk tabanlı dağıtılmış bilgi işlem modelidir.</span><span class="sxs-lookup"><span data-stu-id="a718e-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="a718e-109">Apache Spark hello bulutta kullanarak dağıtabilirsiniz [Azure Hdınsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="a718e-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="a718e-110">Azure Cosmos DB ve Spark birleştirerek Gremlin kullandığınızda OLTP ve OLAP iş yüklerinin gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a718e-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="a718e-111">Bu hızlı başlangıç makalede toorun Gremlin Azure Cosmos DB karşı bir Azure Hdınsight Spark kümesinde nasıl sorgular gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a718e-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a718e-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a718e-112">Prerequisites</span></span>

<span data-ttu-id="a718e-113">Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a718e-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="a718e-114">Azure Hdınsight Spark kümesinde 2.0</span><span class="sxs-lookup"><span data-stu-id="a718e-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="a718e-115">JDK 1.8 + (JDK yoksa çalıştırmak `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="a718e-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="a718e-116">Maven (Maven yoksa, çalıştırmak `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="a718e-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="a718e-117">Bir Azure aboneliği ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="a718e-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="a718e-118">Hakkında bilgi için bir Azure Hdınsight Spark kümesi tooset bkz [sağlama Hdınsight kümeleri](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a718e-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="a718e-119">Bir Azure Cosmos DB veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a718e-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="a718e-120">İlk olarak, bir veritabanı hesabı hello grafik API'si ile Merhaba aşağıdakileri yaparak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a718e-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="a718e-121">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="a718e-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="a718e-122">Apache TinkerPop Al</span><span class="sxs-lookup"><span data-stu-id="a718e-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="a718e-123">Apache TinkerPop hello aşağıdakileri yaparak alın:</span><span class="sxs-lookup"><span data-stu-id="a718e-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="a718e-124">Uzak toohello ana hello Hdınsight küme düğümünün `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="a718e-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="a718e-125">Merhaba TinkerPop3 kaynak kodunu kopyalama, yerel olarak oluşturun ve tooMaven önbellek yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a718e-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="a718e-126">Merhaba Spark-Gremlin eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="a718e-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="a718e-127">a.</span><span class="sxs-lookup"><span data-stu-id="a718e-127">a.</span></span> <span data-ttu-id="a718e-128">Merhaba eklenti Hello yüklemesini üzüm tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="a718e-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="a718e-129">Merhaba eklenti ve bağımlılıklarını karşıdan yükleyebileceğiniz şekilde hello depoları bilgi üzüm için doldurun.</span><span class="sxs-lookup"><span data-stu-id="a718e-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="a718e-130">Konumunda mevcut değilse hello üzümlü yapılandırma dosyası oluşturma `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="a718e-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="a718e-131">Ayarları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a718e-131">Use hello following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="a718e-132">b.</span><span class="sxs-lookup"><span data-stu-id="a718e-132">b.</span></span> <span data-ttu-id="a718e-133">Gremlin konsolunu başlatın `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="a718e-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="a718e-134">c.</span><span class="sxs-lookup"><span data-stu-id="a718e-134">c.</span></span> <span data-ttu-id="a718e-135">Merhaba Gremlin eklenti Spark sürümüyle yükleyin hello önceki adımlarda oluşturduğunuz 3.3.0-SNAPSHOT:</span><span class="sxs-lookup"><span data-stu-id="a718e-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="a718e-136">Toosee olup olmadığını denetleyin `Hadoop-Gremlin` ile etkinleştirilen `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="a718e-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="a718e-137">Devre dışı bırak Spark Gremlin hello ile eklenti engel çünkü bu eklenti `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="a718e-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="a718e-138">TinkerPop3 bağımlılıkları hazırlama</span><span class="sxs-lookup"><span data-stu-id="a718e-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="a718e-139">Merhaba önceki adımda TinkerPop3 yapılandırıldığında hello işlem de tüm jar bağımlılıkları Spark ve Hadoop için hello hedef dizinde çekilen.</span><span class="sxs-lookup"><span data-stu-id="a718e-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="a718e-140">HDI ile önceden yüklenmiş ve ek bağımlılıklar yalnızca gerektiğinde isteme hello Kavanoz kullanın.</span><span class="sxs-lookup"><span data-stu-id="a718e-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="a718e-141">Git toohello Gremlin konsol hedef dizininde `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="a718e-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="a718e-142">Tüm Kavanoz altında taşıma `ext/` çok`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="a718e-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="a718e-143">Tüm jar kitaplıkları altında Kaldır `lib/` içinde değil hello listesi izliyorsanız:</span><span class="sxs-lookup"><span data-stu-id="a718e-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="a718e-144">Hello Azure Cosmos DB Spark bağlayıcı Al</span><span class="sxs-lookup"><span data-stu-id="a718e-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="a718e-145">Hello Azure Cosmos DB Spark bağlayıcı almak `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` ve Cosmos DB Java SDK'sı `azure-documentdb-1.10.0.jar` gelen [Azure Cosmos DB Spark Bağlayıcısı github'da](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="a718e-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="a718e-146">Alternatif olarak, onu yerel olarak oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="a718e-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="a718e-147">Spark Gremlin en son sürümünü Hello 1.6.1 Spark ile oluşturulmuş ve hello Azure Cosmos DB Spark Bağlayıcısı şu anda kullanılan, Spark ile 2.0.2, uyumlu olmadığından hello son TinkerPop3 kodu derleyin ve hello Kavanoz el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a718e-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="a718e-148">Aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a718e-148">Do hello following:</span></span>

    <span data-ttu-id="a718e-149">a.</span><span class="sxs-lookup"><span data-stu-id="a718e-149">a.</span></span> <span data-ttu-id="a718e-150">Hello Azure Cosmos DB Spark bağlayıcı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a718e-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="a718e-151">b.</span><span class="sxs-lookup"><span data-stu-id="a718e-151">b.</span></span> <span data-ttu-id="a718e-152">(Önceki adımlarda zaten yapılır) TinkerPop3 oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a718e-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="a718e-153">Tüm TinkerPop 3.3.0-SNAPSHOT Kavanoz yerel olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a718e-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="a718e-154">c.</span><span class="sxs-lookup"><span data-stu-id="a718e-154">c.</span></span> <span data-ttu-id="a718e-155">Güncelleştirme `tinkerpop.version` `azure-documentdb-spark/pom.xml` çok`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="a718e-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="a718e-156">d.</span><span class="sxs-lookup"><span data-stu-id="a718e-156">d.</span></span> <span data-ttu-id="a718e-157">Maven ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a718e-157">Build with Maven.</span></span> <span data-ttu-id="a718e-158">Merhaba gerekli Kavanoz yerleştirilir `target` ve `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="a718e-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="a718e-159">Kopya hello Kavanoz tooa yerel dizininde daha önce bahsedilen ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="a718e-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="a718e-160">Merhaba bağımlılıkları toohello Spark çalışan düğümleri Dağıt</span><span class="sxs-lookup"><span data-stu-id="a718e-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="a718e-161">Grafik verileri Hello dönüşümü TinkerPop3 üzerinde bağımlı olduğundan dağıtmalısınız hello ilgili bağımlılıkları tooall Spark çalışan düğümleri.</span><span class="sxs-lookup"><span data-stu-id="a718e-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="a718e-162">Kopya hello daha önce Gremlin bağımlılıklar, hello CosmosDB Spark bağlayıcı jar ve CosmosDB Java SDK'sı toohello çalışan düğümleri hello aşağıdakileri yaparak bahsedilen:</span><span class="sxs-lookup"><span data-stu-id="a718e-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="a718e-163">a.</span><span class="sxs-lookup"><span data-stu-id="a718e-163">a.</span></span> <span data-ttu-id="a718e-164">Tüm hello Kavanoz içine kopyalamak `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="a718e-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="a718e-165">b.</span><span class="sxs-lookup"><span data-stu-id="a718e-165">b.</span></span> <span data-ttu-id="a718e-166">Ambari panosunda hello bulabileceğiniz tüm Spark çalışan düğümleri Hello listesini almak `Spark2 Clients` hello listesinde `Spark2` bölümü.</span><span class="sxs-lookup"><span data-stu-id="a718e-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="a718e-167">c.</span><span class="sxs-lookup"><span data-stu-id="a718e-167">c.</span></span> <span data-ttu-id="a718e-168">Bu dizin tooeach hello düğümlerinin kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a718e-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="a718e-169">Hello ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="a718e-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="a718e-170">Merhaba HDP hello Spark kümesi sürümü bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a718e-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="a718e-171">Merhaba dizin adı altında olan `/usr/hdp/` (örneğin, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="a718e-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="a718e-172">Tüm düğümler için hdp.Version ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a718e-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="a718e-173">Ambari panosunda çok Git**YARN bölüm** > **yapılandırmalar** > **Gelişmiş**ve ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a718e-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="a718e-174">a.</span><span class="sxs-lookup"><span data-stu-id="a718e-174">a.</span></span> <span data-ttu-id="a718e-175">İçinde `Custom yarn-site`, yeni bir özellik eklemek `hdp.version` hello ana düğümün hello HDP sürümü hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="a718e-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="a718e-176">b.</span><span class="sxs-lookup"><span data-stu-id="a718e-176">b.</span></span> <span data-ttu-id="a718e-177">Merhaba yapılandırmaları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a718e-177">Save hello configurations.</span></span> <span data-ttu-id="a718e-178">Göz ardı edebilirsiniz uyarıları vardır.</span><span class="sxs-lookup"><span data-stu-id="a718e-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="a718e-179">c.</span><span class="sxs-lookup"><span data-stu-id="a718e-179">c.</span></span> <span data-ttu-id="a718e-180">Merhaba bildirim simgelerini göstermek gibi hello YARN ve Oozie hizmetlerini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a718e-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="a718e-181">Ortam değişkenleri hello ana düğümünde (Değiştir hello değerleri uygun şekilde) aşağıdaki kümesi hello:</span><span class="sxs-lookup"><span data-stu-id="a718e-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="a718e-182">Merhaba grafik yapılandırmasını hazırla</span><span class="sxs-lookup"><span data-stu-id="a718e-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="a718e-183">Yapılandırma dosyası ile hello Azure Cosmos DB bağlantı parametrelerini oluşturma ve Spark ayarları ve adresindeki yerleştirin `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="a718e-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for hello driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="a718e-184">Güncelleştirme hello `spark.driver.extraClassPath` ve `spark.executor.extraClassPath` tooinclude hello hello önceki adımda, bu durumda dağıtılan hello Kavanoz dizininin `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="a718e-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="a718e-185">Azure Cosmos DB için aşağıdaki ayrıntılara hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="a718e-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="a718e-186">Merhaba TinkerPop grafik yükleyin ve tooAzure Cosmos DB kaydedin</span><span class="sxs-lookup"><span data-stu-id="a718e-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="a718e-187">toodemonstrate nasıl toopersist Azure Cosmos DB kullanır hello TinkerPop Bu örnek içine bir grafik TinkerPop modern grafik önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="a718e-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="a718e-188">Merhaba grafik Kryo biçiminde depolanır ve hello TinkerPop deposunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a718e-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="a718e-189">Gremlin YARN modunda çalıştırdığınız için hello grafik verileri hello Hadoop dosya sistemi içinde kullanılabilir olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a718e-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="a718e-190">Kullanım hello aşağıdaki toomake bir dizin ve dosya Kopyala hello yerel grafik içine komutları.</span><span class="sxs-lookup"><span data-stu-id="a718e-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="a718e-191">Geçici olarak hello güncelleştirme `gremlin-spark.properties` toouse dosya `GryoInputFormat` tooread hello grafik.</span><span class="sxs-lookup"><span data-stu-id="a718e-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="a718e-192">Ayrıca belirtmek `inputLocation` hello dizini olarak, olduğu gibi hello aşağıdaki oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="a718e-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="a718e-193">Gremlin konsolunu başlatın ve sonra hesaplama adımları toopersist veri yapılandırılmış toohello Azure Cosmos DB toplama aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a718e-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="a718e-194">a.</span><span class="sxs-lookup"><span data-stu-id="a718e-194">a.</span></span> <span data-ttu-id="a718e-195">Merhaba grafik oluşturmak `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="a718e-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="a718e-196">b.</span><span class="sxs-lookup"><span data-stu-id="a718e-196">b.</span></span> <span data-ttu-id="a718e-197">Yazma için SparkGraphComputer kullanmak `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="a718e-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="a718e-198">Veri Gezgini'nden veriler bu hello tooAzure Cosmos DB kalıcı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a718e-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="a718e-199">Merhaba grafik Azure Cosmos DB'den yükleme ve Gremlin sorgular çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a718e-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="a718e-200">tooload hello grafiği Düzenle `gremlin-spark.properties` tooset `graphReader` çok`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="a718e-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="a718e-201">Yük hello grafik hello veri çapraz geçiş ve Gremlin sorguları ile Merhaba aşağıdakileri yaparak çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a718e-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="a718e-202">a.</span><span class="sxs-lookup"><span data-stu-id="a718e-202">a.</span></span> <span data-ttu-id="a718e-203">Merhaba Gremlin konsolunu Başlat `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="a718e-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="a718e-204">b.</span><span class="sxs-lookup"><span data-stu-id="a718e-204">b.</span></span> <span data-ttu-id="a718e-205">Merhaba yapılandırmayla Hello grafik oluşturmak `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="a718e-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="a718e-206">c.</span><span class="sxs-lookup"><span data-stu-id="a718e-206">c.</span></span> <span data-ttu-id="a718e-207">Grafik geçişi ile SparkGraphComputer oluşturma `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="a718e-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="a718e-208">d.</span><span class="sxs-lookup"><span data-stu-id="a718e-208">d.</span></span> <span data-ttu-id="a718e-209">Gremlin grafik sorguları aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a718e-209">Run hello following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="a718e-210">toosee daha ayrıntılı günlük, kümesinde hello günlük düzeyi `conf/log4j-console.properties` tooa daha fazla ayrıntı düzeyi.</span><span class="sxs-lookup"><span data-stu-id="a718e-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="a718e-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a718e-211">Next steps</span></span>

<span data-ttu-id="a718e-212">Bu hızlı başlangıç makalede, Azure Cosmos DB ve Spark birleştirerek toowork ile nasıl grafiklerde öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a718e-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
