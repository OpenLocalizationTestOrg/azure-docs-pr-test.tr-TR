---
title: "Apache Storm kullanan Azure Event Hubs'tan gelen olayları alma | Microsoft Docs"
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
ms.openlocfilehash: 3e15370c7602276ef323708632b324fe05497f41
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="8b675-103">Apache Storm kullanarak Event Hubs'dan olayları alma</span><span class="sxs-lookup"><span data-stu-id="8b675-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="8b675-104">[Apache Storm](https://storm.incubator.apache.org) sınırsız olarak veri akışları güvenilir işlenmesini kolaylaştırır dağıtılmış gerçek zamanlı hesaplama sistemidir.</span><span class="sxs-lookup"><span data-stu-id="8b675-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="8b675-105">Bu bölümde Azure olay hub'ları Storm spout olayları olay hub'larından almak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b675-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="8b675-106">Apache Storm kullanarak, farklı düğümlerde barındırılan birden çok işlemler arasında olayları bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b675-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="8b675-107">Storm ile olay hub'ları tümleştirme olay tüketimi saydam denetim noktası oluşturma Storm'ın Zookeeper yükleme seçeneğini kullanarak, kalıcı denetim noktalarını yönetme, ilerleme durumunu basitleştirir ve olay hub'larından paralel alır.</span><span class="sxs-lookup"><span data-stu-id="8b675-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="8b675-108">Alma desenleri Event Hubs hakkında daha fazla bilgi için bkz: [Event Hubs'a genel bakış][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="8b675-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="8b675-109">Proje oluşturma ve kod ekleme</span><span class="sxs-lookup"><span data-stu-id="8b675-109">Create project and add code</span></span>

<span data-ttu-id="8b675-110">Bu öğretici kullanan bir [Hdınsight Storm] [ HDInsight Storm] zaten kullanılabilir Event Hubs spout ile birlikte gelen yükleme.</span><span class="sxs-lookup"><span data-stu-id="8b675-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="8b675-111">İzleyin [Hdınsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) yeni bir Hdınsight kümesi oluşturma ve Uzak Masaüstü aracılığıyla bağlanmak için yordamı.</span><span class="sxs-lookup"><span data-stu-id="8b675-111">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="8b675-112">Kopya `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` yerel geliştirme ortamınızı dosyasına.</span><span class="sxs-lookup"><span data-stu-id="8b675-112">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="8b675-113">Bu olaylar storm spout içerir.</span><span class="sxs-lookup"><span data-stu-id="8b675-113">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="8b675-114">Paketi yerel Maven deposuna yüklemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b675-114">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="8b675-115">Bu, sonraki adımda Storm projesi başvuru olarak eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b675-115">This enables you to add it as a reference in the Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="8b675-116">Eclipse'te, yeni bir Maven projesi oluşturun (tıklatın **dosya**, ardından **yeni**, ardından **proje**).</span><span class="sxs-lookup"><span data-stu-id="8b675-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="8b675-117">Seçin **varsayılan çalışma alanı konumu kullanacak**, ardından **sonraki**</span><span class="sxs-lookup"><span data-stu-id="8b675-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="8b675-118">Seçin **maven archetype quickstart** archetype, ardından **sonraki**</span><span class="sxs-lookup"><span data-stu-id="8b675-118">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="8b675-119">INSERT bir **GroupID** ve **Artifactıd**, ardından **son**</span><span class="sxs-lookup"><span data-stu-id="8b675-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="8b675-120">İçinde **pom.xml**, aşağıdaki bağımlılıkları ekleyin `<dependency>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="8b675-120">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>

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

9. <span data-ttu-id="8b675-121">İçinde **src** klasörünü adlı bir dosya oluşturun **Config.properties** ve aşağıdaki kopyalayın değiştirerek, içerik `receive rule key` ve `event hub name` değerler:</span><span class="sxs-lookup"><span data-stu-id="8b675-121">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="8b675-122">Değeri **eventhub.receiver.credits** Storm ardışık düzene serbest bırakmadan önce kaç tane olayları toplu belirler.</span><span class="sxs-lookup"><span data-stu-id="8b675-122">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="8b675-123">Basitleştirmek amacıyla, bu örnekte bu değer 10'a ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b675-123">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="8b675-124">Üretimde, genellikle daha yüksek değerine ayarlanmalıdır; Örneğin, 1024.</span><span class="sxs-lookup"><span data-stu-id="8b675-124">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="8b675-125">Adlı yeni bir sınıf oluşturmak **LoggerBolt** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="8b675-125">Create a new class called **LoggerBolt** with the following code:</span></span>
    
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
    
    <span data-ttu-id="8b675-126">Bu Storm Cıvata alınan olayların içeriğini günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8b675-126">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="8b675-127">Bu kolayca diziler depolama hizmetinde depolamak için genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="8b675-127">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="8b675-128">[Hdınsight algılayıcı analiz öğretici] HBase verileri depolamak için aynı bu yaklaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b675-128">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="8b675-129">Adlı bir sınıf oluşturmak **LogTopology** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="8b675-129">Create a class called **LogTopology** with the following code:</span></span>
    
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
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
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

    <span data-ttu-id="8b675-130">Bu sınıfın örneğini başlatmak için yapılandırma dosyasında özelliklerini kullanarak yeni bir Event Hubs spout oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b675-130">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="8b675-131">Bu örneğin sayıda spout'lar görevleri olay hub'ındaki bölüm sayısı olarak bu olay hub'ı tarafından izin verilen maksimum paralellik kullanmak için oluşturduğu dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8b675-131">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b675-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b675-132">Next steps</span></span>
<span data-ttu-id="8b675-133">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b675-133">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="8b675-134">[Event Hubs'a genel bakış][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="8b675-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="8b675-135">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b675-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8b675-136">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="8b675-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
<span data-ttu-id="8b675-137">[Hdınsight algılayıcı analiz öğretici]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span><span class="sxs-lookup"><span data-stu-id="8b675-137">[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span></span>

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
