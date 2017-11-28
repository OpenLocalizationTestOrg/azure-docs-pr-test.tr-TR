---
title: "Apache Storm ve HBase ile algılayıcı verilerini aaaAnalyze | Microsoft Docs"
description: "Bilgi nasıl tooconnect tooApache Storm ile bir sanal ağ. İle D3.js görselleştirmek ve Storm HBase tooprocess algılayıcı verilerle bir olay hub'ı kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="798bf-104">Apache Storm, olay hub'ı ve (Hadoop) hdınsight'ta HBase ile algılayıcı verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="798bf-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="798bf-105">Bilgi toouse Azure olay hub'ı Hdınsight tooprocess algılayıcı verileri üzerinde Apache Storm nasıl.</span><span class="sxs-lookup"><span data-stu-id="798bf-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="798bf-106">Merhaba veri sonra Hdınsight üzerinde Apache HBase içine depolanır ve D3.js kullanarak görselleştirilen.</span><span class="sxs-lookup"><span data-stu-id="798bf-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="798bf-107">Bu belgede kullanılan hello Azure Resource Manager şablonu gösteren nasıl toocreate bir kaynak grubunda birden çok Azure kaynağı.</span><span class="sxs-lookup"><span data-stu-id="798bf-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="798bf-108">Merhaba şablon bir Azure sanal ağı, iki Hdınsight kümesi (Storm ve HBase) ve Azure Web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="798bf-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="798bf-109">Gerçek zamanlı web Panosu bir node.js uygulaması otomatik olarak dağıtılan toohello web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="798bf-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="798bf-110">Bu belge ve bu belgedeki örnek Hello bilgileri, Hdınsight sürüm 3.6 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="798bf-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="798bf-111">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="798bf-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="798bf-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="798bf-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="798bf-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="798bf-113">Prerequisites</span></span>

