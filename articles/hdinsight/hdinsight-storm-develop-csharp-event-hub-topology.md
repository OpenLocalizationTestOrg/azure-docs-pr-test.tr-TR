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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="8884a-103">Azure Event hubs'tan (C#) hdınsight'ta Storm işlem olayları</span><span class="sxs-lookup"><span data-stu-id="8884a-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="8884a-104">Bilgi nasıl toowork Azure olay hub'larından Hdınsight üzerinde Apache Storm ile.</span><span class="sxs-lookup"><span data-stu-id="8884a-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="8884a-105">Bu belgede bir C# Storm topolojisini tooread ve yazma verileri Evbent hub kullanır</span><span class="sxs-lookup"><span data-stu-id="8884a-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="8884a-106">Bu proje Java sürümü için bkz: [işlem Azure Event Hubs (Java) hdınsight'ta Storm olaylarından](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="8884a-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="8884a-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="8884a-107">SCP.NET</span></span>

<span data-ttu-id="8884a-108">Bu belgedeki Hello adımları SCP.NET, Hdınsight'ta kolay toocreate C# topolojileri ve Storm ile kullanılmak üzere bileşenleri kolaylaştırır bir NuGet paketi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8884a-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8884a-109">Bu belgede Hello adımları sırasında Visual Studio ile Windows geliştirme ortamına dayanır, hello derlenmiş proje gönderilen tooa Storm Hdınsight kümesinde Linux kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="8884a-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="8884a-110">Yalnızca Linux tabanlı kümelerde 28 Ekim 2016'dan sonra oluşturulan SCP.NET topolojileri destekler.</span><span class="sxs-lookup"><span data-stu-id="8884a-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="8884a-111">Hdınsight 3.4 ve büyük kullanım Mono toorun C# topolojileri.</span><span class="sxs-lookup"><span data-stu-id="8884a-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="8884a-112">Bu belgede kullanılan hello örnek Hdınsight 3.6 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="8884a-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="8884a-113">Hdınsight için kendi .NET çözümleri oluşturma üzerinde planlıyorsanız, hello denetleyin [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları belge.</span><span class="sxs-lookup"><span data-stu-id="8884a-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="8884a-114">Küme sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="8884a-114">Cluster versioning</span></span>

<span data-ttu-id="8884a-115">Merhaba projeniz için kullandığınız Microsoft.SCP.Net.SDK NuGet paketi yüklü Hdınsight üzerinde Storm ana sürümüne hello eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8884a-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="8884a-116">Hdınsight sürüm 3.5 ve 3.6 kullanmak Storm 1.x bu kümeleriyle SCP.NET sürüm 1.0.x.x kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8884a-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8884a-117">Bu belgedeki Hello örnek bir Hdınsight 3.5 veya 3,6 küme bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8884a-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="8884a-118">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="8884a-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8884a-119">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8884a-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="8884a-120">C# topolojileri ayrıca .NET 4.5 hedeflemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8884a-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="8884a-121">Nasıl toowork Event Hubs ile</span><span class="sxs-lookup"><span data-stu-id="8884a-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="8884a-122">Microsoft bir Storm topolojisinin Event Hubs'dan ile kullanılan toocommunicate olabilir Java bileşenleri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8884a-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="8884a-123">Bu bileşenler bir Hdınsight 3.6 uyumlu sürümünü içeren hello Java arşiv (JAR) dosyasını bulabilirsiniz [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="8884a-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8884a-124">Merhaba bileşenleri Java'da yazılmış olsa da, bunları bir C# topolojisi kolayca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8884a-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="8884a-125">Bu örnekte aşağıdaki bileşenleri hello kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8884a-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="8884a-126">__EventHubSpout__: olay hub'larından verileri okur.</span><span class="sxs-lookup"><span data-stu-id="8884a-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="8884a-127">__EventHubBolt__: veri tooEvent hub yazar.</span><span class="sxs-lookup"><span data-stu-id="8884a-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="8884a-128">__EventHubSpoutConfig__: tooconfigure EventHubSpout kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8884a-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="8884a-129">__EventHubBoltConfig__: tooconfigure EventHubBolt kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8884a-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="8884a-130">Örnek spout kullanım</span><span class="sxs-lookup"><span data-stu-id="8884a-130">Example spout usage</span></span>

