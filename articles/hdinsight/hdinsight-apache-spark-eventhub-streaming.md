---
title: "aaaUse ile olay hub'ları Azure hdınsight'ta Apache Spark akış | Microsoft Docs"
description: "Nasıl toosend veri akışı tooAzure olay hub'ı ve sonra bu olayları bir scala uygulaması kullanarak Hdınsight Spark kümesinde almak bir Apache Spark akış örnek oluşturun."
keywords: "Apache spark akış, spark akış, spark örnek, apache spark akış örneği, olay hub'ı azure örneği, spark örnek"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="3f5d4-104">Apache Spark akış: Hdınsight'ta Spark ile Azure Event Hubs işlem verilerini küme</span><span class="sxs-lookup"><span data-stu-id="3f5d4-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="3f5d4-105">Bu makalede, aşağıdaki adımları hello içerir örnek akış bir Apache Spark oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="3f5d4-106">Bir Azure olay Hub'ına bir tek başına uygulama tooingest iletileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="3f5d4-107">İki farklı yaklaşım ile gerçek zamanlı Azure Hdınsight'ta Spark kümesinde çalışan bir uygulama kullanarak olay Hub'ından Merhaba iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="3f5d4-108">Toopersist veri toodifferent depolama sistemlerini akış analitik komut zincirleri oluşturun veya hello kolay bir şekilde verilerinden öngörü edinme.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f5d4-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3f5d4-109">Prerequisites</span></span>

* <span data-ttu-id="3f5d4-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-110">An Azure subscription.</span></span> <span data-ttu-id="3f5d4-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="3f5d4-112">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3f5d4-113">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="3f5d4-114">Spark akış kavramları</span><span class="sxs-lookup"><span data-stu-id="3f5d4-114">Spark Streaming concepts</span></span>

