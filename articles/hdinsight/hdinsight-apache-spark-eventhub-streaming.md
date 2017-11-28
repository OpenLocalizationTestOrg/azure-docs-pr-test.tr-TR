---
title: "Apache Spark Azure hdınsight'ta Event Hubs ile akış kullanın | Microsoft Docs"
description: "Örnek veri akışı Azure Event Hub'ına olayları alıp göndermek sonra bu scala uygulaması kullanarak Hdınsight Spark kümesinde konusunda akış bir Apache Spark oluşturun."
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
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="980f6-104">Apache Spark akış: Hdınsight'ta Spark ile Azure Event Hubs işlem verilerini küme</span><span class="sxs-lookup"><span data-stu-id="980f6-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="980f6-105">Bu makalede, aşağıdaki adımları içerir örnek akış bir Apache Spark oluşturun:</span><span class="sxs-lookup"><span data-stu-id="980f6-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="980f6-106">Bir Azure olay Hub'ına iletileri almak için bir tek başına uygulamayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="980f6-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="980f6-107">İki farklı yaklaşım ile gerçek zamanlı Azure Hdınsight'ta Spark kümesinde çalışan bir uygulama kullanarak olay Hub'ından iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="980f6-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="980f6-108">Verileri farklı saklama sistemlerine kalıcı hale getirmek için analitik komut zincirleri akış yapı veya anında verilerinden öngörü edinme.</span><span class="sxs-lookup"><span data-stu-id="980f6-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="980f6-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="980f6-109">Prerequisites</span></span>

* <span data-ttu-id="980f6-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="980f6-110">An Azure subscription.</span></span> <span data-ttu-id="980f6-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="980f6-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="980f6-112">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="980f6-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="980f6-113">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="980f6-114">Spark akış kavramları</span><span class="sxs-lookup"><span data-stu-id="980f6-114">Spark Streaming concepts</span></span>