<span data-ttu-id="8884a-131">SCP.NET EventHubSpout tooyour topoloji eklemek için yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8884a-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="8884a-132">Bu yöntemler bir Java bileşeni eklemek için hello genel yöntemler kullanmaktan daha kolay tooadd bir spout kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="8884a-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="8884a-133">Merhaba aşağıdaki örnekte nasıl toocreate kullanarak spout hello gösteren __SetEventHubSpout__ ve **EventHubSpoutConfig** SCP.NET tarafından sağlanan yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="8884a-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="8884a-134">Merhaba önceki örnek oluşturur adlı yeni bir spout bileşeni __EventHubSpout__ve bir event hub ile toocommunicate yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8884a-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="8884a-135">Merhaba paralellik ipucu hello bileşeni için bölüm toohello sayısı hello event hub'ında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8884a-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="8884a-136">Bu ayar Storm sağlar toocreate hello bileşenin her bölüm için bir örneği.</span><span class="sxs-lookup"><span data-stu-id="8884a-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="8884a-137">Örnek Cıvata kullanım</span><span class="sxs-lookup"><span data-stu-id="8884a-137">Example bolt usage</span></span>

<span data-ttu-id="8884a-138">Kullanım hello **JavaComponmentConstructor** yöntemi toocreate hello Cıvata örneği.</span><span class="sxs-lookup"><span data-stu-id="8884a-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="8884a-139">Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate ve hello yeni bir örneğini yapılandırın **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="8884a-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

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
> <span data-ttu-id="8884a-140">Bu örneği kullanmak yerine bir dize olarak geçirilen Clojure ifade kullanır **JavaComponentConstructor** toocreate bir **EventHubBoltConfig**, hello spout örnek yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="8884a-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="8884a-141">Her iki yöntem çalışır.</span><span class="sxs-lookup"><span data-stu-id="8884a-141">Either method works.</span></span> <span data-ttu-id="8884a-142">En iyi tooyou hissi hello yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8884a-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="8884a-143">Tamamlanan hello projenizi indirin</span><span class="sxs-lookup"><span data-stu-id="8884a-143">Download hello completed project</span></span>

