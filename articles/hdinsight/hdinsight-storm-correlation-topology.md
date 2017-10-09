---
title: "Hdınsight üzerinde Storm ve HBase ile zamanla aaaCorrelate olayları"
description: "Bilgi nasıl Hdınsight üzerinde Storm ve HBase kullanarak farklı zamanlarda gelmesini toocorrelate olaylar."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="ae0dd-103">Farklı zamanlarda geldiğinde olayları ilişkilendirmenize Storm ve HBase kullanma</span><span class="sxs-lookup"><span data-stu-id="ae0dd-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="ae0dd-104">Apache Storm ile kalıcı veri deposu kullanarak, farklı zamanlarda gelmesini veri girişi ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="ae0dd-105">Örneğin, bir kullanıcı oturumu toocalculate için oturum açma ve kapatma olayları nasıl uzun hello oturum bağlama devam.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="ae0dd-106">Bu belgede, bilgi nasıl toocreate kullanıcı oturumları için oturum açma ve kapatma olayları izler ve hello süresini hello oturumunun hesaplar temel bir Storm C# topolojisi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="ae0dd-107">Merhaba topolojisi HBase kalıcı veri deposu olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="ae0dd-108">HBase tooperform Toplu sorguları hello geçmiş verileri tooproduce ek Öngörüler üzerinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="ae0dd-109">Örneğin, kaç kullanıcı oturumlarını başlatıldı veya belirli bir süre içinde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae0dd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ae0dd-110">Prerequisites</span></span>