<span data-ttu-id="980f6-115">Spark akış ayrıntılı bir açıklaması için bkz: [Apache Spark genel bakış akış](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="980f6-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="980f6-116">Hdınsight, Azure üzerinde bir Spark kümesi için aynı akış özellikleri getirir.</span><span class="sxs-lookup"><span data-stu-id="980f6-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="980f6-117">Bu çözüm ne yapar?</span><span class="sxs-lookup"><span data-stu-id="980f6-117">What does this solution do?</span></span>

<span data-ttu-id="980f6-118">Bu makaledeki örnek akış Spark oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="980f6-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="980f6-119">Bir akış olayların alacak bir Azure Event Hub oluşturun.</span><span class="sxs-lookup"><span data-stu-id="980f6-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="980f6-120">Olaylar oluşturur ve Azure Event Hub'ına iter yerel tek başına uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="980f6-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="980f6-121">Bu örnek uygulama yayımlanma [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="980f6-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="980f6-122">Çeşitli veri işleme/analiz gerçekleştirmek ve bir akış uygulaması Azure olay Hub'ından akış olayları okur bir Spark kümesi üzerinde uzaktan çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="980f6-123">Bir Azure olay hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="980f6-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="980f6-124">Oturum [Azure Portal](https://ms.portal.azure.com), tıklatıp **yeni** en üst ekranın sol.</span><span class="sxs-lookup"><span data-stu-id="980f6-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="980f6-125">**Nesnelerin İnterneti**’ne ve ardından **Event Hubs**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="980f6-126">![Örnek Spark akış Create event hub](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "örnek Spark akış Create event hub")</span><span class="sxs-lookup"><span data-stu-id="980f6-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="980f6-127">**Ad alanı oluştur** dikey penceresine bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="980f6-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="980f6-128">Fiyatlandırma Katmanı (temel veya standart) seçin.</span><span class="sxs-lookup"><span data-stu-id="980f6-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="980f6-129">Ayrıca, bir Azure aboneliği, kaynak grubu ve kaynağın oluşturulacağı konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="980f6-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="980f6-130">Ad alanını oluşturmak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="980f6-131">![Bir örnek Spark akış için olay hub'ı ad](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "örnek Spark akış için bir olay hub'ı adı belirtin")</span><span class="sxs-lookup"><span data-stu-id="980f6-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="980f6-132">Aynı seçmelisiniz **konumu** gecikme süresini ve maliyetleri azaltmak hdınsight'ta Apache Spark kümeniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="980f6-133">Event Hubs ad alanı listesinde yeni oluşturulan ad alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="980f6-134">Ad alanı dikey penceresinde tıklayın **Event Hubs**ve ardından **+ olay hub'ı** yeni bir olay hub'ı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="980f6-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="980f6-135">![Örnek Spark akış Create event hub](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "örnek Spark akış Create event hub")</span><span class="sxs-lookup"><span data-stu-id="980f6-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="980f6-136">Olay Hub'ınız için bir ad yazın, bölüm sayısı 10 ve ileti bekletme 1 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="980f6-137">Geri kalan varsayılan olarak bırakın ve ardından Biz bu çözüm iletilerinde arşivleme değil **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="980f6-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="980f6-138">![Olay hub'ı ayrıntılarını sağlamak için örnek akış Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "için Spark akış örnek olay hub'ı ayrıntılarını sağlayın")</span><span class="sxs-lookup"><span data-stu-id="980f6-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="980f6-139">Yeni oluşturulan olay hub'ı olay Hub dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="980f6-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="980f6-140">![Olay hub'ı görüntülemek için örnek akış Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "örnek akış Spark için Görünüm olay hub'ı")</span><span class="sxs-lookup"><span data-stu-id="980f6-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="980f6-141">Ad alanı dikey penceresine (ilgili Olay Hub’ı dikey penceresine değil) geri dönerek **Paylaşılan erişim ilkeleri** ve ardından **RootManageSharedAccessKey** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="980f6-142">![Olay hub'ı ilkeler için örnek akış Spark ayarlama](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "örnek akış Spark için Event Hub'ı ayarlamak ilkeleri")</span><span class="sxs-lookup"><span data-stu-id="980f6-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="980f6-143">Kopyalamak için Kopyala düğmesini tıklatın **RootManageSharedAccessKey** birincil anahtar ve bağlantı dizesini panoya.</span><span class="sxs-lookup"><span data-stu-id="980f6-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="980f6-144">Bu öğreticide daha sonra kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="980f6-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="980f6-145">![Olay hub'ı İlkesi anahtarları için örnek akış Spark görüntülemek](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "görünüm olay hub'ı ilke anahtarları için Spark akış örneği")</span><span class="sxs-lookup"><span data-stu-id="980f6-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="980f6-146">Azure Event kullanan bir örnek Scala uygulamaları Hub'ına iletileri gönder</span><span class="sxs-lookup"><span data-stu-id="980f6-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="980f6-147">Bu bölümdeki olayların bir akış oluşturur ve Azure Event Hub için daha önce oluşturduğunuz gönderen bir tek başına yerel Scala uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="980f6-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="980f6-148">Bu uygulama github'da kullanılabilir [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="980f6-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="980f6-149">Adımlar burada bu GitHub deposunu zaten çatallanmış varsayar.</span><span class="sxs-lookup"><span data-stu-id="980f6-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="980f6-150">Bu uygulamayı çalıştırdığınız bilgisayarda yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="980f6-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="980f6-151">Oracle Java Geliştirme Seti.</span><span class="sxs-lookup"><span data-stu-id="980f6-151">Oracle Java Development kit.</span></span> <span data-ttu-id="980f6-152">Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="980f6-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="980f6-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="980f6-153">Apache Maven.</span></span> <span data-ttu-id="980f6-154">Buradan indirebilirsiniz [burada](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="980f6-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="980f6-155">Maven yüklemeye yönelik yönergeleri [burada](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="980f6-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="980f6-156">Bir komut istemi açın ve uygulama oluşturmak için aşağıdaki komutu çalıştırın ve örnek Scala uygulama için GitHub deposuna kopyalanabilir konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="980f6-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="980f6-157">Uygulama için çıktı jar **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, altında oluşturulan **/target** dizin.</span><span class="sxs-lookup"><span data-stu-id="980f6-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="980f6-158">Bu makalenin sonraki bölümlerinde bu JAR eksiksiz çözüm sınamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="980f6-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="980f6-159">Olay Hub'ından bir Spark küme içinde iletileri almak için uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="980f6-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="980f6-160">Biz, Spark akış ve Azure Event Hubs, alıcı tabanlı bağlantısı ve doğrudan-DStream tabanlı bağlantısı bağlanmak için iki yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="980f6-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="980f6-161">Doğrudan-DStream tabanlı 2017 Oca üzerinde sunulan 2.0.3 serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="980f6-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="980f6-162">Daha fazla kullanıcı olduğu gibi özgün alıcı tabanlı bağlantıyı değiştirmek için beklenen ve verimli kaynak.</span><span class="sxs-lookup"><span data-stu-id="980f6-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="980f6-163">Daha fazla ayrıntı bulunan [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="980f6-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="980f6-164">Doğrudan DStream yalnızca Spark 2.0 + destekler.</span><span class="sxs-lookup"><span data-stu-id="980f6-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="980f6-165">Spark eventhubs bağlayıcı bağımlılık uygulamaları derleme</span><span class="sxs-lookup"><span data-stu-id="980f6-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="980f6-166">Spark EventHubs hazırlama sürümünü de Github'da yayımlar.</span><span class="sxs-lookup"><span data-stu-id="980f6-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="980f6-167">Spark EventHubs hazırlama sürümünü kullanmak için ilk adım GitHub kaynak deposu pom.xml için şu girdiyi ekleyerek belirtmektir:</span><span class="sxs-lookup"><span data-stu-id="980f6-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

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

<span data-ttu-id="980f6-168">Yayın öncesi sürüm yapılacak projenize aşağıdaki bağımlılığı daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="980f6-169">Maven bağımlılığı</span><span class="sxs-lookup"><span data-stu-id="980f6-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="980f6-170">SBT bağımlılık</span><span class="sxs-lookup"><span data-stu-id="980f6-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="980f6-171">Doğrudan DStream bağlantı</span><span class="sxs-lookup"><span data-stu-id="980f6-171">Direct DStream Connection</span></span>

<span data-ttu-id="980f6-172">İçinde doğrudan DStream kullanan örnekler içeren bir önceden derlenmiş jar dosyasını karşıdan [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="980f6-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="980f6-173">Kaynak kodu kullanılabilir üç örnekler jar dosyasını içeren [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="980f6-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="980f6-174">Alma [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) bir örnek olarak:</span><span class="sxs-lookup"><span data-stu-id="980f6-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="980f6-175">Yukarıdaki örnekte, `eventhubParameters` parametreleri tek bir EventHubs örnek özeldir ve ona geçirmek zorunda `createDirectStreams` bir olay hub'ları ad alanı için doğrudan DStream nesne eşleme oluşturur API.</span><span class="sxs-lookup"><span data-stu-id="980f6-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="980f6-176">Doğrudan DStream nesnesi üzerinde Spark akış API çerçevesi tarafından sağlanan herhangi bir DStream API'yi çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="980f6-177">Bu örnekte, biz son 3 mikro toplu aralıkları her sözcüğün sıklığını hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="980f6-178">Alıcı tabanlı bağlantı</span><span class="sxs-lookup"><span data-stu-id="980f6-178">Receiver-based Connection</span></span>

<span data-ttu-id="980f6-179">Örnek uygulama olaylarını alır ve farklı hedefler yönlendirmek, Scala içinde yazılmış akış Spark şu adresten edinilebilir [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="980f6-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="980f6-180">Olay hub'ı yapılandırmanızı için uygulamayı güncelleştir ve çıktı jar oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="980f6-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="980f6-181">Intellij Idea başlatın ve başlatma ekranından seçin **sürüm denetiminden kullanıma** ve ardından **Git**.</span><span class="sxs-lookup"><span data-stu-id="980f6-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="980f6-182">![Apache Spark örnek - Git get kaynaklardan akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark örnek - Git get kaynaklardan akış")</span><span class="sxs-lookup"><span data-stu-id="980f6-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="980f6-183">İçinde **kopya deposu** iletişim kutusunda, kopyası, için kopyalayın ve ardından dizin belirlemek için Git deposu URL'sini sağlayın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="980f6-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="980f6-184">![Apache Spark örnek - Git kopya akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark örnek - Git kopya akış")</span><span class="sxs-lookup"><span data-stu-id="980f6-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="980f6-185">Proje tamamen kopyalanması kadar istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="980f6-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="980f6-186">Tuşuna **Alt + 1** açmak için **proje görünümü**.</span><span class="sxs-lookup"><span data-stu-id="980f6-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="980f6-187">Aşağıdakine benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="980f6-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="980f6-188">![Apache Spark örnek - proje görünümü akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark akış örnek - proje görünümü")</span><span class="sxs-lookup"><span data-stu-id="980f6-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="980f6-189">Uygulama kodu ile Java8 derlendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="980f6-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="980f6-190">Bunu sağlamak için **dosya**, tıklatın **Proje yapısı**ve **proje** sekmesinde, dil düzeyi ayarlandığından emin projeyi **8 - Lambda'lar, türü Ek açıklamalar, vb.**.</span><span class="sxs-lookup"><span data-stu-id="980f6-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="980f6-191">![Apache Spark örnek - kümesi derleyici akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark örnek - kümesi derleyici akış")</span><span class="sxs-lookup"><span data-stu-id="980f6-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="980f6-192">Açık **pom.xml** ve Spark sürüm doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="980f6-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="980f6-193">Altında `<properties>` düğümü için aşağıdaki kod parçacığında arayın ve Spark sürüm doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="980f6-194">Uygulama adı verilen bir bağımlılık jar gerektiriyor **JDBC sürücüsü jar**.</span><span class="sxs-lookup"><span data-stu-id="980f6-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="980f6-195">Bu, bir Azure SQL veritabanına olay Hub'ından alınan iletileri yazmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="980f6-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="980f6-196">Bu jar yükleyebilirsiniz (v4.1 veya sonrası) gelen [burada](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="980f6-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="980f6-197">Proje Kitaplığı'nda bu jar başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="980f6-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="980f6-198">Aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="980f6-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="980f6-199">Sahip olduğu açık uygulama Intellij Idea penceresinden tıklatın **dosya**, tıklatın **proje yapısını**ve ardından **kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="980f6-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="980f6-200">Ekle simgesini tıklatın (![Ekle simgesi](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), tıklatın **Java**ve ardından JDBC sürücüsü jar indirdiğiniz konuma gidin.</span><span class="sxs-lookup"><span data-stu-id="980f6-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="980f6-201">Proje kitaplığına jar dosyasına eklemek için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="980f6-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="980f6-202">![eksik bağımlılıkları ekleyin](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "eksik bağımlılık Kavanoz ekleme")</span><span class="sxs-lookup"><span data-stu-id="980f6-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="980f6-203">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-203">Click **Apply**.</span></span>

7. <span data-ttu-id="980f6-204">Çıktı jar dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="980f6-204">Create the output jar file.</span></span> <span data-ttu-id="980f6-205">Aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="980f6-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="980f6-206">İçinde **proje yapısını** iletişim kutusu, tıklatın **yapıları** artı simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="980f6-207">Açılan iletişim kutusundan tıklatın **JAR**ve ardından **bağımlılıkları olan modüller gelen**.</span><span class="sxs-lookup"><span data-stu-id="980f6-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="980f6-208">![Apache Spark akış örnek - JAR oluşturma](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark akış örnek - JAR oluşturma")</span><span class="sxs-lookup"><span data-stu-id="980f6-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="980f6-209">İçinde **oluşturma JAR modüllerden** iletişim kutusunda, üç nokta işaretine (![üç nokta](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) karşı **ana sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="980f6-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="980f6-210">İçinde **ana sınıftan** iletişim kutusu, kullanılabilir sınıfların birini seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="980f6-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="980f6-211">![Apache Spark örnek - select sınıfı jar için akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark akış örnek - jar için select sınıfı")</span><span class="sxs-lookup"><span data-stu-id="980f6-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="980f6-212">İçinde **oluşturma JAR modüllerden** iletişim kutusunda, olduğundan emin olun seçeneği **hedef JAR ayıklamak** seçilir ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="980f6-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="980f6-213">Bu, tüm bağımlılıkları olan tek bir JAR oluşturur.</span><span class="sxs-lookup"><span data-stu-id="980f6-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="980f6-214">![Apache Spark akış örnek - jar modüllerden oluşturma](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark akış örnek - jar modüllerden oluşturma")</span><span class="sxs-lookup"><span data-stu-id="980f6-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="980f6-215">**Çıkış düzeni** sekmesi Maven projenin bir parçası olarak dahil tüm Kavanoz listeler.</span><span class="sxs-lookup"><span data-stu-id="980f6-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="980f6-216">Seçin ve üretileceği olanları Sil Scala uygulama doğrudan hiçbir bağımlılık içeriyor.</span><span class="sxs-lookup"><span data-stu-id="980f6-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="980f6-217">Biz burada oluşturma uygulama için tüm sonuncu kaldırabilirsiniz (**spark-akış-data-Kalıcılık-örnekleri derleme çıktı**).</span><span class="sxs-lookup"><span data-stu-id="980f6-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="980f6-218">Silin ve ardından Kavanoz seçin **silmek** simgesi (![Sil simgesi](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="980f6-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="980f6-219">![Apache Spark örnek - ayıklanan delete Kavanoz akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark örnek - ayıklanan delete Kavanoz akış")</span><span class="sxs-lookup"><span data-stu-id="980f6-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="980f6-220">Emin olun **olun yapı** kutusu seçiliyse, proje oluşturulmuş veya güncelleştirilmiş her zaman jar oluşturulur sağlar.</span><span class="sxs-lookup"><span data-stu-id="980f6-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="980f6-221">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="980f6-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="980f6-222">İçinde **çıkış düzeni** sağ ekranın alt kısmındaki sekme **kullanılabilir öğeleri** kutusunda proje Kitaplığı'na daha önce eklediğiniz SQL JDBC jar sahip.</span><span class="sxs-lookup"><span data-stu-id="980f6-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="980f6-223">Bu eklemelisiniz **çıkış düzeni** sekmesi. Jar dosyasını sağ tıklatın ve ardından **ayıklamak halinde çıkış kök**.</span><span class="sxs-lookup"><span data-stu-id="980f6-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="980f6-224">![Apache Spark örnek - extract bağımlılık jar akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark örnek - extract bağımlılık jar akış")</span><span class="sxs-lookup"><span data-stu-id="980f6-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="980f6-225">**Çıkış düzeni** sekmesini şimdi şöyle görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="980f6-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="980f6-226">![Apache Spark örnek - son çıktı sekmesi akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark akış örnek - son çıktı sekmesi")</span><span class="sxs-lookup"><span data-stu-id="980f6-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="980f6-227">İçinde **proje yapısını** iletişim kutusu, tıklatın **Uygula** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="980f6-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="980f6-228">Menü çubuğundaki **yapı**ve ardından **olun proje**.</span><span class="sxs-lookup"><span data-stu-id="980f6-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="980f6-229">Tıklatarak **derleme yapıları** jar oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="980f6-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="980f6-230">Çıktı jar altında oluşturulan **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="980f6-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="980f6-231">![Apache Spark akış örnek - çıktı JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark akış örnek - çıktı JAR")</span><span class="sxs-lookup"><span data-stu-id="980f6-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="980f6-232">Uygulamayı uzaktan Livy kullanarak Spark kümesinde çalıştırın</span><span class="sxs-lookup"><span data-stu-id="980f6-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="980f6-233">Bu makalede bir Spark kümesinde uzaktan uygulama yayınlamayı Apache Spark çalıştırmak için Livy kullanın.</span><span class="sxs-lookup"><span data-stu-id="980f6-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="980f6-234">Livy Hdınsight Spark kümesinde ile kullanma hakkında ayrıntılı bilgi için bkz: [gönderme işleri uzaktan bir Apache Spark küme Azure Hdınsight'ta](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="980f6-235">Uygulama yayınlamayı Spark çalıştıran başlamadan önce şunları yapmalısınız vardır:</span><span class="sxs-lookup"><span data-stu-id="980f6-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="980f6-236">Olay Hub'ına gönderilen ve olaylar oluşturmak için yerel tek başına uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="980f6-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="980f6-237">Bunu yapmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="980f6-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="980f6-238">Akış jar kopyalayın (**spark akış-data-Kalıcılık-examples.jar**) kümesi ile ilişkili Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="980f6-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="980f6-239">Bu jar Livy için erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="980f6-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="980f6-240">Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bunu yapmak için bir komut satırı yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="980f6-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="980f6-241">Verileri yüklemek için kullanabileceğiniz diğer istemcilerin çok vardır.</span><span class="sxs-lookup"><span data-stu-id="980f6-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="980f6-242">Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="980f6-243">CURL Bu uygulamalardan çalıştırdığınız bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="980f6-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="980f6-244">İşlerini uzaktan çalıştırmak için Livy uç noktaları çağrılacak CURL kullanırız.</span><span class="sxs-lookup"><span data-stu-id="980f6-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="980f6-245">Bir Azure Storage Blobuna metin olarak içine olaylarını almak için uygulama yayınlamayı Spark çalıştırın</span><span class="sxs-lookup"><span data-stu-id="980f6-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="980f6-246">Bir komut istemi açın, CURL yüklediğiniz dizine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="980f6-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="980f6-247">Parametreler dosyasında **inputBlob.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="980f6-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="980f6-248">Bize giriş dosyası parametrelerinde neler olduğunu anlama:</span><span class="sxs-lookup"><span data-stu-id="980f6-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="980f6-249">**Dosya** kümesi ile ilişkili Azure depolama hesabı üzerinde uygulama jar dosyasını yoludur.</span><span class="sxs-lookup"><span data-stu-id="980f6-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="980f6-250">**className** jar sınıfında adıdır.</span><span class="sxs-lookup"><span data-stu-id="980f6-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="980f6-251">**bağımsız değişken** sınıfı tarafından gerekli bağımsız değişkenleri listesi</span><span class="sxs-lookup"><span data-stu-id="980f6-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="980f6-252">**numExecutors** tarafından Spark akış uygulamayı çalıştırmak için kullanılan çekirdek sayısı.</span><span class="sxs-lookup"><span data-stu-id="980f6-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="980f6-253">Bu, her zaman en az iki kez olay hub'ı bölüm sayısı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="980f6-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="980f6-254">**executorMemory**, **executorCores**, **driverMemory** gerekli kaynakları akış uygulamaya atamak için kullanılan parametreler bulunur.</span><span class="sxs-lookup"><span data-stu-id="980f6-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="980f6-255">Parametre olarak kullanılan çıkış klasörler (EventCheckpoint, EventCount/EventCount10) oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="980f6-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="980f6-256">Akış uygulama bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="980f6-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="980f6-257">Komutu çalıştırdığınızda, aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="980f6-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="980f6-258">Çıkış ('1'. Bu örnekte) son satırında toplu iş kimliği not edin.</span><span class="sxs-lookup"><span data-stu-id="980f6-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="980f6-259">Uygulamanın başarıyla çalıştığını doğrulamak için Azure depolama hesabınızın kümeyle ilişkili bakabilirsiniz ve görmelisiniz **/EventCount/EventCount10** oluşturulan klasör.</span><span class="sxs-lookup"><span data-stu-id="980f6-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="980f6-260">Bu klasör, belirtilen süre içinde parametresi için işlenen olay sayısı yakalar BLOB'ları içermelidir **saniye içinde toplu iş aralığı**.</span><span class="sxs-lookup"><span data-stu-id="980f6-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="980f6-261">Uygulama yayınlamayı Spark, KILL kadar çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="980f6-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="980f6-262">Bunu yapmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="980f6-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="980f6-263">Bir Azure Storage blobu JSON olarak içine olaylarını almak için uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="980f6-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="980f6-264">Bir komut istemi açın, CURL yüklediğiniz dizine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="980f6-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="980f6-265">Parametreler dosyasında **inputJSON.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="980f6-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="980f6-266">Parametreleri ne için metin çıktısı önceki adımda belirttiğiniz için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="980f6-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="980f6-267">Yeniden, parametre olarak kullanılan çıkış klasörler (EventCheckpoint, EventCount/EventCount10) oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="980f6-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="980f6-268">Akış uygulama bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="980f6-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="980f6-269">Komutu çalıştırın, kümeyle ilişkili Azure depolama hesabınızın bakabilir ve görmeniz gerekir sonra **/EventStore10** oluşturulan klasör.</span><span class="sxs-lookup"><span data-stu-id="980f6-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="980f6-270">Açık herhangi bir dosyayı önekine sahip **bölümü -** ve bir JSON biçiminde işlenen olayların görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="980f6-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="980f6-271">Hive tabloya olaylarını almak için uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="980f6-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="980f6-272">Bir Hive tabloya olayları akışları uygulama yayınlamayı Spark çalıştırmak için bazı ek bileşenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="980f6-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="980f6-273">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="980f6-273">These are:</span></span>

* <span data-ttu-id="980f6-274">API jdo 3.2.6.jar datanucleus</span><span class="sxs-lookup"><span data-stu-id="980f6-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="980f6-275">datanucleus rdbms 3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="980f6-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="980f6-276">datanucleus çekirdek 3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="980f6-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="980f6-277">Hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="980f6-277">hive-site.xml</span></span>

<span data-ttu-id="980f6-278">**.Jar** konumunda Hdınsight Spark kümenize dosyaları kullanılabilir `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="980f6-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="980f6-279">**Hive-site.xml** şu adresten edinilebilir `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="980f6-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="980f6-280">Kullanabileceğiniz [WinScp](http://winscp.net/eng/download.php) bu dosyalar, yerel bilgisayarınıza kümeden kopyalamak için.</span><span class="sxs-lookup"><span data-stu-id="980f6-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="980f6-281">Ardından, bu dosyalar üzerinde kümeyle ilişkili depolama hesabınıza kopyalamak için araçları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="980f6-282">Depolama hesabı dosyaları karşıya yükleme hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="980f6-283">Azure depolama hesabınıza dosyalar kopyalandıktan sonra bir komut istemi açın, CURL yüklediğiniz dizine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="980f6-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="980f6-284">Parametreler dosyasında **inputHive.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="980f6-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="980f6-285">Parametreleri ne için metin çıktısı, önceki adımda belirttiğiniz için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="980f6-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="980f6-286">Yeniden Çıkış klasörleri (EventCheckpoint, EventCount/EventCount10) veya çıkış oluşturma gerekmez Hive tablosu (EventHiveTable10) parametreleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="980f6-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="980f6-287">Akış uygulama bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="980f6-287">The streaming application creates them for you.</span></span> <span data-ttu-id="980f6-288">Unutmayın **Kavanoz** ve **dosyaları** seçenek .jar dosya ve depolama hesabına üzerinden kopyalanan hive-site.xml yollara içerir.</span><span class="sxs-lookup"><span data-stu-id="980f6-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="980f6-289">Hive tablosu başarıyla oluşturulduğunu doğrulamak için Küme ve çalışma Hive sorguları SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="980f6-290">Yönergeler için bkz: [SSH ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="980f6-291">SSH kullanarak bağlandıktan sonra Hive tablosu doğrulamak için aşağıdaki komutu çalıştırabilirsiniz **EventHiveTable10**, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="980f6-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="980f6-292">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="980f6-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="980f6-293">SEÇME sorgusu tablosunun içeriğini görüntülemek için de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="980f6-294">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="980f6-294">You should see an output like the following:</span></span>

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


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="980f6-295">Bir Azure SQL veritabanı tablosuna olaylarını almak için uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="980f6-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="980f6-296">Bu adımı çalıştırmadan önce oluşturulan bir Azure SQL veritabanı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="980f6-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="980f6-297">Yönergeler için bkz: [dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="980f6-298">Bu bölümde tamamlamak için değerleri veritabanı adı, veritabanı sunucusu adını ve veritabanı yöneticisi kimlik bilgileri için parametre olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="980f6-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="980f6-299">Veritabanı tablosu oluştur gerekmez.</span><span class="sxs-lookup"><span data-stu-id="980f6-299">You do not need to create the database table though.</span></span> <span data-ttu-id="980f6-300">Uygulama yayınlamayı Spark, sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="980f6-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="980f6-301">Bir komut istemi açın, CURL yüklediğiniz dizine gidin ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="980f6-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="980f6-302">Parametreler dosyasında **inputSQL.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="980f6-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="980f6-303">Uygulamanın başarıyla çalıştığını doğrulamak için SQL Server Management Studio'yu kullanarak Azure SQL veritabanına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="980f6-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="980f6-304">Bunun hakkında daha fazla yönerge için bkz: [SQL Server Management Studio ile SQL veritabanına bağlanma](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="980f6-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="980f6-305">Veritabanına bağlandıktan sonra gidebilirsiniz **EventContent** akış uygulaması tarafından oluşturulmuş tablo.</span><span class="sxs-lookup"><span data-stu-id="980f6-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="980f6-306">Tablodan veri almak için hızlı bir sorgu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980f6-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="980f6-307">Aşağıdaki sorguyu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="980f6-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="980f6-308">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="980f6-308">You should see output similar to the following:</span></span>

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


## <span data-ttu-id="980f6-309"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="980f6-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="980f6-310">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="980f6-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="980f6-311">Alıcı tabanlı bağlantı ve doğrudan DStream tasarımı</span><span class="sxs-lookup"><span data-stu-id="980f6-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="980f6-312">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="980f6-312">Scenarios</span></span>
* [<span data-ttu-id="980f6-313">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="980f6-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="980f6-314">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="980f6-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="980f6-315">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="980f6-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="980f6-316">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="980f6-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="980f6-317">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="980f6-317">Create and run applications</span></span>
* [<span data-ttu-id="980f6-318">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="980f6-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="980f6-319">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="980f6-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="980f6-320">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="980f6-320">Tools and extensions</span></span>
* [<span data-ttu-id="980f6-321">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="980f6-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="980f6-322">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="980f6-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="980f6-323">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="980f6-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="980f6-324">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="980f6-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="980f6-325">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="980f6-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="980f6-326">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="980f6-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="980f6-327">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="980f6-327">Manage resources</span></span>
* [<span data-ttu-id="980f6-328">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="980f6-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="980f6-329">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="980f6-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