* <span data-ttu-id="798bf-114">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="798bf-114">An Azure subscription.</span></span>
* <span data-ttu-id="798bf-115">[Node.js](http://nodejs.org/): geliştirme ortamınızı yerel olarak kullanılan toopreview hello web Panosu.</span><span class="sxs-lookup"><span data-stu-id="798bf-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="798bf-116">[Java ve hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): toodevelop hello Storm topolojisini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="798bf-117">[Maven](http://maven.apache.org/what-is-maven.html): kullanılan toobuild ve derleme hello projesi.</span><span class="sxs-lookup"><span data-stu-id="798bf-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="798bf-118">[Git](http://git-scm.com/): kullanılan toodownload Merhaba projeyi github'dan.</span><span class="sxs-lookup"><span data-stu-id="798bf-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="798bf-119">Bir **SSH** istemci: tooconnect toohello Linux tabanlı Hdınsight kümeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="798bf-120">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="798bf-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="798bf-121">Mevcut bir Hdınsight kümesine gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="798bf-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="798bf-122">Bu belgedeki Hello adımlar kaynakları aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="798bf-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="798bf-123">Bir Azure sanal ağı</span><span class="sxs-lookup"><span data-stu-id="798bf-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="798bf-124">Hdınsight kümesinde bir Storm (Linux tabanlı iki alt düğümleri)</span><span class="sxs-lookup"><span data-stu-id="798bf-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="798bf-125">Hdınsight kümesinde bir HBase (Linux tabanlı iki alt düğümleri)</span><span class="sxs-lookup"><span data-stu-id="798bf-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="798bf-126">Merhaba web Pano barındıran bir Azure Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="798bf-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="798bf-127">Mimari</span><span class="sxs-lookup"><span data-stu-id="798bf-127">Architecture</span></span>

![mimarisi diyagramı](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="798bf-129">Bu örnek bileşenleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="798bf-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="798bf-130">**Azure Event Hubs**: algılayıcı toplanan verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="798bf-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="798bf-131">**Hdınsight üzerinde Storm**: olay Hub'ından veri gerçek zamanlı işlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="798bf-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="798bf-132">**Hdınsight'ta HBase**: Storm tarafından işlendikten sonra kalıcı NoSQL veri deposu için veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="798bf-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="798bf-133">**Azure sanal ağ hizmeti**: Hdınsight kümelerinde hello Hdınsight üzerinde Storm ve HBase arasında güvenli iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="798bf-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="798bf-134">Bir sanal ağ hello Java HBase istemci API kullanılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="798bf-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="798bf-135">Merhaba HBase kümeleri için ortak ağ geçidi üzerinden açık değil.</span><span class="sxs-lookup"><span data-stu-id="798bf-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="798bf-136">Yükleme HBase ve Storm kümeleri aynı sanal ağ sağlar hello içine hello Storm kümesi (veya başka bir sistem hello sanal ağ üzerinde) toodirectly istemci API kullanarak HBase erişim.</span><span class="sxs-lookup"><span data-stu-id="798bf-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="798bf-137">**Pano Web sitesi**: Gerçek zamanlı veri grafikleri bir örnek Pano.</span><span class="sxs-lookup"><span data-stu-id="798bf-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="798bf-138">Merhaba Web sitesi Node.js içinde uygulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="798bf-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="798bf-139">[Socket.IO](http://socket.io/) hello Storm topolojisini hello Web sitesi arasındaki gerçek zamanlı iletişim için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="798bf-140">Socket.IO iletişim için bir uygulama ayrıntılarını kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="798bf-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="798bf-141">Ham WebSockets veya SignalR gibi tüm iletişimler çerçevesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="798bf-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="798bf-142">[D3.js](http://d3js.org/) toohello Web gönderilen kullanılan toograph hello veriler.</span><span class="sxs-lookup"><span data-stu-id="798bf-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="798bf-143">Hiçbir desteklenen yöntem toocreate bir Hdınsight kümesi için Storm ve HBase olarak iki küme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="798bf-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="798bf-144">Merhaba topoloji verileri olay Hub'ından hello kullanarak okur [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) sınıfı ve hello kullanarak HBase yazma verisine [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) sınıf.</span><span class="sxs-lookup"><span data-stu-id="798bf-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="798bf-145">Merhaba Web sitesiyle iletişim kullanarak gerçekleştirilir [Socket.IO client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="798bf-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="798bf-146">Diyagram aşağıdaki hello hello topoloji hello düzenini açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="798bf-146">hello following diagram explains hello layout of hello topology:</span></span>

![Topoloji diyagramı](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="798bf-148">Bu diyagramda, hello topoloji Basitleştirilmiş görünümüdür.</span><span class="sxs-lookup"><span data-stu-id="798bf-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="798bf-149">Her bileşen örneği, olay hub'ınızdaki her bir bölümü için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="798bf-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="798bf-150">Bu örnekler hello kümedeki hello düğümler arasında dağıtılır ve veri aralarında gibi yönlendirilir:</span><span class="sxs-lookup"><span data-stu-id="798bf-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="798bf-151">Merhaba spout toohello ayrıştırıcı yükü dengelenmiş verilerdir.</span><span class="sxs-lookup"><span data-stu-id="798bf-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="798bf-152">Merhaba ayrıştırıcı toohello Pano ve HBase verilerini cihaz Kimliğine göre gruplandırılmış, böylece her zaman aynı aygıt iletilerden hello toohello akış aynı bileşeni.</span><span class="sxs-lookup"><span data-stu-id="798bf-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="798bf-153">Topoloji bileşenleri</span><span class="sxs-lookup"><span data-stu-id="798bf-153">Topology components</span></span>

* <span data-ttu-id="798bf-154">**Event Hubs Spout**: Merhaba spout 0.10.0 Apache Storm sürümünün parçası olarak sağlanan ve daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="798bf-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="798bf-155">Bu örnekte kullanılan hello olay hub'ı spout Hdınsight kümesi sürüm 3.5 veya 3.6 Storm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="798bf-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="798bf-156">**ParserBolt.java**: Merhaba spout'un yayılan hello verilerinin ham JSON ve bazen birden fazla olay aynı anda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="798bf-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="798bf-157">Bu Cıvata tarafından hello yayılan hello veriler spout ve hello JSON ileti ayrıştırır okur.</span><span class="sxs-lookup"><span data-stu-id="798bf-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="798bf-158">Merhaba Cıvata sonra birden çok alan içeren bir tanımlama grubu hello veri yayar.</span><span class="sxs-lookup"><span data-stu-id="798bf-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="798bf-159">**DashboardBolt.java**: Bu bileşen nasıl toouse hello Java toosend verileri gerçek zamanlı toohello web Pano için Socket.IO istemci kitaplığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="798bf-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="798bf-160">**Hayır-hbase.yaml**: Merhaba yerel modda çalışırken kullanılan topoloji tanımı.</span><span class="sxs-lookup"><span data-stu-id="798bf-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="798bf-161">HBase bileşenleri kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="798bf-161">It does not use HBase components.</span></span>
* <span data-ttu-id="798bf-162">**hbase.yaml ile**: Merhaba hello topoloji Merhaba kümede çalışırken kullanılan topoloji tanımı.</span><span class="sxs-lookup"><span data-stu-id="798bf-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="798bf-163">HBase bileşenlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-163">It does use HBase components.</span></span>
* <span data-ttu-id="798bf-164">**dev.Properties**: Merhaba hello olay hub'ı spout, HBase Cıvata ve Panosu bileşenleri için yapılandırma bilgilerini.</span><span class="sxs-lookup"><span data-stu-id="798bf-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="798bf-165">Ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="798bf-165">Prepare your environment</span></span>

<span data-ttu-id="798bf-166">Bu örneğini kullanmadan önce hangi hello Storm topolojisinin okur bir Azure Event Hub oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="798bf-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="798bf-167">Olay hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="798bf-167">Configure Event Hub</span></span>

<span data-ttu-id="798bf-168">Olay hub'ı hello veri bu örneğin kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="798bf-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="798bf-169">Aşağıdaki adımları toocreate bir Event Hub'hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="798bf-170">Merhaba gelen [Azure portal](https://portal.azure.com)seçin **+ yeni** -> **nesnelerin interneti** -> **olay hub'ları**.</span><span class="sxs-lookup"><span data-stu-id="798bf-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="798bf-171">Merhaba, **oluşturma Namespace** bölümünde, hello aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="798bf-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="798bf-172">Girin bir **adı** hello ad alanı için.</span><span class="sxs-lookup"><span data-stu-id="798bf-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="798bf-173">Fiyatlandırma katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="798bf-173">Select a pricing tier.</span></span> <span data-ttu-id="798bf-174">**Temel** Bu örnek için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="798bf-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="798bf-175">Select hello Azure **abonelik** toouse.</span><span class="sxs-lookup"><span data-stu-id="798bf-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="798bf-176">Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="798bf-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="798bf-177">Select hello **konumu** hello olay hub'ı için.</span><span class="sxs-lookup"><span data-stu-id="798bf-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="798bf-178">Seçin **PIN toodashboard**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="798bf-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="798bf-179">Merhaba oluşturma işlemi tamamlandığında hello ad alanınız için olay hub'ları bilgileri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="798bf-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="798bf-180">Buradan, seçin **+ olay hub'ı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="798bf-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="798bf-181">Merhaba, **Event Hub'ı oluşturma** bölümünde, bir ad girin **sensordata**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="798bf-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="798bf-182">Merhaba diğer alanları hello varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="798bf-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="798bf-183">Merhaba olay hub'larından görüntülemek, ad alanı için select **olay hub'ları**.</span><span class="sxs-lookup"><span data-stu-id="798bf-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="798bf-184">Select hello **sensordata** girişi.</span><span class="sxs-lookup"><span data-stu-id="798bf-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="798bf-185">Merhaba sensordata Event Hub ' seçin **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="798bf-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="798bf-186">Kullanım hello **+ Ekle** ilkelere bağlantı tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="798bf-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="798bf-187">İlke adı</span><span class="sxs-lookup"><span data-stu-id="798bf-187">Policy name</span></span> | <span data-ttu-id="798bf-188">Talepleri</span><span class="sxs-lookup"><span data-stu-id="798bf-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="798bf-189">cihazlar</span><span class="sxs-lookup"><span data-stu-id="798bf-189">devices</span></span> | <span data-ttu-id="798bf-190">Gönder</span><span class="sxs-lookup"><span data-stu-id="798bf-190">Send</span></span> |
    | <span data-ttu-id="798bf-191">Storm</span><span class="sxs-lookup"><span data-stu-id="798bf-191">storm</span></span> | <span data-ttu-id="798bf-192">Dinleme</span><span class="sxs-lookup"><span data-stu-id="798bf-192">Listen</span></span> |

1. <span data-ttu-id="798bf-193">Her iki ilkeyi seçin ve hello Not **birincil anahtar** değeri.</span><span class="sxs-lookup"><span data-stu-id="798bf-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="798bf-194">Sonraki adımlarda hem ilkeleri için hello değer gerekir.</span><span class="sxs-lookup"><span data-stu-id="798bf-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="798bf-195">İndirme ve başlangıç projesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="798bf-195">Download and configure hello project</span></span>

<span data-ttu-id="798bf-196">Toodownload Merhaba projeyi Github'dan aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="798bf-197">Merhaba komutu tamamlandıktan sonra aşağıdaki dizin yapısını hello vardır:</span><span class="sxs-lookup"><span data-stu-id="798bf-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="798bf-198">Bu belgede, bu örnekteki hello kodunun toofull ayrıntılarını geçmez.</span><span class="sxs-lookup"><span data-stu-id="798bf-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="798bf-199">Ancak, hello kodu tam olarak geçersiz kılınan.</span><span class="sxs-lookup"><span data-stu-id="798bf-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="798bf-200">Olay Hub'ı Aç hello gelen tooconfigure hello proje tooread `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` dosya ve izleyerek, olay hub'ı bilgi toohello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="798bf-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="798bf-201">Derleme ve yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="798bf-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="798bf-202">Merhaba topolojisi kullanarak yerel olarak çalışan bir Storm geliştirme ortamını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="798bf-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="798bf-203">Daha fazla bilgi için bkz: [bir Storm geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) Apache.org.</span><span class="sxs-lookup"><span data-stu-id="798bf-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="798bf-204">Bir Windows geliştirme ortamını kullanıyorsanız, alabileceğiniz bir `java.io.IOException` çalışırken hello topoloji yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="798bf-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="798bf-205">Bu durumda, Hdınsight toorunning hello topolojisini taşıyın.</span><span class="sxs-lookup"><span data-stu-id="798bf-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="798bf-206">Test etmeden önce hello Pano tooview hello çıktı hello topolojisinin başlatmalı ve Event Hub'ında veri toostore oluşturur.</span><span class="sxs-lookup"><span data-stu-id="798bf-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="798bf-207">Bu topoloji Hello HBase bileşeni, yerel olarak test edilirken etkin değil.</span><span class="sxs-lookup"><span data-stu-id="798bf-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="798bf-208">Merhaba Java API hello HBase kümesi için dış hello hello kümeleri içeren Azure Virtual Network erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="798bf-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="798bf-209">Merhaba web uygulamasını Başlat</span><span class="sxs-lookup"><span data-stu-id="798bf-209">Start hello web application</span></span>

1. <span data-ttu-id="798bf-210">Bir komut istemi açın ve dizinleri çok`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="798bf-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="798bf-211">Merhaba web uygulama tarafından gerek duyulan komutu tooinstall hello bağımlılıklar aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="798bf-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="798bf-212">Komut toostart hello web uygulama aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="798bf-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="798bf-213">Metin aşağıdaki ileti benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="798bf-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="798bf-214">Bir web tarayıcısı açın ve girin `http://localhost:3000/` hello adresi olarak.</span><span class="sxs-lookup"><span data-stu-id="798bf-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="798bf-215">Aşağıdaki görüntü bir sayfa benzer toohello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="798bf-215">A page similar toohello following image is displayed:</span></span>
   
    ![Web Panosu](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="798bf-217">Bu komut istemini açık bırakın.</span><span class="sxs-lookup"><span data-stu-id="798bf-217">Leave this command prompt open.</span></span> <span data-ttu-id="798bf-218">Test sonra Ctrl-C toostop hello web sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="798bf-219">Veri oluştur</span><span class="sxs-lookup"><span data-stu-id="798bf-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="798bf-220">herhangi bir platformda kullanılabilir hello bu bölümdeki adımları Node.js kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="798bf-221">Merhaba diğer dil örnekler için bkz: `SendEvents` dizin.</span><span class="sxs-lookup"><span data-stu-id="798bf-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="798bf-222">Yeni istemi, kabuk veya terminal açın ve dizinleri çok değiştirin`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="798bf-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="798bf-223">Merhaba uygulama tarafından gerek duyulan tooinstall hello bağımlılıkları hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="798bf-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="798bf-224">Açık hello `app.js` dosyasını bir metin düzenleyicisinde ve hello daha önce aldığınız olay hub'ı bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="798bf-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="798bf-225">Bu örnekte, kullandığınız varsayılır `sensordata` olay Hub'ınızı hello adından farklı.</span><span class="sxs-lookup"><span data-stu-id="798bf-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="798bf-226">Ve `devices` sahip hello İlkesi hello adından farklı bir `Send` talep.</span><span class="sxs-lookup"><span data-stu-id="798bf-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="798bf-227">Komut tooinsert yeni girişler Event Hub'ındaki aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="798bf-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="798bf-228">Merhaba veri içeren birkaç satırlık çıktı tooEvent Hub gönderilen bakın:</span><span class="sxs-lookup"><span data-stu-id="798bf-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="798bf-229">Oluşturun ve hello topoloji başlatın</span><span class="sxs-lookup"><span data-stu-id="798bf-229">Build and start hello topology</span></span>

1. <span data-ttu-id="798bf-230">Yeni bir komut istemi açın ve dizinleri çok`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="798bf-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="798bf-231">toobuild ve paket topoloji Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="798bf-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="798bf-232">toostart yerel mod topolojisinde Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="798bf-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="798bf-233">`--local`Merhaba topoloji yerel modunda başlatır.</span><span class="sxs-lookup"><span data-stu-id="798bf-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="798bf-234">`--filter`kullandığı hello `dev.properties` hello topoloji tanımı'nda dosya toopopulate parametreleri.</span><span class="sxs-lookup"><span data-stu-id="798bf-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="798bf-235">`resources/no-hbase.yaml`kullandığı hello `no-hbase.yaml` topoloji tanımı.</span><span class="sxs-lookup"><span data-stu-id="798bf-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="798bf-236">Başladıktan sonra hello topoloji girişleri olay Hub'ından okur ve onları yerel makine üzerinde çalışan toohello Pano gönderir.</span><span class="sxs-lookup"><span data-stu-id="798bf-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="798bf-237">Merhaba web Pano görüntü aşağıdaki benzer toohello görünen satırlarını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="798bf-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![verilerle Panosu](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="798bf-239">Merhaba Pano çalışırken hello kullan `node app.js` hello önceki komuttan adımları toosend yeni veri tooEvent hub.</span><span class="sxs-lookup"><span data-stu-id="798bf-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="798bf-240">Merhaba sıcaklık değerleri rastgele oluşturulur çünkü hello grafik sıcaklık tooshow büyük değişiklikleri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="798bf-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="798bf-241">Hello olmalıdır **hdınsight-eventhub-örnek/SendEvents/Nodejs** hello kullanırken dizin `node app.js` komutu.</span><span class="sxs-lookup"><span data-stu-id="798bf-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="798bf-242">Bu hello Pano güncelleştirmeleri, Ctrl + C kullanarak Dur hello topolojisi doğruladıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="798bf-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="798bf-243">Ctrl + C toostop hello yerel web sunucusu de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="798bf-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="798bf-244">Bir Storm ve HBase kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="798bf-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="798bf-245">Merhaba adımları bölümüne kullanması durumunda bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) toocreate hello sanal ağda bir Azure sanal ağı ve bir Storm ve HBase kümesi.</span><span class="sxs-lookup"><span data-stu-id="798bf-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="798bf-246">Hello şablonu ayrıca bir Azure Web uygulaması oluşturur ve hello panonun bir kopyasını uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="798bf-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="798bf-247">Bir sanal ağ Hello Storm kümesi üzerinde çalışan hello topoloji hello HBase Java API kullanarak hello HBase kümesi ile doğrudan iletişim kurabilmesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="798bf-248">Bu belgede kullanılan hello Resource Manager şablonu ortak blob kapsayıcısında bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="798bf-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="798bf-249">Düğme toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure portal'ın aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="798bf-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="798bf-250">Merhaba gelen **özel dağıtım** bölümünde, aşağıdaki değerleri hello girin:</span><span class="sxs-lookup"><span data-stu-id="798bf-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Hdınsight parametreleri](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="798bf-252">**Temel küme adı**: Bu değer hello Storm ve HBase kümeleri için hello temel adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="798bf-253">Örneğin, **abc** adlı bir Storm kümesi oluşturur **storm abc** ve adlı bir HBase kümesi **hbase abc**.</span><span class="sxs-lookup"><span data-stu-id="798bf-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="798bf-254">**Oturum açma kullanıcı adı küme**: hello Storm ve HBase kümeleri için hello yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="798bf-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="798bf-255">**Oturum açma parolası küme**: hello Storm ve HBase kümeleri için hello yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="798bf-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="798bf-256">**SSH kullanıcı adı**: hello Storm ve HBase kümeleri için SSH kullanıcı toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="798bf-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="798bf-257">**SSH parolası**: hello SSH kullanıcı hello Storm ve HBase kümeleri için başlangıç parolası.</span><span class="sxs-lookup"><span data-stu-id="798bf-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="798bf-258">**Konum**: hello kümeleri oluşturulan hello bölgesi.</span><span class="sxs-lookup"><span data-stu-id="798bf-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="798bf-259">Tıklatın **Tamam** toosave hello parametreleri.</span><span class="sxs-lookup"><span data-stu-id="798bf-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="798bf-260">Kullanım hello **Temelleri** bölümünde toocreate bir kaynak grubu veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="798bf-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="798bf-261">Merhaba, **kaynak grubu konumu** açılır menüsünde, select hello aynı konuma Merhaba seçtiğinizde **konumu** hello parametresinde **ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="798bf-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="798bf-262">Merhaba hüküm ve koşulları okuyun ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.</span><span class="sxs-lookup"><span data-stu-id="798bf-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="798bf-263">Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="798bf-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="798bf-264">Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="798bf-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="798bf-265">Merhaba kaynakları oluşturduktan sonra hello kaynak grubu hakkında bilgi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="798bf-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Merhaba vnet ve kümeler için kaynak grubu](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="798bf-267">Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **storm BASENAME** ve **hbase BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="798bf-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="798bf-268">Bu adları toohello kümeleri bağlanırken bir sonraki adımda kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="798bf-269">Aynı zamanda hello Pano sitenin adını hello Not olan **basename Pano**.</span><span class="sxs-lookup"><span data-stu-id="798bf-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="798bf-270">Bu değer, bu belgenin sonraki bölümlerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="798bf-271">Merhaba Pano Cıvata yapılandırın</span><span class="sxs-lookup"><span data-stu-id="798bf-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="798bf-272">toosend veri toohello Pano, bir web uygulaması dağıtılan hello satırında aşağıdaki hello değiştirmelisiniz `dev.properties`dosyası:</span><span class="sxs-lookup"><span data-stu-id="798bf-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="798bf-273">Değişiklik `http://localhost:3000` çok`http://BASENAME-dashboard.azurewebsites.net` ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="798bf-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="798bf-274">Değiştir **BASENAME** hello önceki adımda sağlanan hello temel ada sahip.</span><span class="sxs-lookup"><span data-stu-id="798bf-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="798bf-275">Daha önce tooselect hello panoyu ve görünüm hello URL oluşturulan hello kaynak grubuna de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="798bf-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="798bf-276">Merhaba HBase tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="798bf-276">Create hello HBase table</span></span>

<span data-ttu-id="798bf-277">HBase toostore verileri, biz öncelikle bir tablo oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="798bf-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="798bf-278">Storm toowrite için gereken kaynakları önceden oluşturmak, bir Storm topolojisinin içinde çalışırken toocreate kaynaklardan çalışırken birden çok örneğinde neden olabileceğinden toocreate hello aynı kaynak.</span><span class="sxs-lookup"><span data-stu-id="798bf-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="798bf-279">Merhaba topoloji dışındaki Hello kaynaklar oluşturun ve okuma/yazma ve analizi için Storm kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="798bf-280">Merhaba SSH kullanıcı ve küme oluşturma sırasında toohello şablonu sağlanan parola kullanarak SSH tooconnect toohello HBase kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="798bf-281">Örneğin, hello kullanarak bağlanma `ssh` komutunu kullanma sözdizimi aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="798bf-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="798bf-282">Değiştir `sshuser` hello SSH kullanıcı adı ile Merhaba küme oluştururken verdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="798bf-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="798bf-283">Değiştir `clustername` hello HBase kümesi ada sahip.</span><span class="sxs-lookup"><span data-stu-id="798bf-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="798bf-284">Merhaba SSH oturumundan hello HBase Kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="798bf-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="798bf-285">Merhaba Kabuk yüklendikten sonra gördüğünüz bir `hbase(main):001:0>` istemi.</span><span class="sxs-lookup"><span data-stu-id="798bf-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="798bf-286">Hello ifadesini HBase Kabuğu komut toocreate bir tablo toostore hello algılayıcı verilerini aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="798bf-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="798bf-287">Hello tablosunun komutu aşağıdaki hello kullanılarak oluşturulup oluşturulmadığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="798bf-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="798bf-288">Aşağıdaki örnek, hello tabloda 0 satır olduğunu belirten bilgi benzer toohello döndürür.</span><span class="sxs-lookup"><span data-stu-id="798bf-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="798bf-289">Girin `exit` tooexit hello HBase Kabuğu:</span><span class="sxs-lookup"><span data-stu-id="798bf-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="798bf-290">Merhaba HBase Cıvata yapılandırın</span><span class="sxs-lookup"><span data-stu-id="798bf-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="798bf-291">toowrite tooHBase hello Storm kümeden hello yapılandırma ayrıntılarını, HBase kümesi ile Merhaba HBase Cıvata sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="798bf-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="798bf-292">Örnekler tooretrieve hello Zookeeper çekirdek HBase kümesi için aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="798bf-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="798bf-293">Değiştir `your_HDInsight_cluster_name` Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="798bf-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="798bf-294">Merhaba yükleme hakkında daha fazla bilgi için `jq` yardımcı programı, bkz: [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="798bf-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="798bf-295">İstendiğinde, hello Hdınsight yönetici oturum açma hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="798bf-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="798bf-296">Değiştir ' your_HDInsight_cluster_name Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="798bf-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="798bf-297">İstendiğinde, hello Hdınsight yönetici oturum açma hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="798bf-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="798bf-298">Bu örnek, Azure PowerShell gerektirir.</span><span class="sxs-lookup"><span data-stu-id="798bf-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="798bf-299">Azure PowerShell kullanma hakkında daha fazla bilgi için bkz: [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="798bf-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="798bf-300">Bu örnekler tarafından döndürülen hello bilgi metnini izleyen benzer toohello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="798bf-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="798bf-301">Bu bilgiler, Storm toocommunicate ile Merhaba HBase kümesi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="798bf-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="798bf-302">Merhaba değiştirme `dev.properties` dosya ve hello Zookeeper çekirdek bilgi toohello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="798bf-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="798bf-303">, Paketi, derleme ve hello çözüm tooHDInsight dağıtma</span><span class="sxs-lookup"><span data-stu-id="798bf-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="798bf-304">Geliştirme ortamınızı adımları toodeploy hello Storm topolojisini toohello storm kümesi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="798bf-305">Merhaba gelen `TemperatureMonitor` dizin kullanım hello aşağıdakiler komut tooperform yeni bir yapı ve projenizden JAR paketi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="798bf-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="798bf-306">Bu komut adlı bir dosya oluşturur `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `hedef ' projenizin dizin.</span><span class="sxs-lookup"><span data-stu-id="798bf-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="798bf-307">Kullanım scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` ve `dev.properties` dosyaları tooyour Storm kümesi.</span><span class="sxs-lookup"><span data-stu-id="798bf-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="798bf-308">Örneğin, aşağıdaki Hello yerine `sshuser` hello küme oluştururken verdiğiniz hello SSH kullanıcı ile ve `clustername` Storm kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="798bf-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="798bf-309">İstendiğinde, hello SSH kullanıcı için hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="798bf-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="798bf-310">Tooupload hello dosyaları bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="798bf-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="798bf-311">Merhaba kullanma hakkında daha fazla bilgi için `scp` ve `ssh` komutları, Hdınsight ile bkz [Hdınsight ile SSH kullanma](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="798bf-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="798bf-312">Hello dosya karşıya yüklendikten sonra SSH kullanarak toohello Storm kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="798bf-313">Değiştir `sshuser` hello SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="798bf-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="798bf-314">Değiştir `clustername` hello Storm kümesi ada sahip.</span><span class="sxs-lookup"><span data-stu-id="798bf-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="798bf-315">toostart topoloji Merhaba, hello SSH oturumundan komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="798bf-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="798bf-316">`--remote`Merhaba topoloji toohello toohello supervisor hello küme düğümünde IT Nimbus hizmet gönderir.</span><span class="sxs-lookup"><span data-stu-id="798bf-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="798bf-317">`--filter`kullandığı hello `dev.properties` hello topoloji tanımı'nda dosya toopopulate parametreleri.</span><span class="sxs-lookup"><span data-stu-id="798bf-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="798bf-318">`-R /with-hbase.yaml`kullandığı hello `with-hbase.yaml` hello paketindeki topolojisi.</span><span class="sxs-lookup"><span data-stu-id="798bf-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="798bf-319">Merhaba topoloji başlatıldıktan sonra sonra kullanım hello Azure üzerinde yayımlanan bir tarayıcı toohello Web sitesini açın `node app.js` komutu toosend veri tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="798bf-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="798bf-320">Merhaba web Pano güncelleştirme toodisplay hello bilgileri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="798bf-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![pano](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="798bf-322">HBase verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="798bf-322">View HBase data</span></span>

<span data-ttu-id="798bf-323">Aşağıdaki adımları tooconnect tooHBase hello kullanın ve hello veri toohello tablo yazılmış emin olun:</span><span class="sxs-lookup"><span data-stu-id="798bf-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="798bf-324">SSH tooconnect toohello HBase kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="798bf-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="798bf-325">Değiştir `sshuser` hello SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="798bf-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="798bf-326">Değiştir `clustername` hello HBase kümesi ada sahip.</span><span class="sxs-lookup"><span data-stu-id="798bf-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="798bf-327">Merhaba SSH oturumundan hello HBase Kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="798bf-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="798bf-328">Merhaba Kabuk yüklendikten sonra gördüğünüz bir `hbase(main):001:0>` istemi.</span><span class="sxs-lookup"><span data-stu-id="798bf-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="798bf-329">Merhaba tablodan satırları görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="798bf-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="798bf-330">Bu komut metnini izleyen, hello tabloda veri olduğunu belirten bilgi benzer toohello döndürür.</span><span class="sxs-lookup"><span data-stu-id="798bf-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="798bf-331">Bu tarama işlemi hello tablodan en fazla 10 satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="798bf-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="798bf-332">Kümelerinizi Sil</span><span class="sxs-lookup"><span data-stu-id="798bf-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="798bf-333">aynı anda toodelete hello kümeleri, depolama ve web uygulaması bunları içeren hello kaynak grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="798bf-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="798bf-334">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="798bf-334">Next steps</span></span>

<span data-ttu-id="798bf-335">Storm topolojileri Hdınsight ile daha fazla örnekleri için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="798bf-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="798bf-336">Apache Storm hakkında daha fazla bilgi için bkz: Merhaba [Apache Storm](https://storm.incubator.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="798bf-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="798bf-337">Hdınsight'ta HBase hakkında daha fazla bilgi için bkz: Merhaba [Hdınsight genel bakış ile HBase](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="798bf-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="798bf-338">Merhaba Socket.IO hakkında daha fazla bilgi için bkz: [Socket.IO](http://socket.io/) site.</span><span class="sxs-lookup"><span data-stu-id="798bf-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="798bf-339">D3.js hakkında daha fazla bilgi için bkz: [D3.js - veri güdümlü belgeleri](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="798bf-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="798bf-340">Java topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Apache Storm için geliştirme Java topolojileri](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="798bf-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="798bf-341">.NET topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="798bf-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