* <span data-ttu-id="ae0dd-111">Hdınsight için Visual Studio Araçları, Visual Studio ve hello.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="ae0dd-112">Daha fazla bilgi için bkz: [hello Hdınsight araçları Visual Studio için kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ae0dd-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="ae0dd-113">Hdınsight üzerinde Apache Storm küme (Windows tabanlı).</span><span class="sxs-lookup"><span data-stu-id="ae0dd-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="ae0dd-114">28/10/2016 sonrasında oluşturulan Linux tabanlı Storm kümeleri üzerinde SCP.NET topolojileri destekleniyorsa hello HBase SDK 28/10/2016 itibariyle kullanılabilir .NET paketi için Linux tabanlı Hdınsight üzerinde düzgün çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="ae0dd-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="ae0dd-115">Hdınsight kümesi üzerinde Apache HBase (Linux veya Windows tabanlı).</span><span class="sxs-lookup"><span data-stu-id="ae0dd-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ae0dd-116">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae0dd-117">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ae0dd-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ae0dd-118">[Java](https://java.com) 1,7 veya geliştirme ortamınız üzerinde daha büyük.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="ae0dd-119">Gönderilen toohello Hdınsight kümesi olduğunda Java kullanılan toopackage hello topolojisi olur.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="ae0dd-120">Merhaba **JAVA_HOME** Java içeren ortam değişkeni gereken noktası toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="ae0dd-121">Merhaba **%JAVA_HOME%/bin** directory hello yolunda olması gerekir</span><span class="sxs-lookup"><span data-stu-id="ae0dd-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="ae0dd-122">Mimari</span><span class="sxs-lookup"><span data-stu-id="ae0dd-122">Architecture</span></span>

![Merhaba topoloji aracılığıyla hello veri akışı diyagramı](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="ae0dd-124">Olayları bağıntı ortak bir tanımlayıcı için hello olay kaynağı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="ae0dd-125">For example, bir kullanıcı kimliği, oturum kimliği veya diğer veri parçası a) benzersiz ve (b) dahil tüm gönderilen veriler tooStorm olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="ae0dd-126">Bu örnek, bir oturum kimliği bir GUID değeri toorepresent kullanır</span><span class="sxs-lookup"><span data-stu-id="ae0dd-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="ae0dd-127">Bu örnekte, iki Hdınsight kümeleri oluşur:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="ae0dd-128">HBase: geçmiş verileri kalıcı veri deposu</span><span class="sxs-lookup"><span data-stu-id="ae0dd-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="ae0dd-129">Storm: tooingest gelen veri kullanılan</span><span class="sxs-lookup"><span data-stu-id="ae0dd-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="ae0dd-130">Merhaba veri rastgele hello Storm topolojisini tarafından oluşturulan ve aşağıdaki öğelerindeki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="ae0dd-131">Oturum kimliği: her oturuma benzersiz olarak tanımlayan bir GUID</span><span class="sxs-lookup"><span data-stu-id="ae0dd-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="ae0dd-132">Olay: bir başlangıç veya bitiş olayı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-132">Event: a START or END event.</span></span> <span data-ttu-id="ae0dd-133">Bu örnekte, başlangıç her zaman son önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="ae0dd-134">Süresi: Merhaba olay hello zamanı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="ae0dd-135">Bu veriler işlenir ve HBase depolanır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="ae0dd-136">Storm topolojisi</span><span class="sxs-lookup"><span data-stu-id="ae0dd-136">Storm topology</span></span>

<span data-ttu-id="ae0dd-137">Bir oturum başlatıldığında bir **Başlat** olay hello topolojisi tarafından alınır ve tooHBase oturum.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="ae0dd-138">Zaman bir **son** olayı alındığında, hello topoloji alır hello **Başlat** olay ve hello iki olaylar arasındaki süreyi hello hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="ae0dd-139">Bu **süresi** değeri HBase sonra hello birlikte depolanır **son** olay bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae0dd-140">Bu topoloji hello temel düzeni gösterir, ancak bir üretim çözüm senaryoları aşağıdaki Merhaba tootake tasarım gerekir:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="ae0dd-141">Sıralama dışında gelen olayları</span><span class="sxs-lookup"><span data-stu-id="ae0dd-141">Events arriving out of order</span></span>
> * <span data-ttu-id="ae0dd-142">Yinelenen olay</span><span class="sxs-lookup"><span data-stu-id="ae0dd-142">Duplicate events</span></span>
> * <span data-ttu-id="ae0dd-143">Bırakılan olayları</span><span class="sxs-lookup"><span data-stu-id="ae0dd-143">Dropped events</span></span>

<span data-ttu-id="ae0dd-144">Merhaba örnek topoloji bileşenleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="ae0dd-145">Session.cs: bir kullanıcı oturumunu Başlat zaman ve ne kadar süreyle hello oturum lasts bir rastgele oturum kimliği oluşturarak benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="ae0dd-146">Spout.cs: 100 oturum oluşturur, başlangıç olayı yayar, her oturum için hello rastgele zaman aşımı bekler ve bitiş olayı yayar.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="ae0dd-147">Ardından dönüştürür oturumları toogenerate yenilerini sona erdi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="ae0dd-148">HBaseLookupBolt.cs: HBase oturum bilgi hello oturum kimliği toolook kullanır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="ae0dd-149">Bitiş Olayı işlendiğinde hello karşılık gelen başlangıç olayı bulur ve hello süresini hello oturumunun hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="ae0dd-150">HBaseBolt.cs: HBase bilgileri depolar.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="ae0dd-151">TypeHelper.cs: okuma / yazma tooHBase türü dönüştürme işlemine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="ae0dd-152">HBase şema</span><span class="sxs-lookup"><span data-stu-id="ae0dd-152">HBase schema</span></span>

<span data-ttu-id="ae0dd-153">İçinde HBase, hello veriler ile Merhaba şema/ayarları aşağıdaki tabloda saklanır:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="ae0dd-154">Satır anahtarını: hello oturum kimliği için bu tablodaki satırları hello anahtar olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="ae0dd-155">Sütun ailesi: hello aile adı olan 'cf'.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="ae0dd-156">Bu serideki depolanan sütunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="ae0dd-157">olay: başlangıç veya bitiş.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-157">event: START or END.</span></span>

  * <span data-ttu-id="ae0dd-158">saat: hello zaman olay hello milisaniye cinsinden.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="ae0dd-159">süre: Merhaba başlangıç ve bitiş olayı arasındaki uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="ae0dd-160">SÜRÜMLER: hello 'cf' ailesi her satır tooretain 5 sürümleri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ae0dd-161">Günlük için belirli satır anahtarını depolanan önceki değerlerin sürümleridir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="ae0dd-162">Varsayılan olarak, HBase, yalnızca bir satır en son sürümünü hello hello değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="ae0dd-163">Bu durumda, hello aynı satır her bir satır sürümü hello zaman damgası değeri tarafından tanımlanan tüm olayları (başlatma, End) için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="ae0dd-164">Sürümleri için belirli bir kimliği günlüğe kaydedilen olayları bir geçmiş görünümünü sağlar</span><span class="sxs-lookup"><span data-stu-id="ae0dd-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="ae0dd-165">Merhaba projenizi indirin</span><span class="sxs-lookup"><span data-stu-id="ae0dd-165">Download hello project</span></span>

<span data-ttu-id="ae0dd-166">Merhaba örnek proje adresinden yüklenebilir [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="ae0dd-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="ae0dd-167">Bu yükleme, C# projeleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="ae0dd-168">CorrelationTopology: rastgele kullanıcı oturumları için başlangıç ve bitiş olayları yayar C# Storm topolojisini.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="ae0dd-169">Her oturum arasındaki 1 ve 5 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="ae0dd-170">SessionInfo: Merhaba HBase tablo oluşturur ve örnek sorguları saklı oturum verilerini tooreturn bilgilerini sağlayan C# konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="ae0dd-171">Merhaba tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae0dd-171">Create hello table</span></span>

1. <span data-ttu-id="ae0dd-172">Açık hello **SessionInfo** Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="ae0dd-173">İçinde **Çözüm Gezgini**, sağ hello **SessionInfo** proje ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Seçili özellikleriyle menüsünün ekran görüntüsü](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="ae0dd-175">Seçin **ayarları**, sonra kümesi hello aşağıdaki değerler:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="ae0dd-176">HBaseClusterURL: hello URL tooyour HBase kümesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="ae0dd-177">Örneğin, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="ae0dd-178">HBaseClusterUserName: kümeniz Merhaba yönetici/HTTP kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="ae0dd-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="ae0dd-179">HBaseClusterPassword: hello hello yönetici/HTTP kullanıcı hesabının parolasını</span><span class="sxs-lookup"><span data-stu-id="ae0dd-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="ae0dd-180">HBaseTableName: Bu örnekle hello tablo toouse hello adı</span><span class="sxs-lookup"><span data-stu-id="ae0dd-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="ae0dd-181">HBaseTableColumnFamily: hello sütun ailesi adı</span><span class="sxs-lookup"><span data-stu-id="ae0dd-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Ayarları iletişim kutusu görüntüsü](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="ae0dd-183">Merhaba çözümü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-183">Run hello solution.</span></span> <span data-ttu-id="ae0dd-184">İstendiğinde, hello 'c' anahtar toocreate hello tablosunda HBase kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="ae0dd-185">Derleme ve hello Storm topolojisini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ae0dd-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="ae0dd-186">Açık hello **CorrelationTopology** Visual Studio'da çözüm.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="ae0dd-187">İçinde **Çözüm Gezgini**, sağ hello **CorrelationTopology** proje ve Özellikler'i seçin.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="ae0dd-188">Merhaba Özellikler penceresinde seçin **ayarları** ve bu proje için hello yapılandırma değerlerini girin.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="ae0dd-189">Merhaba ilk 5 olan hello tarafından kullanılan aynı değerleri hello **SessionInfo** proje:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="ae0dd-190">HBaseClusterURL: hello URL tooyour HBase kümesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="ae0dd-191">Örneğin, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="ae0dd-192">HBaseClusterUserName: kümeniz Merhaba yönetici/HTTP kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="ae0dd-193">HBaseClusterPassword: hello Yöneticisi/HTTP kullanıcı hesabı hello parola.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="ae0dd-194">HBaseTableName: Bu örnekle hello tablo toouse hello adı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="ae0dd-195">Bu değer aynı hello olduğu hello SessionInfo projesinde kullanılan tablo adı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="ae0dd-196">HBaseTableColumnFamily: hello sütun ailesi adı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="ae0dd-197">Bu değer aynı hello olan sütun ailesi hello SessionInfo projesinde kullanılan adı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ae0dd-198">Tarafından kullanılan hello adlarını Hello varsayılan değerler olarak hello HBaseTableColumnNames, değiştirmeyin **SessionInfo** tooretrieve veri.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="ae0dd-199">Merhaba özellikleri kaydedin, sonra Merhaba projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="ae0dd-200">İçinde **Çözüm Gezgini**, hello projesine sağ tıklatın ve **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="ae0dd-201">İstenirse, Azure aboneliğinizin hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Merhaba görüntüsü gönderme toostorm menü öğesi](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="ae0dd-203">Merhaba, **gönderme topoloji** iletişim, bu topolojiyle toodeploy istediğiniz select hello Storm kümesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ae0dd-204">Merhaba ilk kez bir topoloji göndermek, birkaç saniye tooretrieve hello Hdınsight kümelerinizi adını sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="ae0dd-205">Merhaba topoloji gönderilen ve karşıya toohello küme silindikten sonra hello **Storm topoloji görünümü** açar ve topoloji çalıştıran hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="ae0dd-206">toorefresh hello veri, select hello **CorrelationTopology** ve hello hello Yenile düğmesini kullanın hello sayfasının sağ üst.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Merhaba topoloji görünümü görüntüsü](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="ae0dd-208">Merhaba topoloji bir veri üreterek başladığında hello değerinde hello **Emitted** sütun artırır.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ae0dd-209">Merhaba, **Storm topoloji görünümü** yok otomatik olarak açmak, kullanın hello adımları tooopen onu:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="ae0dd-210">İçinde **Çözüm Gezgini**, genişletin **Azure**, genişletin ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="ae0dd-211">Topoloji hello sağ hello Storm kümesi üzerinde çalışan ve ardından **görünüm Storm topolojileri**</span><span class="sxs-lookup"><span data-stu-id="ae0dd-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="ae0dd-212">Merhaba verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="ae0dd-212">Query hello data</span></span>

<span data-ttu-id="ae0dd-213">Veri yayılan sonra aşağıdaki adımları tooquery hello veri hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="ae0dd-214">Toohello iade **SessionInfo** projesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="ae0dd-215">Çalıştıran yeni bir örneğini başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="ae0dd-216">İstendiğinde, seçin **s** toosearch başlangıç olayı.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="ae0dd-217">Bir başlangıç istendiğinde tooenter olan ve zaman toodefine bir zaman aralığı - end bu iki kez arasındaki yalnızca olayları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="ae0dd-218">Kullanım hello aşağıdaki hello başlangıç girerken biçimlendirmek ve bitiş zamanları: ss: dd ve ''M' veya 'pm'.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="ae0dd-219">Örneğin, 23:20:00.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="ae0dd-220">oturum tooreturn olayları hello Storm topolojisini dağıtıldı önce bir başlangıç saati ve şimdi bir bitiş saatini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="ae0dd-221">Merhaba dönüş verileri metin aşağıdaki girişleri benzer toohello içerir:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="ae0dd-222">Son olayları works hello için aynı başlangıç olayları olarak aranıyor.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="ae0dd-223">Ancak, son olayları hello başlangıç olayından sonra 1 ile 5 dakika arasında rastgele oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="ae0dd-224">Birkaç zaman aralıkları toofind hello bitiş olayları tootry olabilir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="ae0dd-225">Bitiş olayları hello oturum - hello başlangıç olay zamanı ve bitiş olay saati arasındaki farkı hello hello süresini de içerir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="ae0dd-226">Bitiş olayları için verileri bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ae0dd-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="ae0dd-227">Girdiğiniz hello saat değerlerini yerel saat olsa da, hello sorgusundan döndürülen hello UTC saattir.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="ae0dd-228">Merhaba topolojiyi durdurma</span><span class="sxs-lookup"><span data-stu-id="ae0dd-228">Stop hello topology</span></span>

<span data-ttu-id="ae0dd-229">Hazır toostop hello topoloji olduğunda toohello dönmek **CorrelationTopology** Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="ae0dd-230">Merhaba, **Storm topoloji görünümü**, hello topoloji seçin ve ardından hello **KILL** hello topoloji görünümü hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ae0dd-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="ae0dd-231">Kümenizi Sil</span><span class="sxs-lookup"><span data-stu-id="ae0dd-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="ae0dd-232">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ae0dd-232">Next steps</span></span>

<span data-ttu-id="ae0dd-233">Daha fazla Storm örnekler için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ae0dd-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
