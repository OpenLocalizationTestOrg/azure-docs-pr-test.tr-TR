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
# <a name="receive-events-from-event-hubs-using-apache-storm"></a>Apache Storm kullanarak Event Hubs'dan olayları alma

[Apache Storm](https://storm.incubator.apache.org) sınırsız olarak veri akışları güvenilir işlenmesini kolaylaştırır dağıtılmış gerçek zamanlı hesaplama sistemidir. Bu bölümde Azure olay hub'ları Storm spout olayları olay hub'larından almak için nasıl kullanılacağını gösterir. Apache Storm kullanarak, farklı düğümlerde barındırılan birden çok işlemler arasında olayları bölebilirsiniz. Storm ile olay hub'ları tümleştirme olay tüketimi saydam denetim noktası oluşturma Storm'ın Zookeeper yükleme seçeneğini kullanarak, kalıcı denetim noktalarını yönetme, ilerleme durumunu basitleştirir ve olay hub'larından paralel alır.

Alma desenleri Event Hubs hakkında daha fazla bilgi için bkz: [Event Hubs'a genel bakış][Event Hubs overview].

## <a name="create-project-and-add-code"></a>Proje oluşturma ve kod ekleme

Bu öğretici kullanan bir [Hdınsight Storm] [ HDInsight Storm] zaten kullanılabilir Event Hubs spout ile birlikte gelen yükleme.

1. İzleyin [Hdınsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) yeni bir Hdınsight kümesi oluşturma ve Uzak Masaüstü aracılığıyla bağlanmak için yordamı.
2. Kopya `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` yerel geliştirme ortamınızı dosyasına. Bu olaylar storm spout içerir.
3. Paketi yerel Maven deposuna yüklemek için aşağıdaki komutu kullanın. Bu, sonraki adımda Storm projesi başvuru olarak eklemenize olanak sağlar.

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. Eclipse'te, yeni bir Maven projesi oluşturun (tıklatın **dosya**, ardından **yeni**, ardından **proje**).
   
    ![][12]
5. Seçin **varsayılan çalışma alanı konumu kullanacak**, ardından **sonraki**
6. Seçin **maven archetype quickstart** archetype, ardından **sonraki**
7. INSERT bir **GroupID** ve **Artifactıd**, ardından **son**
8. İçinde **pom.xml**, aşağıdaki bağımlılıkları ekleyin `<dependency>` düğümü.

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

9. İçinde **src** klasörünü adlı bir dosya oluşturun **Config.properties** ve aşağıdaki kopyalayın değiştirerek, içerik `receive rule key` ve `event hub name` değerler:

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
    Değeri **eventhub.receiver.credits** Storm ardışık düzene serbest bırakmadan önce kaç tane olayları toplu belirler. Basitleştirmek amacıyla, bu örnekte bu değer 10'a ayarlar. Üretimde, genellikle daha yüksek değerine ayarlanmalıdır; Örneğin, 1024.
10. Adlı yeni bir sınıf oluşturmak **LoggerBolt** aşağıdaki kod ile:
    
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
    
    Bu Storm Cıvata alınan olayların içeriğini günlüğe kaydeder. Bu kolayca diziler depolama hizmetinde depolamak için genişletilebilir. [Hdınsight algılayıcı analiz öğretici] HBase verileri depolamak için aynı bu yaklaşımı kullanır.
11. Adlı bir sınıf oluşturmak **LogTopology** aşağıdaki kod ile:
    
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

    Bu sınıfın örneğini başlatmak için yapılandırma dosyasında özelliklerini kullanarak yeni bir Event Hubs spout oluşturur. Bu örneğin sayıda spout'lar görevleri olay hub'ındaki bölüm sayısı olarak bu olay hub'ı tarafından izin verilen maksimum paralellik kullanmak için oluşturduğu dikkate almak önemlidir.

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs'a genel bakış][Event Hubs overview]
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[Hdınsight algılayıcı analiz öğretici]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
