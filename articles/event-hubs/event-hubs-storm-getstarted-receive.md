---
title: "Apache Storm kullanan Azure Event Hubs aaaReceive olaylarından | Microsoft Docs"
description: "Apache Storm kullanarak Event Hubs'dan alma kullanmaya başlama"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="f4dc9-103">Apache Storm kullanarak Event Hubs'dan olayları alma</span><span class="sxs-lookup"><span data-stu-id="f4dc9-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="f4dc9-104">[Apache Storm](https://storm.incubator.apache.org) sınırsız olarak veri akışları güvenilir işlenmesini kolaylaştırır dağıtılmış gerçek zamanlı hesaplama sistemidir.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="f4dc9-105">Bu bölümde, nasıl Azure olay hub'ları fırtınası toouse spout tooreceive olayları Event Hubs'dan gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="f4dc9-106">Apache Storm kullanarak, farklı düğümlerde barındırılan birden çok işlemler arasında olayları bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="f4dc9-107">Merhaba Storm ile olay hub'ları tümleştirme olay tüketimi saydam denetim noktası oluşturma Storm'ın Zookeeper yükleme seçeneğini kullanarak, kalıcı denetim noktalarını yönetme, ilerleme durumunu basitleştirir ve olay hub'larından paralel alır.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="f4dc9-108">Merhaba desenleri Event Hubs hakkında daha fazla bilgi almak için bkz [Event Hubs'a genel bakış][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="f4dc9-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="f4dc9-109">Proje oluşturma ve kod ekleme</span><span class="sxs-lookup"><span data-stu-id="f4dc9-109">Create project and add code</span></span>

<span data-ttu-id="f4dc9-110">Bu öğretici kullanan bir [Hdınsight Storm] [ HDInsight Storm] Event Hubs spout hello ile zaten gelen yükleme.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="f4dc9-111">Merhaba izleyin [Hdınsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) yordamı toocreate yeni Hdınsight kümesi ve Uzak Masaüstü tooit bağlanın.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="f4dc9-112">Kopya hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` dosya tooyour yerel geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="f4dc9-113">Merhaba olayları storm spout içerir.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="f4dc9-114">Kullanım hello aşağıdaki tooinstall hello paket hello yerel Maven deposuna komutu.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="f4dc9-115">Bu, bir sonraki adımda hello Storm başvuru olarak proje tooadd sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="f4dc9-116">Eclipse'te, yeni bir Maven projesi oluşturun (tıklatın **dosya**, ardından **yeni**, ardından **proje**).</span><span class="sxs-lookup"><span data-stu-id="f4dc9-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="f4dc9-117">Seçin **varsayılan çalışma alanı konumu kullanacak**, ardından **sonraki**</span><span class="sxs-lookup"><span data-stu-id="f4dc9-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="f4dc9-118">Select hello **maven archetype quickstart** archetype, ardından **sonraki**</span><span class="sxs-lookup"><span data-stu-id="f4dc9-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="f4dc9-119">INSERT bir **GroupID** ve **Artifactıd**, ardından **son**</span><span class="sxs-lookup"><span data-stu-id="f4dc9-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="f4dc9-120">İçinde **pom.xml**, hello bağımlılıklar aşağıdaki hello eklemek `<dependency>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. <span data-ttu-id="f4dc9-121">Merhaba, **src** klasörünü adlı bir dosya oluşturun **Config.properties** ve içeriği izleyerek, hello değiştirerek kopyalama hello `receive rule key` ve `event hub name` değerler:</span><span class="sxs-lookup"><span data-stu-id="f4dc9-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    <span data-ttu-id="f4dc9-122">Merhaba değeri **eventhub.receiver.credits** toohello Storm ardışık serbest bırakmadan önce kaç tane olayları toplu belirler.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="f4dc9-123">Basitlik Hello artırmak amacıyla için bu örnek, bu değer too10 ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="f4dc9-124">Üretimde, genellikle toohigher değerleri ayarlanmalıdır; Örneğin, 1024.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="f4dc9-125">Adlı yeni bir sınıf oluşturmak **LoggerBolt** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="f4dc9-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    <span data-ttu-id="f4dc9-126">Bu Storm Cıvata alınan hello olayları hello içeriğini günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="f4dc9-127">Bu, bir depolama hizmetindeki toostore diziler kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="f4dc9-128">Merhaba [Hdınsight algılayıcı analiz öğretici] HBase bu aynı yaklaşımı toostore verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="f4dc9-129">Adlı bir sınıf oluşturmak **LogTopology** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="f4dc9-129">Create a class called **LogTopology** with hello following code:</span></span>
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    <span data-ttu-id="f4dc9-130">Bu sınıf hello yapılandırma dosyası tooinstantiate hello özelliklerini kullanarak yeni bir Event Hubs spout oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="f4dc9-131">Bu örnek kadar oluşturur toonote görevleri hello hello event hub'ındaki bölüm sayısı olarak sipariş toouse hello maksimum paralellik bu olay hub'ın izin içinde spout'lar önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f4dc9-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4dc9-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f4dc9-132">Next steps</span></span>
<span data-ttu-id="f4dc9-133">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4dc9-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="f4dc9-134">[Event Hubs'a genel bakış][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="f4dc9-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="f4dc9-135">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4dc9-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="f4dc9-136">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="f4dc9-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[Hdınsight algılayıcı analiz öğretici]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