<span data-ttu-id="3f5d4-115">Spark akış ayrıntılı bir açıklaması için bkz: [Apache Spark genel bakış akış](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="3f5d4-116">Hdınsight aynı akış özellikleri tooa Spark küme Azure'da hello getirir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="3f5d4-117">Bu çözüm ne yapar?</span><span class="sxs-lookup"><span data-stu-id="3f5d4-117">What does this solution do?</span></span>

<span data-ttu-id="3f5d4-118">Bu makalede, toocreate bir Spark akış örneği hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="3f5d4-119">Bir akış olayların alacak bir Azure Event Hub oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="3f5d4-120">Bir yerel tek başına uygulamayı çalıştırmak olaylar oluşturur ve toohello Azure olay hub'ı iter.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="3f5d4-121">Bu örnek uygulama hello konumunda yayımlanır [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="3f5d4-122">Çeşitli veri işleme/analiz gerçekleştirmek ve bir akış uygulaması Azure olay Hub'ından akış olayları okur bir Spark kümesi üzerinde uzaktan çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="3f5d4-123">Bir Azure olay hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="3f5d4-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="3f5d4-124">Toohello üzerinde oturum [Azure Portal](https://ms.portal.azure.com), tıklatıp **yeni** hello adresindeki hello ekranın sol üst.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="3f5d4-125">**Nesnelerin İnterneti**’ne ve ardından **Event Hubs**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="3f5d4-126">![Örnek Spark akış Create event hub](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "örnek Spark akış Create event hub")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="3f5d4-127">Merhaba, **ad alanı oluşturma** dikey penceresinde, bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="3f5d4-128">Merhaba fiyatlandırma Katmanı (temel veya standart) seçin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="3f5d4-129">Ayrıca, hangi toocreate hello kaynak bir Azure aboneliği, kaynak grubunu ve konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="3f5d4-130">Tıklatın **oluşturma** toocreate hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="3f5d4-131">![Bir örnek Spark akış için olay hub'ı ad](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "örnek Spark akış için bir olay hub'ı adı belirtin")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f5d4-132">Select aynı hello **konumu** Apache Spark kümeniz Hdınsight tooreduce gecikme ve maliyetlerin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="3f5d4-133">Merhaba olay hub'ları ad listesinde hello yeni oluşturulan ad alanı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="3f5d4-134">Merhaba ad alanı dikey penceresinde tıklayın **Event Hubs**ve ardından **+ olay hub'ı** toocreate yeni bir olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="3f5d4-135">![Örnek Spark akış Create event hub](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "örnek Spark akış Create event hub")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="3f5d4-136">Olay hub'ı, kümesi hello bölüm sayısı too10 ve ileti bekletme too1 için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="3f5d4-137">Böylece hello geri kalan varsayılan olarak bırakın ve ardından Biz bu çözümdeki Merhaba iletileri arşivleme değil **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="3f5d4-138">![Olay hub'ı ayrıntılarını sağlamak için örnek akış Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "için Spark akış örnek olay hub'ı ayrıntılarını sağlayın")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="3f5d4-139">Olay hub'ı yeni oluşturulan hello hello Event Hub dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="3f5d4-140">![Merhaba Spark akış örneği için olay hub'ı görüntülemek](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "görünüm Event Hub'hello için Spark akış örneği")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="3f5d4-141">Geri hello ad alanı dikey penceresinde (değil hello belirli olay Hub dikey) tıklayın **paylaşılan erişim ilkeleri**ve ardından **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="3f5d4-142">![Merhaba Spark akış örneği için olay hub'ı ilkeler ayarlama](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "hello için Event Hub'ı ayarlamak ilkeleri Spark akış örneği")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="3f5d4-143">Merhaba Kopyala düğmesine toocopy hello tıklatın **RootManageSharedAccessKey** birincil anahtar ve bağlantı dizesi toohello Pano.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="3f5d4-144">Bu toouse daha sonra hello öğreticide kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="3f5d4-145">![Merhaba Spark akış örneği için olay hub'ı ilke anahtarları görüntülemek](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "görünüm olay hub'ı ilke anahtarları hello için Spark akış örneği")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="3f5d4-146">İletileri tooAzure olay hub'ı kullanan bir örnek Scala uygulamaları Gönder</span><span class="sxs-lookup"><span data-stu-id="3f5d4-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="3f5d4-147">Bu bölümdeki olayların bir akış oluşturur ve tooAzure daha önce oluşturduğunuz olay Hub gönderen bir tek başına yerel Scala uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="3f5d4-148">Bu uygulama github'da kullanılabilir [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="3f5d4-149">Bu GitHub deposunu zaten çatallanmış Hello adımlar burada varsayar.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="3f5d4-150">Merhaba aşağıdaki bu uygulamayı çalıştırdığınız hello bilgisayarda yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="3f5d4-151">Oracle Java Geliştirme Seti.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-151">Oracle Java Development kit.</span></span> <span data-ttu-id="3f5d4-152">Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="3f5d4-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-153">Apache Maven.</span></span> <span data-ttu-id="3f5d4-154">Buradan indirebilirsiniz [burada](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="3f5d4-155">Yönergeler tooinstall Maven kullanılabilir [burada](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="3f5d4-156">Bir komut istemi açın ve hello GitHub deposuna Merhaba örnek Scala uygulaması için klonlanmış toohello konuma gidin ve komut toobuild Merhaba uygulaması aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="3f5d4-157">Merhaba çıkış jar Merhaba uygulaması için **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, altında oluşturulan **/target** dizin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="3f5d4-158">Bu makale tootest hello eksiksiz çözüm içinde daha sonra bu JAR kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="3f5d4-159">Uygulama tooreceive iletileri olay Hub'ından bir Spark kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="3f5d4-160">İki yaklaşım tooconnect Spark akış ve Azure Event Hubs, alıcı tabanlı bağlantı ve doğrudan-DStream tabanlı bağlantı sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="3f5d4-161">Doğrudan-DStream tabanlı 2017 Oca üzerinde hello 2.0.3 sürümde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="3f5d4-162">Daha fazla kullanıcı olarak tooreplace hello özgün alıcı tabanlı bağlantı beklenir ve verimli kaynak.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="3f5d4-163">Daha fazla ayrıntı bulunan [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="3f5d4-164">Doğrudan DStream yalnızca Spark 2.0 + destekler.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="3f5d4-165">Merhaba bağımlılık toospark eventhubs Bağlayıcısı ile uygulamaları derleme</span><span class="sxs-lookup"><span data-stu-id="3f5d4-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="3f5d4-166">Biz de Spark-EventHubs github'da sürümü hazırlama hello yayımlar.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="3f5d4-167">toouse hello hazırlama Spark EventHubs, hello ilk adımı tooindicate girişi toopom.xml aşağıdaki hello ekleyerek kaynak deposu hello olarak GitHub sürümüdür:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="3f5d4-168">Bağımlılık tooyour proje tootake hello yayın öncesi sürüm aşağıdaki hello daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="3f5d4-169">Maven bağımlılığı</span><span class="sxs-lookup"><span data-stu-id="3f5d4-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="3f5d4-170">SBT bağımlılık</span><span class="sxs-lookup"><span data-stu-id="3f5d4-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="3f5d4-171">Doğrudan DStream bağlantı</span><span class="sxs-lookup"><span data-stu-id="3f5d4-171">Direct DStream Connection</span></span>

<span data-ttu-id="3f5d4-172">İçinde doğrudan DStream kullanan örnekler içeren bir önceden derlenmiş jar dosyasını karşıdan [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="3f5d4-173">Merhaba jar dosyasını içeren kaynak kodu kullanılabilir üç örnekler [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="3f5d4-174">Alma [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) bir örnek olarak:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="3f5d4-175">Örneğin, yukarıdaki hello içinde `eventhubParameters` hello parametreleri belirli tooa tek EventHubs örnek ve sahip toopass, toohello `createDirectStreams` doğrudan DStream nesne eşleme tooa olay hub'ları ad alanı oluşturur API.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="3f5d4-176">Merhaba doğrudan DStream nesnesi üzerinde Spark akış API çerçevesi tarafından sağlanan herhangi bir DStream API'yi çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="3f5d4-177">Bu örnekte, biz hello son 3 mikro toplu aralıkları her sözcüğün hello sıklığını hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="3f5d4-178">Alıcı tabanlı bağlantı</span><span class="sxs-lookup"><span data-stu-id="3f5d4-178">Receiver-based Connection</span></span>

<span data-ttu-id="3f5d4-179">Olaylar ve yol hello toodifferent hedeflerine alır, Scala içinde yazılmış örnek uygulama yayınlamayı Spark şu adresten edinilebilir [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="3f5d4-180">Merhaba tooupdate hello uygulama olay hub'ı yapılandırmanız için aşağıdaki adımları izleyin ve hello çıkış jar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="3f5d4-181">Intellij Idea başlatın ve ekran seçin hello başlatma **sürüm denetiminden kullanıma** ve ardından **Git**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="3f5d4-182">![Apache Spark örnek - Git get kaynaklardan akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark örnek - Git get kaynaklardan akış")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="3f5d4-183">Merhaba, **kopya deposu** iletişim kutusu, hello URL toohello Git deposu tooclone gelen sağlamak, hello dizin tooclone belirtin ve ardından **kopya**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="3f5d4-184">![Apache Spark örnek - Git kopya akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark örnek - Git kopya akış")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="3f5d4-185">Merhaba proje tamamen kopyalanması kadar hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="3f5d4-186">Tuşuna **Alt + 1** tooopen hello **proje görünümü**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="3f5d4-187">Merhaba aşağıdaki benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="3f5d4-188">![Apache Spark örnek - proje görünümü akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark akış örnek - proje görünümü")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="3f5d4-189">Merhaba uygulama kodu ile Java8 derlendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="3f5d4-190">tooensure bunu, **dosya**, tıklatın **proje yapısını**ve hello **proje** sekmesi, proje dil düzeyi çok ayarlandığından emin olun**8 - Lambda'lar, türü Ek açıklamalar, vb.**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="3f5d4-191">![Apache Spark örnek - kümesi derleyici akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark örnek - kümesi derleyici akış")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="3f5d4-192">Açık hello **pom.xml** ve hello Spark sürüm doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="3f5d4-193">Altında `<properties>` düğümü, aşağıdaki kod parçacığında Merhaba arayın ve hello Spark sürüm doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="3f5d4-194">Merhaba uygulaması gerektirir adlı bir bağımlılık jar **JDBC sürücüsü jar**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="3f5d4-195">Bir Azure SQL veritabanına olay Hub'ından alınan gerekli toowrite Merhaba iletileri budur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="3f5d4-196">Bu jar yükleyebilirsiniz (v4.1 veya sonrası) gelen [burada](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="3f5d4-197">Başvuru toothis jar hello proje kitaplığa ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="3f5d4-198">Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="3f5d4-199">Merhaba uygulaması açık olduğu Intellij Idea penceresinden tıklatın **dosya**, tıklatın **Proje yapısı**ve ardından **kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="3f5d4-200">Hello tıklatın Ekle simgesi (![Ekle simgesi](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), tıklatın **Java**ve ardından hello JDBC sürücüsü jar indirdiğiniz toohello konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="3f5d4-201">Merhaba istemleri tooadd hello jar dosyasını toohello projesi kitaplık izleyin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="3f5d4-202">![eksik bağımlılıkları ekleyin](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "eksik bağımlılık Kavanoz ekleme")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="3f5d4-203">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-203">Click **Apply**.</span></span>

7. <span data-ttu-id="3f5d4-204">Merhaba çıkış jar dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-204">Create hello output jar file.</span></span> <span data-ttu-id="3f5d4-205">Merhaba aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="3f5d4-206">Merhaba, **Proje yapısı** iletişim kutusu, tıklatın **yapıları** ve hello artı simgesi'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="3f5d4-207">Merhaba açılan iletişim kutusunda tıklatın **JAR**ve ardından **bağımlılıkları olan modüller gelen**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="3f5d4-208">![Apache Spark akış örnek - JAR oluşturma](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark akış örnek - JAR oluşturma")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="3f5d4-209">Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, hello üç nokta düğmesine (![üç nokta](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) hello karşı **ana sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="3f5d4-210">Merhaba, **ana sınıftan** iletişim kutusunda, hello kullanılabilir sınıfların birini seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="3f5d4-211">![Apache Spark örnek - select sınıfı jar için akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark akış örnek - jar için select sınıfı")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="3f5d4-212">Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, o hello seçeneği çok emin olun**toohello hedef JAR ayıklamak** seçilir ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="3f5d4-213">Bu, tüm bağımlılıkları olan tek bir JAR oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="3f5d4-214">![Apache Spark akış örnek - jar modüllerden oluşturma](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark akış örnek - jar modüllerden oluşturma")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="3f5d4-215">Merhaba **çıkış düzeni** sekmesi hello Maven projenin bir parçası olarak dahil tüm hello Kavanoz listeler.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="3f5d4-216">Seçebileceğiniz ve hiçbir doğrudan bağımlılık olanları üretileceği Scala uygulama hello delete hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="3f5d4-217">Biz burada oluşturma Merhaba uygulaması için kaldırdığınız dışındaki tüm sonuncu hello (**spark-akış-data-Kalıcılık-örnekleri derleme çıktı**).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="3f5d4-218">Merhaba Kavanoz toodelete seçin ve hello **silmek** simgesi (![Sil simgesi](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="3f5d4-219">![Apache Spark örnek - ayıklanan delete Kavanoz akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark örnek - ayıklanan delete Kavanoz akış")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="3f5d4-220">Emin olun **olun yapı** kutusu seçiliyse, o hello jar hello proje oluşturulmuş veya güncelleştirilmiş her zaman oluşturulan sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="3f5d4-221">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="3f5d4-222">Merhaba, **çıkış düzeni** sekmesini sağ hello hello altındaki **kullanılabilir öğeleri** kutusu, önceki toohello proje kitaplık eklenebilir hello SQL JDBC jar sahip.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="3f5d4-223">Bu toohello eklemelisiniz **çıkış düzeni** sekmesi. Merhaba jar dosyasını sağ tıklatın ve ardından **ayıklamak halinde çıkış kök**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="3f5d4-224">![Apache Spark örnek - extract bağımlılık jar akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark örnek - extract bağımlılık jar akış")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="3f5d4-225">Merhaba **çıkış düzeni** sekmesini şimdi şöyle görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="3f5d4-226">![Apache Spark örnek - son çıktı sekmesi akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark akış örnek - son çıktı sekmesi")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="3f5d4-227">Merhaba, **proje yapısını** iletişim kutusu, tıklatın **Uygula** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="3f5d4-228">Merhaba menü çubuğundaki **yapı**ve ardından **olun proje**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="3f5d4-229">Tıklatarak **derleme yapıları** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="3f5d4-230">Merhaba çıkış jar altında oluşturulan **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="3f5d4-231">![Apache Spark akış örnek - çıktı JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark akış örnek - çıktı JAR")</span><span class="sxs-lookup"><span data-stu-id="3f5d4-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="3f5d4-232">Merhaba uygulaması Livy kullanarak Spark kümesinde uzaktan çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3f5d4-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="3f5d4-233">Bu makalede, Livy toorun Merhaba Apache Spark akış uygulaması uzaktan Spark kümesinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="3f5d4-234">Nasıl toouse Livy Hdınsight Spark ile küme hakkında ayrıntılı bilgi için bkz: [gönderme işleri uzaktan tooan Apache Spark küme Azure Hdınsight'ta](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="3f5d4-235">Merhaba Spark akış uygulaması çalıştıran başlamadan önce şunları yapmalısınız vardır:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="3f5d4-236">Merhaba yerel tek başına uygulama toogenerate olayları başlatmak ve tooEvent Hub gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="3f5d4-237">Komut toodo şekilde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="3f5d4-238">Kopya hello jar akış (**spark akış-data-Kalıcılık-examples.jar**) toohello hello kümesi ile ilişkili Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="3f5d4-239">Bu hello jar erişilebilir tooLivy hale getirir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="3f5d4-240">Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bir komut satırı yardımcı programı, toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="3f5d4-241">Var olan çok diğer istemcileri tooupload verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="3f5d4-242">Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="3f5d4-243">CURL Bu uygulamalardan çalıştırdığınız hello bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="3f5d4-244">Livy uç noktaları toorun hello uzaktan işleri CURL tooinvoke hello kullanırız.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="3f5d4-245">Merhaba Spark akış uygulama tooreceive hello olayları bir Azure depolama blob'a metin olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="3f5d4-246">Bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3f5d4-247">Merhaba hello dosyasındaki parametreleri **inputBlob.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3f5d4-248">Bize hello giriş dosyası hello parametrelerinde neler olduğunu anlama:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="3f5d4-249">**Dosya** hello yolu toohello uygulama jar hello kümesi ile ilişkili hello Azure depolama hesabı üzerinde bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="3f5d4-250">**className** hello jar hello sınıfında hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="3f5d4-251">**bağımsız değişken** hello hello sınıfı tarafından gerekli bağımsız değişkenleri listesi</span><span class="sxs-lookup"><span data-stu-id="3f5d4-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="3f5d4-252">**numExecutors** uygulama yayınlamayı Spark toorun hello tarafından kullanılan çekirdek hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="3f5d4-253">Bu, her zaman en az iki kez hello olay hub'ı bölüm sayısı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="3f5d4-254">**executorMemory**, **executorCores**, **driverMemory** kullanılan parametreler gerekli tooassign kaynaklardır toohello akış uygulama.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="3f5d4-255">Parametre olarak kullanılan toocreate hello Çıkış klasörleri (EventCheckpoint, EventCount/EventCount10) gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="3f5d4-256">Uygulama yayınlamayı hello bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="3f5d4-257">Merhaba komutu çalıştırdığınızda, hello aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="3f5d4-258">Hello son satırında hello çıktı ('1'. Bu örnekte) hello toplu iş Kimliğini not edin.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="3f5d4-259">Uygulama hello tooverify çalıştırıyorsa başarıyla hello kümesi ile ilişkili Azure depolama hesabınızın bakabilir ve hello görmeniz gerekir **/EventCount/EventCount10** oluşturulan klasör.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="3f5d4-260">Bu klasör hello hello içinde belirtilen süre hello parametresi için işlenen olay sayısı yakalar BLOB'ları içermelidir **saniye içinde toplu iş aralığı**.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="3f5d4-261">Bunu KILL kadar Merhaba Spark akış uygulaması toorun devam eder.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="3f5d4-262">toodo, bu nedenle, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="3f5d4-263">Merhaba uygulamaları tooreceive hello olayları bir Azure depolama blob'a JSON olarak çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3f5d4-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="3f5d4-264">Bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3f5d4-265">Merhaba hello dosyasındaki parametreleri **inputJSON.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3f5d4-266">Merhaba, hello önceki adımda hello metin çıktısı için belirtilen benzer toowhat parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="3f5d4-267">Yeniden, parametre olarak kullanılan toocreate hello Çıkış klasörleri (EventCheckpoint, EventCount/EventCount10) gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="3f5d4-268">Uygulama yayınlamayı hello bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="3f5d4-269">Sonra hello komutunu çalıştırın, hello kümesi ile ilişkili Azure depolama hesabınızın bakabilir ve hello görmelisiniz **/EventStore10** oluşturulan klasör.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="3f5d4-270">Açık herhangi bir dosyayı önekine sahip **bölümü -** ve bir JSON biçiminde işlenen hello olayların görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="3f5d4-271">Merhaba uygulamaları tooreceive hello olayları Hive tabloya çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="3f5d4-272">toorun hello Spark akış uygulaması bir Hive akışları olayları, tablo bazı ek bileşenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="3f5d4-273">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-273">These are:</span></span>

* <span data-ttu-id="3f5d4-274">API jdo 3.2.6.jar datanucleus</span><span class="sxs-lookup"><span data-stu-id="3f5d4-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="3f5d4-275">datanucleus rdbms 3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="3f5d4-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="3f5d4-276">datanucleus çekirdek 3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="3f5d4-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="3f5d4-277">Hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="3f5d4-277">hive-site.xml</span></span>

<span data-ttu-id="3f5d4-278">Merhaba **.jar** konumunda Hdınsight Spark kümenize dosyaları kullanılabilir `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="3f5d4-279">Merhaba **hive-site.xml** şu adresten edinilebilir `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="3f5d4-280">Kullanabileceğiniz [WinScp](http://winscp.net/eng/download.php) toocopy hello küme tooyour yerel bilgisayardan bu dosyalar üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="3f5d4-281">Daha sonra bu dosyalar tooyour depolama hesabı hello kümesi ile ilişkili araçları toocopy kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="3f5d4-282">Nasıl tooupload toohello depolama hesabı dosyaları ile ilgili daha fazla bilgi için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="3f5d4-283">Merhaba dosyaları tooyour Azure depolama hesabı üzerinde kopyalandıktan sonra bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3f5d4-284">Merhaba hello dosyasındaki parametreleri **inputHive.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3f5d4-285">Merhaba, önceki adımlarda hello hello metin çıktısı için belirtilen benzer toowhat parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="3f5d4-286">Yeniden toocreate hello çıkış gerekmez klasörleri (EventCheckpoint, EventCount/EventCount10) veya hello çıktı parametreleri olarak kullanılan Hive tablosu (EventHiveTable10).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="3f5d4-287">Uygulama yayınlamayı hello bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="3f5d4-288">Bu hello Not **Kavanoz** ve **dosyaları** yolları toohello .jar dosyaları ve toohello depolama hesabı üzerinde kopyaladığınız hello hive-site.xml seçeneği içerir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="3f5d4-289">hive tablosu hello tooverify başarıyla oluşturuldu, SSH hello küme ve çalışma Hive sorguları halinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="3f5d4-290">Yönergeler için bkz: [SSH ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="3f5d4-291">SSH kullanarak bağlandıktan sonra o hello Hive tablosu komutu tooverify aşağıdaki hello çalıştırabilirsiniz **EventHiveTable10**, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="3f5d4-292">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="3f5d4-293">SEÇME sorgusu hello tablosunun tooview Merhaba içeriğine de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="3f5d4-294">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-294">You should see an output like hello following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="3f5d4-295">Merhaba uygulamaları tooreceive hello olayları bir Azure SQL veritabanı tablosuna çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="3f5d4-296">Bu adımı çalıştırmadan önce oluşturulan bir Azure SQL veritabanı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="3f5d4-297">Yönergeler için bkz: [dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="3f5d4-298">toocomplete Bu bölüm, veritabanı adı, veritabanı sunucusu adı ve parametre olarak hello veritabanı yöneticisi kimlik bilgileri değerlerine ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="3f5d4-299">Toocreate hello veritabanı tablosu ancak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="3f5d4-300">Merhaba Spark akış uygulamanın, sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="3f5d4-301">Bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3f5d4-302">Merhaba hello dosyasındaki parametreleri **inputSQL.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3f5d4-303">Uygulama hello tooverify başarıyla çalışır, toohello Azure SQL veritabanını SQL Server Management Studio'yu kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="3f5d4-304">Yönergeler için bkz: toodo [tooSQL veritabanı SQL Server Management Studio ile bağlanma](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d4-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="3f5d4-305">Bağlı toohello veritabanı olduktan sonra toohello gidebilirsiniz **EventContent** uygulama yayınlamayı hello tarafından oluşturulan tablo.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="3f5d4-306">Hızlı sorgu tooget hello veri hello tablosundan çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="3f5d4-307">Sorgu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="3f5d4-308">Çıktı benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3f5d4-308">You should see output similar toohello following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="3f5d4-309"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3f5d4-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3f5d4-310">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="3f5d4-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="3f5d4-311">Alıcı tabanlı bağlantı ve doğrudan DStream tasarımı</span><span class="sxs-lookup"><span data-stu-id="3f5d4-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="3f5d4-312">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="3f5d4-312">Scenarios</span></span>
* [<span data-ttu-id="3f5d4-313">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="3f5d4-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3f5d4-314">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3f5d4-315">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3f5d4-316">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="3f5d4-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3f5d4-317">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-317">Create and run applications</span></span>
* [<span data-ttu-id="3f5d4-318">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3f5d4-319">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3f5d4-320">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="3f5d4-320">Tools and extensions</span></span>
* [<span data-ttu-id="3f5d4-321">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="3f5d4-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3f5d4-322">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3f5d4-323">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3f5d4-324">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="3f5d4-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3f5d4-325">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5d4-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3f5d4-326">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="3f5d4-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3f5d4-327">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="3f5d4-327">Manage resources</span></span>
* [<span data-ttu-id="3f5d4-328">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="3f5d4-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3f5d4-329">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="3f5d4-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
