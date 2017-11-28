---
title: "aaaDeploy ve Hdınsight üzerinde Apache Storm topolojilerini yönetme | Microsoft Docs"
description: "Nasıl toodeploy, izlemek ve hello Storm panosunu kullanarak Hdınsight üzerinde Apache Storm topolojilerini yönetmek öğrenin. Visual Studio Hadoop araçlarını kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="6bd17-104">Dağıtma ve Windows tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="6bd17-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="6bd17-105">Merhaba Storm Panosu tooeasily verir dağıtın ve Apache Storm topolojileri tooyour Hdınsight kümesi, web tarayıcısı kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="6bd17-106">Ayrıca, hello Pano toomonitor kullanın ve çalışan topolojileri izleyip yönetmek.</span><span class="sxs-lookup"><span data-stu-id="6bd17-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="6bd17-107">Visual Studio kullanırsanız, Visual Studio için Hdınsight araçları hello Visual Studio'da benzer özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bd17-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="6bd17-108">Merhaba Storm panosu ve hello Storm hello Hdınsight araçları özelliklerinde kullanılan toocreate olabilen Storm REST API hello üzerinde kendi izleme ve yönetim çözümleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bd17-109">Bu belgedeki Hello adımlar Windows hello işletim sistemi olarak kullanan Hdınsight kümesi üzerinde Storm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="6bd17-110">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6bd17-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6bd17-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="6bd17-112">Dağıtma ve Storm topolojileri Linux kullanan bir Hdınsight kümesi ile yönetme hakkında daha fazla bilgi için bkz: [dağıtma ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="6bd17-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bd17-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6bd17-113">Prerequisites</span></span>

* <span data-ttu-id="6bd17-114">**Hdınsight üzerinde Apache Storm** -bkz [Hdınsight üzerinde Apache Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started.md) küme oluşturma adımları için.</span><span class="sxs-lookup"><span data-stu-id="6bd17-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="6bd17-115">Hello için **Storm Panosu**: HTML5 destekleyen modern bir web tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="6bd17-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="6bd17-116">İçin **Visual Studio** -Azure SDK'sı 2.5.1 ya da daha yeni ve Visual Studio için Hdınsight araçları hello.</span><span class="sxs-lookup"><span data-stu-id="6bd17-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="6bd17-117">Bkz: [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall ve hello Hdınsight araçları Visual Studio için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="6bd17-118">Visual Studio sürümleri aşağıdaki hello biri:</span><span class="sxs-lookup"><span data-stu-id="6bd17-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="6bd17-119">Visual Studio 2012 güncelleştirme 4 ile</span><span class="sxs-lookup"><span data-stu-id="6bd17-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="6bd17-120">Visual Studio 2013 güncelleştirme 4 veya Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="6bd17-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="6bd17-121">Visual Studio 2015 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="6bd17-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="6bd17-122">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="6bd17-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="6bd17-123">Storm Panosu</span><span class="sxs-lookup"><span data-stu-id="6bd17-123">Storm Dashboard</span></span>

<span data-ttu-id="6bd17-124">Merhaba Storm Panosu Storm kümenizde kullanılabilir bir web sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="6bd17-125">Merhaba URL **https://&lt;clustername >.azurehdinsight.net/**, burada **clustername** Hdınsight kümesi üzerinde Storm'a hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="6bd17-126">Merhaba Storm Panosu Hello üstten seçin **gönderme topoloji**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="6bd17-127">Başlangıç sayfası toorun örnek topoloji Hello yönergeler veya tooupload izleyin ve sizin oluşturduğunuz bir topoloji çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Merhaba topolojisi sayfasında Gönder][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="6bd17-129">Storm kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="6bd17-129">Storm UI</span></span>

<span data-ttu-id="6bd17-130">Storm Panosu Hello hello seçin **Storm kullanıcı Arabirimi** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="6bd17-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="6bd17-131">Bu, çalışan topolojilerle toplama tooany içinde hello küme hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6bd17-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![Merhaba storm kullanıcı arabirimi][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="6bd17-133">Internet Explorer'ın bazı sürümleriyle ilk ziyaret ettikten sonra Storm kullanıcı Arabirimi yenilemez bu hello fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bd17-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="6bd17-134">Örneğin, bunu hello yeni topolojileri gönderdiğiniz ya da daha önce etkinliği, bir topoloji etkin olarak gösterebilir göstermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="6bd17-135">Microsoft bu sorunun farkındadır ve bir çözüm üzerinde çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="6bd17-136">Ana sayfa</span><span class="sxs-lookup"><span data-stu-id="6bd17-136">Main page</span></span>

<span data-ttu-id="6bd17-137">Merhaba Storm kullanıcı Arabirimi ana sayfasının Hello bilgisinden hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="6bd17-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="6bd17-138">**Küme Özet**: hello Storm kümesi hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="6bd17-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="6bd17-139">**Topoloji özeti**: topolojileri çalışan bir listesi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="6bd17-140">Bu bölümde tooview Hello bağlantıları belirli topolojileri hakkında daha fazla bilgi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="6bd17-141">**Yönetici Özeti**: hello Storm İdarecisi hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="6bd17-142">**Nimbus yapılandırma**: hello küme Nimbus yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="6bd17-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="6bd17-143">Topoloji özeti</span><span class="sxs-lookup"><span data-stu-id="6bd17-143">Topology summary</span></span>

<span data-ttu-id="6bd17-144">Merhaba bir bağlantı seçme **topoloji özeti** bölümü hello topolojisi hakkında bilgi aşağıdaki hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="6bd17-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="6bd17-145">**Topoloji özeti**: hello topolojisi hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="6bd17-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="6bd17-146">**Topoloji eylemleri**: hello topolojisi gerçekleştirebilen yönetim işlemleri.</span><span class="sxs-lookup"><span data-stu-id="6bd17-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="6bd17-147">**Etkinleştirme**: devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="6bd17-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="6bd17-148">**Devre dışı**: çalışan topolojiyi duraklatır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="6bd17-149">**Yeniden dengelemeniz**: hello hello topolojisinin paralelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6bd17-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="6bd17-150">Merhaba hello kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="6bd17-151">Bu, hello topoloji tooadjust paralellik toocompensate hello için artırılabilir veya hello kümedeki düğüm sayısını azaltılabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bd17-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="6bd17-152">Daha fazla bilgi için bkz: [hello (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) bir Storm topolojisinin paralelliğini anlama](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="6bd17-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="6bd17-153">**KILL**: hello belirtilen zaman aşımı sonra Storm topolojisini sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="6bd17-154">**Topoloji istatistikleri**: hello topoloji hakkındaki istatistiklerdir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="6bd17-155">Hello Hello bağlantıları kullanın **penceresi** sütun tooset hello hello sayfasında girişleri kalan hello ilişkin zaman çerçevesini.</span><span class="sxs-lookup"><span data-stu-id="6bd17-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="6bd17-156">**Spout'lar**: Merhaba spout'lar hello topolojisi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="6bd17-157">Bu bölümde tooview Hello bağlantıları belirli spout'lar hakkında daha fazla bilgi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="6bd17-158">**Cıvatalar**: Merhaba Cıvatalar hello topolojisi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6bd17-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="6bd17-159">Bu bölümde tooview Hello bağlantıları belirli Cıvatalar hakkında daha fazla bilgi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="6bd17-160">**Topoloji Yapılandırması**: Seçili hello topolojisinin hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="6bd17-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="6bd17-161">Spout ve Cıvata özeti</span><span class="sxs-lookup"><span data-stu-id="6bd17-161">Spout and Bolt summary</span></span>

<span data-ttu-id="6bd17-162">Bir spout hello seçme **Spout'lar** veya **Cıvatalar** bölümleri hello seçili öğe hakkında bilgileri aşağıdaki hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="6bd17-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="6bd17-163">**Bileşen özeti**: Merhaba spout veya Cıvata hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="6bd17-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="6bd17-164">**Spout/Cıvata istatistikleri**: hello hakkındaki istatistiklerdir spout veya Cıvata.</span><span class="sxs-lookup"><span data-stu-id="6bd17-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="6bd17-165">Hello Hello bağlantıları kullanın **penceresi** sütun tooset hello hello sayfasında girişleri kalan hello ilişkin zaman çerçevesini.</span><span class="sxs-lookup"><span data-stu-id="6bd17-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="6bd17-166">**Giriş İstatistikleri** (yalnızca Cıvata): hello hakkında bilgi giriş hello Cıvata tarafından kullanılan akışı.</span><span class="sxs-lookup"><span data-stu-id="6bd17-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="6bd17-167">**Çıkış istatistikleri**: spout veya Cıvata bu tarafından gösterilen hello akışları hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="6bd17-168">**Yürütücüler**: hello örneklerini hello spout veya Cıvata hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="6bd17-169">Select hello **bağlantı noktası** girişi belirli Yürütücü tooview için tanılama bilgileri günlüğünü üretilen Bu örneği için.</span><span class="sxs-lookup"><span data-stu-id="6bd17-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="6bd17-170">**Hataları**: Bu hata bilgilerini spout veya Cıvata.</span><span class="sxs-lookup"><span data-stu-id="6bd17-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="6bd17-171">Visual Studio için HDInsight Araçları</span><span class="sxs-lookup"><span data-stu-id="6bd17-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="6bd17-172">Merhaba Hdınsight araçları kullanılan toosubmit C# veya karma topolojiler tooyour Storm kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="6bd17-173">Aşağıdaki adımları hello örnek bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-173">hello following steps use a sample application.</span></span> <span data-ttu-id="6bd17-174">Merhaba Hdınsight araçları kullanarak kendi topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio için Hdınsight araçları hello kullanarak C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6bd17-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="6bd17-175">Adımları toodeploy örnek tooyour Storm Hdınsight kümesinde aşağıdaki hello kullanın, sonra görüntüleyin ve hello topoloji yönetin.</span><span class="sxs-lookup"><span data-stu-id="6bd17-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="6bd17-176">Visual Studio için Hdınsight araçları hello en son sürümünü hello yüklemediyseniz, bkz: [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6bd17-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="6bd17-177">Visual Studio'ni açın, **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="6bd17-178">Merhaba, **yeni proje** iletişim kutusunda, genişletin **yüklü** > **şablonları**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="6bd17-179">Merhaba şablonları listesinden **Storm örnek**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="6bd17-180">Merhaba iletişim kutusunun Hello altında hello uygulama için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Görüntü](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="6bd17-182">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6bd17-183">İstenirse, Azure aboneliğinizin hello oturum açma kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="6bd17-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="6bd17-184">Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="6bd17-185">Hdınsight kümesi üzerinde Storm'a hello seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="6bd17-186">Hello kullanarak Hello gönderme başarılı olup olmadığını izleyebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="6bd17-187">Merhaba topoloji başarıyla gönderildi, hello **Storm topolojilerini** hello küme görünür.</span><span class="sxs-lookup"><span data-stu-id="6bd17-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="6bd17-188">Merhaba topoloji hello listesi tooview topoloji çalıştıran hello bilgilerini seçin.</span><span class="sxs-lookup"><span data-stu-id="6bd17-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![Visual studio İzleyicisi](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="6bd17-190">De görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini** genişleterek **Azure** > **Hdınsight**ve Hdınsight kümesinde bir Storm sağ tıklayıp seçerek **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="6bd17-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="6bd17-191">Merhaba spout'lar ya da bu bileşenler hakkında bilgi tooview Cıvatalar hello şekli seçin.</span><span class="sxs-lookup"><span data-stu-id="6bd17-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="6bd17-192">Yeni bir pencere için seçilen her öğenin açar.</span><span class="sxs-lookup"><span data-stu-id="6bd17-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6bd17-193">Merhaba hello topoloji adıdır hello topolojisinin hello sınıf adı (Bu durumda, `HelloWord`,) eklenmiş bir zaman damgasına sahip.</span><span class="sxs-lookup"><span data-stu-id="6bd17-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="6bd17-194">Merhaba gelen **topoloji özeti** görünümü, select **KILL** toostop hello topolojisi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6bd17-195">Storm topolojilerini durdurulmuş veya hello küme silinene kadar çalışmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="6bd17-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="6bd17-196">REST API</span><span class="sxs-lookup"><span data-stu-id="6bd17-196">REST API</span></span>

<span data-ttu-id="6bd17-197">benzer yönetim ve izleme işlevselliği hello REST API kullanarak gerçekleştirebilmek için hello Storm kullanıcı Arabirimi REST API hello üzerinde oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="6bd17-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="6bd17-198">Merhaba REST API toocreate özel araçlar yönetmek ve Storm topolojilerini izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bd17-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="6bd17-199">Daha fazla bilgi için bkz: [Storm kullanıcı Arabirimi REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="6bd17-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="6bd17-200">Merhaba aşağıdaki bilgiler belirli toousing hello Hdınsight üzerinde Apache Storm ile REST API sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bd17-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="6bd17-201">Taban URI</span><span class="sxs-lookup"><span data-stu-id="6bd17-201">Base URI</span></span>

<span data-ttu-id="6bd17-202">Hdınsight kümelerinde hello REST API için ana Uri hello **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, burada **clustername** hello Storm'a üzerinde adıdır Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="6bd17-203">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="6bd17-203">Authentication</span></span>

<span data-ttu-id="6bd17-204">REST API kullanmalıdır istekleri toohello **temel kimlik doğrulaması**, hello Hdınsight Küme Yönetici adı ve parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="6bd17-205">Temel kimlik doğrulaması düz metin kullanarak gönderildiğinden, aşağıdakileri yapmalısınız **her zaman** hello kümeyle HTTPS toosecure iletişimleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd17-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="6bd17-206">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="6bd17-206">Return values</span></span>

<span data-ttu-id="6bd17-207">Hello REST API yalnızca hello küme içinde kullanılabilir olabilir veya sanal makinelerde hello küme aynı Azure sanal ağ hello döndürülen bilgi.</span><span class="sxs-lookup"><span data-stu-id="6bd17-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="6bd17-208">Örneğin, Zookeeper sunucuları için döndürülen hello tam etki alanı adı (FQDN) değil olması Internet hello erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="6bd17-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bd17-209">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6bd17-209">Next Steps</span></span>

<span data-ttu-id="6bd17-210">Storm panosunu kullanarak toodeploy ve İzleyici topolojileri nasıl hello öğrendiğinize göre öğrenin nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="6bd17-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="6bd17-211">Visual Studio için Hdınsight araçları Hello kullanarak C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="6bd17-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="6bd17-212">Maven kullanarak Java tabanlı topolojiler geliştirme</span><span class="sxs-lookup"><span data-stu-id="6bd17-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="6bd17-213">Daha fazla örnek topolojileri listesi için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6bd17-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
