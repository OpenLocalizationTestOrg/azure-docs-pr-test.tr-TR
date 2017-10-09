---
title: "aaaProcess olayları Event Hubs'dan Storm - Azure Hdınsight | Microsoft Docs"
description: "Nasıl tooprocess verilerden Azure Event Hubs bir C# Storm topolojisi ile Visual Studio'da hello kullanarak Hdınsight araçları Visual Studio için oluşturulmuş öğrenin."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Azure Event hubs'tan (C#) hdınsight'ta Storm işlem olayları

Bilgi nasıl toowork Azure olay hub'larından Hdınsight üzerinde Apache Storm ile. Bu belgede bir C# Storm topolojisini tooread ve yazma verileri Evbent hub kullanır

> [!NOTE]
> Bu proje Java sürümü için bkz: [işlem Azure Event Hubs (Java) hdınsight'ta Storm olaylarından](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

Bu belgedeki Hello adımları SCP.NET, Hdınsight'ta kolay toocreate C# topolojileri ve Storm ile kullanılmak üzere bileşenleri kolaylaştırır bir NuGet paketi kullanın.

> [!IMPORTANT]
> Bu belgede Hello adımları sırasında Visual Studio ile Windows geliştirme ortamına dayanır, hello derlenmiş proje gönderilen tooa Storm Hdınsight kümesinde Linux kullanıyor olabilir. Yalnızca Linux tabanlı kümelerde 28 Ekim 2016'dan sonra oluşturulan SCP.NET topolojileri destekler.

Hdınsight 3.4 ve büyük kullanım Mono toorun C# topolojileri. Bu belgede kullanılan hello örnek Hdınsight 3.6 ile çalışır. Hdınsight için kendi .NET çözümleri oluşturma üzerinde planlıyorsanız, hello denetleyin [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları belge.

### <a name="cluster-versioning"></a>Küme sürüm oluşturma

Merhaba projeniz için kullandığınız Microsoft.SCP.Net.SDK NuGet paketi yüklü Hdınsight üzerinde Storm ana sürümüne hello eşleşmesi gerekir. Hdınsight sürüm 3.5 ve 3.6 kullanmak Storm 1.x bu kümeleriyle SCP.NET sürüm 1.0.x.x kullanmalısınız.

> [!IMPORTANT]
> Bu belgedeki Hello örnek bir Hdınsight 3.5 veya 3,6 küme bekliyor.
>
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

C# topolojileri ayrıca .NET 4.5 hedeflemesi gerekir.

## <a name="how-toowork-with-event-hubs"></a>Nasıl toowork Event Hubs ile

Microsoft bir Storm topolojisinin Event Hubs'dan ile kullanılan toocommunicate olabilir Java bileşenleri kümesi sağlar. Bu bileşenler bir Hdınsight 3.6 uyumlu sürümünü içeren hello Java arşiv (JAR) dosyasını bulabilirsiniz [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Merhaba bileşenleri Java'da yazılmış olsa da, bunları bir C# topolojisi kolayca kullanabilirsiniz.

Bu örnekte aşağıdaki bileşenleri hello kullanılır:

* __EventHubSpout__: olay hub'larından verileri okur.
* __EventHubBolt__: veri tooEvent hub yazar.
* __EventHubSpoutConfig__: tooconfigure EventHubSpout kullanılır.
* __EventHubBoltConfig__: tooconfigure EventHubBolt kullanılır.

### <a name="example-spout-usage"></a>Örnek spout kullanım

SCP.NET EventHubSpout tooyour topoloji eklemek için yöntemler sağlar. Bu yöntemler bir Java bileşeni eklemek için hello genel yöntemler kullanmaktan daha kolay tooadd bir spout kolaylaştırır. Merhaba aşağıdaki örnekte nasıl toocreate kullanarak spout hello gösteren __SetEventHubSpout__ ve **EventHubSpoutConfig** SCP.NET tarafından sağlanan yöntemleri:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

Merhaba önceki örnek oluşturur adlı yeni bir spout bileşeni __EventHubSpout__ve bir event hub ile toocommunicate yapılandırır. Merhaba paralellik ipucu hello bileşeni için bölüm toohello sayısı hello event hub'ında ayarlanır. Bu ayar Storm sağlar toocreate hello bileşenin her bölüm için bir örneği.

### <a name="example-bolt-usage"></a>Örnek Cıvata kullanım

Kullanım hello **JavaComponmentConstructor** yöntemi toocreate hello Cıvata örneği. Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate ve hello yeni bir örneğini yapılandırın **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> Bu örneği kullanmak yerine bir dize olarak geçirilen Clojure ifade kullanır **JavaComponentConstructor** toocreate bir **EventHubBoltConfig**, hello spout örnek yaptığınız gibi. Her iki yöntem çalışır. En iyi tooyou hissi hello yöntemini kullanın.

## <a name="download-hello-completed-project"></a>Tamamlanan hello projenizi indirin

Bu öğreticide oluşturulan hello proje tam bir sürümünü yükleyebilirsiniz [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). Ancak, yine tooprovide yapılandırma ayarlarını Bu öğreticide hello adımları izleyerek gerekir.

### <a name="prerequisites"></a>Ön koşullar

* Bir [Hdınsight kümesi sürüm 3.5 veya 3.6 üzerinde Apache Storm](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > Bu belgede kullanılan hello örnek sürüm 3.5 ya da 3.6 hdınsight'ta Storm gerektirir. Bu Hdınsight, eski sürümleri toobreaking sınıf adı değişikliği nedeniyle ile çalışmaz. Eski kümeleriyle çalışır Bu örnek sürümü için bkz: [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* Bir [Azure olay hub'ı](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Merhaba [Azure .NET SDK'sı](http://azure.microsoft.com/downloads/).

* Merhaba [Visual Studio için Hdınsight Araçları](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 veya sonraki geliştirme ortamınızı. JDK yüklemeleri web'da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Merhaba **JAVA_HOME** Java içeren ortam değişkeni gereken noktası toohello dizini.
  * Merhaba **%JAVA_HOME%/bin** directory hello yolunda olması gerekir.

## <a name="download-hello-event-hubs-components"></a>Merhaba olay hub'ları bileşenlerini yükle

İndirme hello Event Hubs spout ve Cıvata bileşeninden [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Adlı bir dizin oluşturun `eventhubspout`ve hello dizine hello dosyasını kaydedin.

## <a name="configure-event-hubs"></a>Olay hub'ları yapılandırma

Bu örnek için hello veri kaynağı olay hub ' dir. Merhaba bilgileri hello "bir olay hub'ı oluşturma" bölümünde kullanın [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Merhaba olay hub'ı oluşturulduktan sonra hello görüntülemek **EventHub** dikey penceresinde hello Azure portal ve select **paylaşılan erişim ilkeleri**. Seçin **+ Ekle** ilkelere tooadd hello:

   | Ad | İzinler |
   | --- | --- |
   | Yazıcı |Gönder |
   | Okuyucu |Dinleme |

    ![Ekran görüntüsü, paylaşım erişim ilkeleri penceresi](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Select hello **okuyucu** ve **yazan** ilkeleri. Kopyalayın ve bu değerleri daha sonra kullanılmak üzere hello birincil anahtar değeri için her iki ilkeyi kaydedin.

## <a name="configure-hello-eventhubwriter"></a>Merhaba EventHubWriter yapılandırın

1. Visual Studio için hello en son sürümünü hello Hdınsight araçları yüklemediyseniz, bkz: [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Merhaba çözümden karşıdan [eventhub storm karma](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. Merhaba, **EventHubWriter** proje, açık hello **App.config** dosya. Merhaba bilgilerinden anahtarları aşağıdaki hello için hello değer önceki toofill yapılandırılmış hello olay hub'ı kullanın:

   | Anahtar | Değer |
   | --- | --- |
   | EventHubPolicyName |Yazıcı (Merhaba ilkesiyle için farklı bir ad kullandıysanız *Gönder* izni, bunun yerine kullanın.) |
   | EventHubPolicyKey |Merhaba yazıcı ilkesi için Hello anahtar. |
   | EventHubNamespace |Olay hub'ınızı içeren hello ad alanı. |
   | EventHubName |Olay hub'ı adınız. |
   | EventHubPartitionCount |Olay hub'ınızı bölüm Hello sayısı. |

4. Kaydet ve Kapat hello **App.config** dosya.

## <a name="configure-hello-eventhubreader"></a>Merhaba EventHubReader yapılandırın

1. Açık hello **EventHubReader** projesi.

2. Açık hello **App.config** hello dosyası **EventHubReader**. Merhaba bilgilerinden anahtarları aşağıdaki hello için hello değer önceki toofill yapılandırılmış hello olay hub'ı kullanın:

   | Anahtar | Değer |
   | --- | --- |
   | EventHubPolicyName |Okuyucu (Merhaba ilkesiyle için farklı bir ad kullandıysanız *dinleme* izni, bunun yerine kullanın.) |
   | EventHubPolicyKey |Merhaba okuyucu ilkesi için Hello anahtar. |
   | EventHubNamespace |Olay hub'ınızı içeren hello ad alanı. |
   | EventHubName |Olay hub'ı adınız. |
   | EventHubPartitionCount |Olay hub'ınızı bölüm Hello sayısı. |

3. Kaydet ve Kapat hello **App.config** dosya.

## <a name="deploy-hello-topologies"></a>Merhaba topolojilerini dağıtma

1. Gelen **Çözüm Gezgini**, sağ hello **EventHubReader** proje ve seçin **hdınsight'ta tooStorm gönderme**.

    ![Ekran görüntüsü, Çözüm Gezgini'nde, gönderme tooStorm vurgulanmış hdınsight'ta ile](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. Merhaba üzerinde **gönderme topoloji** iletişim kutusunda, **Storm kümesi**. Genişletme **ek yapılandırmalar**seçin **Java dosya yolları**seçin **...** ve daha önce indirdiğiniz hello JAR dosyasını içeren select başlangıç dizini. Son olarak, tıklatın **gönderme**.

    ![Gönderme topoloji ekran iletişim kutusu](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Merhaba topoloji gönderildiğinde hello **Storm topolojileri Görüntüleyicisi** görüntülenir. Merhaba topoloji, select hello tooview bilgilerini **EventHubReader** hello sol bölmede topolojisi.

    ![Storm topolojileri Görüntüleyicisi'nin ekran görüntüsü](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. Gelen **Çözüm Gezgini**, sağ hello **EventHubWriter** proje ve seçin **hdınsight'ta tooStorm gönderme**.

5. Merhaba üzerinde **gönderme topoloji** iletişim kutusunda, **Storm kümesi**. Genişletme **ek yapılandırmalar**seçin **Java dosya yolları**seçin **...** , ve hello JAR dosyasını içeren select hello dizini indirdiğiniz daha önce. Son olarak, tıklatın **gönderme**.

6. Merhaba topoloji gönderildiğinde hello topoloji hello listesinde yenileme **Storm topolojileri Görüntüleyicisi** her iki topolojide hello küme üzerinde çalışan tooverify.

7. İçinde **Storm topolojileri Görüntüleyicisi**seçin hello **EventHubReader** topolojisi.

8. tooopen hello bileşen hello Cıvata için Özet çift hello **LogBolt** hello diyagramındaki bileşen.

9. Merhaba, **yürütücüler** bölümünde, hello bağlantılardan birini hello seçin **bağlantı noktası** sütun. Merhaba bileşen tarafından günlüğe kaydedilen bilgi görüntüler. Merhaba günlüğe bilgi metnini izleyen benzer toohello şöyledir:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Merhaba topolojileri Durdur

toostop hello topolojiler, her topolojisi hello seçin **Storm topolojisini Görüntüleyicisi**, ardından **KILL**.

![Ekran görüntüsü, Storm topolojisini Görüntüleyici, KILL düğmesi vurgulanan](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Kümenizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede nasıl toouse hello Java Event Hubs spout ve bir C# topolojisi toowork Azure Event Hubs verilerle gelen Cıvata öğrendiniz. C# topolojileri, oluşturma hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [SCP Programlama Kılavuzu](hdinsight-storm-scp-programming-guide.md)
* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)