<span data-ttu-id="8884a-144">Bu öğreticide oluşturulan hello proje tam bir sürümünü yükleyebilirsiniz [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="8884a-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="8884a-145">Ancak, yine tooprovide yapılandırma ayarlarını Bu öğreticide hello adımları izleyerek gerekir.</span><span class="sxs-lookup"><span data-stu-id="8884a-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8884a-146">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8884a-146">Prerequisites</span></span>

* <span data-ttu-id="8884a-147">Bir [Hdınsight kümesi sürüm 3.5 veya 3.6 üzerinde Apache Storm](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8884a-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="8884a-148">Bu belgede kullanılan hello örnek sürüm 3.5 ya da 3.6 hdınsight'ta Storm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8884a-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="8884a-149">Bu Hdınsight, eski sürümleri toobreaking sınıf adı değişikliği nedeniyle ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8884a-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="8884a-150">Eski kümeleriyle çalışır Bu örnek sürümü için bkz: [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="8884a-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="8884a-151">Bir [Azure olay hub'ı](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="8884a-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="8884a-152">Merhaba [Azure .NET SDK'sı](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8884a-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="8884a-153">Merhaba [Visual Studio için Hdınsight Araçları](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8884a-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="8884a-154">Java JDK 1.8 veya sonraki geliştirme ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="8884a-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="8884a-155">JDK yüklemeleri web'da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="8884a-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="8884a-156">Merhaba **JAVA_HOME** Java içeren ortam değişkeni gereken noktası toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="8884a-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="8884a-157">Merhaba **%JAVA_HOME%/bin** directory hello yolunda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8884a-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="8884a-158">Merhaba olay hub'ları bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="8884a-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="8884a-159">İndirme hello Event Hubs spout ve Cıvata bileşeninden [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="8884a-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="8884a-160">Adlı bir dizin oluşturun `eventhubspout`ve hello dizine hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8884a-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="8884a-161">Olay hub'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8884a-161">Configure Event Hubs</span></span>

<span data-ttu-id="8884a-162">Bu örnek için hello veri kaynağı olay hub ' dir.</span><span class="sxs-lookup"><span data-stu-id="8884a-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="8884a-163">Merhaba bilgileri hello "bir olay hub'ı oluşturma" bölümünde kullanın [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="8884a-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="8884a-164">Merhaba olay hub'ı oluşturulduktan sonra hello görüntülemek **EventHub** dikey penceresinde hello Azure portal ve select **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="8884a-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="8884a-165">Seçin **+ Ekle** ilkelere tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="8884a-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="8884a-166">Ad</span><span class="sxs-lookup"><span data-stu-id="8884a-166">Name</span></span> | <span data-ttu-id="8884a-167">İzinler</span><span class="sxs-lookup"><span data-stu-id="8884a-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="8884a-168">Yazıcı</span><span class="sxs-lookup"><span data-stu-id="8884a-168">writer</span></span> |<span data-ttu-id="8884a-169">Gönder</span><span class="sxs-lookup"><span data-stu-id="8884a-169">Send</span></span> |
   | <span data-ttu-id="8884a-170">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="8884a-170">reader</span></span> |<span data-ttu-id="8884a-171">Dinleme</span><span class="sxs-lookup"><span data-stu-id="8884a-171">Listen</span></span> |

    ![Ekran görüntüsü, paylaşım erişim ilkeleri penceresi](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="8884a-173">Select hello **okuyucu** ve **yazan** ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="8884a-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="8884a-174">Kopyalayın ve bu değerleri daha sonra kullanılmak üzere hello birincil anahtar değeri için her iki ilkeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8884a-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="8884a-175">Merhaba EventHubWriter yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8884a-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="8884a-176">Visual Studio için hello en son sürümünü hello Hdınsight araçları yüklemediyseniz, bkz: [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8884a-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="8884a-177">Merhaba çözümden karşıdan [eventhub storm karma](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="8884a-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="8884a-178">Merhaba, **EventHubWriter** proje, açık hello **App.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="8884a-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="8884a-179">Merhaba bilgilerinden anahtarları aşağıdaki hello için hello değer önceki toofill yapılandırılmış hello olay hub'ı kullanın:</span><span class="sxs-lookup"><span data-stu-id="8884a-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="8884a-180">Anahtar</span><span class="sxs-lookup"><span data-stu-id="8884a-180">Key</span></span> | <span data-ttu-id="8884a-181">Değer</span><span class="sxs-lookup"><span data-stu-id="8884a-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8884a-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="8884a-182">EventHubPolicyName</span></span> |<span data-ttu-id="8884a-183">Yazıcı (Merhaba ilkesiyle için farklı bir ad kullandıysanız *Gönder* izni, bunun yerine kullanın.)</span><span class="sxs-lookup"><span data-stu-id="8884a-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="8884a-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="8884a-184">EventHubPolicyKey</span></span> |<span data-ttu-id="8884a-185">Merhaba yazıcı ilkesi için Hello anahtar.</span><span class="sxs-lookup"><span data-stu-id="8884a-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="8884a-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="8884a-186">EventHubNamespace</span></span> |<span data-ttu-id="8884a-187">Olay hub'ınızı içeren hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="8884a-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="8884a-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="8884a-188">EventHubName</span></span> |<span data-ttu-id="8884a-189">Olay hub'ı adınız.</span><span class="sxs-lookup"><span data-stu-id="8884a-189">Your event hub name.</span></span> |
   | <span data-ttu-id="8884a-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="8884a-190">EventHubPartitionCount</span></span> |<span data-ttu-id="8884a-191">Olay hub'ınızı bölüm Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="8884a-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="8884a-192">Kaydet ve Kapat hello **App.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="8884a-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="8884a-193">Merhaba EventHubReader yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8884a-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="8884a-194">Açık hello **EventHubReader** projesi.</span><span class="sxs-lookup"><span data-stu-id="8884a-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="8884a-195">Açık hello **App.config** hello dosyası **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="8884a-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="8884a-196">Merhaba bilgilerinden anahtarları aşağıdaki hello için hello değer önceki toofill yapılandırılmış hello olay hub'ı kullanın:</span><span class="sxs-lookup"><span data-stu-id="8884a-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="8884a-197">Anahtar</span><span class="sxs-lookup"><span data-stu-id="8884a-197">Key</span></span> | <span data-ttu-id="8884a-198">Değer</span><span class="sxs-lookup"><span data-stu-id="8884a-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8884a-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="8884a-199">EventHubPolicyName</span></span> |<span data-ttu-id="8884a-200">Okuyucu (Merhaba ilkesiyle için farklı bir ad kullandıysanız *dinleme* izni, bunun yerine kullanın.)</span><span class="sxs-lookup"><span data-stu-id="8884a-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="8884a-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="8884a-201">EventHubPolicyKey</span></span> |<span data-ttu-id="8884a-202">Merhaba okuyucu ilkesi için Hello anahtar.</span><span class="sxs-lookup"><span data-stu-id="8884a-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="8884a-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="8884a-203">EventHubNamespace</span></span> |<span data-ttu-id="8884a-204">Olay hub'ınızı içeren hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="8884a-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="8884a-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="8884a-205">EventHubName</span></span> |<span data-ttu-id="8884a-206">Olay hub'ı adınız.</span><span class="sxs-lookup"><span data-stu-id="8884a-206">Your event hub name.</span></span> |
   | <span data-ttu-id="8884a-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="8884a-207">EventHubPartitionCount</span></span> |<span data-ttu-id="8884a-208">Olay hub'ınızı bölüm Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="8884a-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="8884a-209">Kaydet ve Kapat hello **App.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="8884a-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="8884a-210">Merhaba topolojilerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="8884a-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="8884a-211">Gelen **Çözüm Gezgini**, sağ hello **EventHubReader** proje ve seçin **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="8884a-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Ekran görüntüsü, Çözüm Gezgini'nde, gönderme tooStorm vurgulanmış hdınsight'ta ile](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="8884a-213">Merhaba üzerinde **gönderme topoloji** iletişim kutusunda, **Storm kümesi**.</span><span class="sxs-lookup"><span data-stu-id="8884a-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="8884a-214">Genişletme **ek yapılandırmalar**seçin **Java dosya yolları**seçin **...** ve daha önce indirdiğiniz hello JAR dosyasını içeren select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="8884a-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="8884a-215">Son olarak, tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="8884a-215">Finally, click **Submit**.</span></span>

    ![Gönderme topoloji ekran iletişim kutusu](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="8884a-217">Merhaba topoloji gönderildiğinde hello **Storm topolojileri Görüntüleyicisi** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8884a-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="8884a-218">Merhaba topoloji, select hello tooview bilgilerini **EventHubReader** hello sol bölmede topolojisi.</span><span class="sxs-lookup"><span data-stu-id="8884a-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Storm topolojileri Görüntüleyicisi'nin ekran görüntüsü](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="8884a-220">Gelen **Çözüm Gezgini**, sağ hello **EventHubWriter** proje ve seçin **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="8884a-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="8884a-221">Merhaba üzerinde **gönderme topoloji** iletişim kutusunda, **Storm kümesi**.</span><span class="sxs-lookup"><span data-stu-id="8884a-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="8884a-222">Genişletme **ek yapılandırmalar**seçin **Java dosya yolları**seçin **...** , ve hello JAR dosyasını içeren select hello dizini indirdiğiniz daha önce.</span><span class="sxs-lookup"><span data-stu-id="8884a-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="8884a-223">Son olarak, tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="8884a-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="8884a-224">Merhaba topoloji gönderildiğinde hello topoloji hello listesinde yenileme **Storm topolojileri Görüntüleyicisi** her iki topolojide hello küme üzerinde çalışan tooverify.</span><span class="sxs-lookup"><span data-stu-id="8884a-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="8884a-225">İçinde **Storm topolojileri Görüntüleyicisi**seçin hello **EventHubReader** topolojisi.</span><span class="sxs-lookup"><span data-stu-id="8884a-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="8884a-226">tooopen hello bileşen hello Cıvata için Özet çift hello **LogBolt** hello diyagramındaki bileşen.</span><span class="sxs-lookup"><span data-stu-id="8884a-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="8884a-227">Merhaba, **yürütücüler** bölümünde, hello bağlantılardan birini hello seçin **bağlantı noktası** sütun.</span><span class="sxs-lookup"><span data-stu-id="8884a-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="8884a-228">Merhaba bileşen tarafından günlüğe kaydedilen bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8884a-228">This displays information logged by hello component.</span></span> <span data-ttu-id="8884a-229">Merhaba günlüğe bilgi metnini izleyen benzer toohello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8884a-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="8884a-230">Merhaba topolojileri Durdur</span><span class="sxs-lookup"><span data-stu-id="8884a-230">Stop hello topologies</span></span>

<span data-ttu-id="8884a-231">toostop hello topolojiler, her topolojisi hello seçin **Storm topolojisini Görüntüleyicisi**, ardından **KILL**.</span><span class="sxs-lookup"><span data-stu-id="8884a-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Ekran görüntüsü, Storm topolojisini Görüntüleyici, KILL düğmesi vurgulanan](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="8884a-233">Kümenizi Sil</span><span class="sxs-lookup"><span data-stu-id="8884a-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="8884a-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8884a-234">Next steps</span></span>

<span data-ttu-id="8884a-235">Bu belgede nasıl toouse hello Java Event Hubs spout ve bir C# topolojisi toowork Azure Event Hubs verilerle gelen Cıvata öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="8884a-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="8884a-236">C# topolojileri, oluşturma hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="8884a-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="8884a-237">Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="8884a-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="8884a-238">SCP Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8884a-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="8884a-239">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="8884a-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
