---
title: "aaaDeploy ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme | Microsoft Docs"
description: "Nasıl toodeploy, izlemek ve hello Storm panosunu kullanarak Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetmek öğrenin. Visual Studio Hadoop araçlarını kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="2f624-104">Dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="2f624-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="2f624-105">Bu belgede, yönetme ve izleme üzerinde Storm Hdınsight kümelerinde çalışan Storm topolojilerini hello temellerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2f624-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f624-106">Merhaba bu makaledeki adımlarda Hdınsight kümesinde Linux tabanlı Storm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f624-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="2f624-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="2f624-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2f624-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2f624-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="2f624-109">Dağıtma ve Windows tabanlı Hdınsight üzerinde topolojileri izleme hakkında daha fazla bilgi için bkz: [dağıtma ve Windows tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="2f624-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2f624-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f624-110">Prerequisites</span></span>

* <span data-ttu-id="2f624-111">**Hdınsight kümesinde Linux tabanlı Storm**: bkz [Hdınsight üzerinde Apache Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md) küme oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="2f624-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="2f624-112">(İsteğe bağlı) **SSH ve SCP**: daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="2f624-113">(İsteğe bağlı) **Visual Studio**: Azure SDK'sı 2.5.1 ya da daha yeni ve Visual Studio için Data Lake araçları hello.</span><span class="sxs-lookup"><span data-stu-id="2f624-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="2f624-114">Daha fazla bilgi için bkz: [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="2f624-115">Visual Studio sürümleri aşağıdaki hello biri:</span><span class="sxs-lookup"><span data-stu-id="2f624-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="2f624-116">Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="2f624-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="2f624-117">Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="2f624-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="2f624-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="2f624-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="2f624-119">Visual Studio 2015 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="2f624-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="2f624-120">Visual Studio 2017 (herhangi bir sürümünü).</span><span class="sxs-lookup"><span data-stu-id="2f624-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="2f624-121">Visual Studio 2017 için Data Lake araçları hello Azure iş yükü bir parçası olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2f624-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="2f624-122">Bir topoloji gönderin: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f624-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="2f624-123">Merhaba Hdınsight araçları kullanılan toosubmit C# veya karma topolojiler tooyour Storm kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f624-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="2f624-124">Aşağıdaki adımları hello örnek bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-124">hello following steps use a sample application.</span></span> <span data-ttu-id="2f624-125">Merhaba Hdınsight araçları kullanarak kendi topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio için Hdınsight araçları hello kullanarak C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="2f624-126">Visual Studio için hello Data Lake Araçları'nın en son sürümünü hello yüklemediyseniz, bkz: [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2f624-127">Visual Studio için Data Lake araçları Hello adıysa hello Hdınsight araçları Visual Studio için.</span><span class="sxs-lookup"><span data-stu-id="2f624-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="2f624-128">Visual Studio için Data Lake araçları hello dahil __Azure iş yükü__ Visual Studio 2017 için.</span><span class="sxs-lookup"><span data-stu-id="2f624-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="2f624-129">Visual Studio'ni açın, **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="2f624-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="2f624-130">Merhaba, **yeni proje** iletişim kutusunda, genişletin **yüklü** > **şablonları**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="2f624-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="2f624-131">Merhaba şablonları listesinden **Storm örnek**.</span><span class="sxs-lookup"><span data-stu-id="2f624-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="2f624-132">Merhaba iletişim kutusunun Hello altında hello uygulama için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="2f624-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Görüntü](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="2f624-134">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="2f624-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f624-135">İstenirse, Azure aboneliğinizin hello oturum açma kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="2f624-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="2f624-136">Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2f624-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="2f624-137">Hdınsight kümesi üzerinde Storm'a hello seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="2f624-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="2f624-138">Hello kullanarak Hello gönderme başarılı olup olmadığını izleyebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2f624-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="2f624-139">Bir topoloji gönderin: SSH ve hello komutu Storm</span><span class="sxs-lookup"><span data-stu-id="2f624-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="2f624-140">SSH tooconnect toohello Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="2f624-141">Değiştir **kullanıcıadı** SSH oturumunuzla hello adı.</span><span class="sxs-lookup"><span data-stu-id="2f624-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="2f624-142">Değiştir **CLUSTERNAME** Hdınsight küme adıyla:</span><span class="sxs-lookup"><span data-stu-id="2f624-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="2f624-143">SSH tooconnect tooyour Hdınsight kullanma hakkında daha fazla bilgi için küme için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2f624-144">Aşağıdaki komut toostart örnek bir topoloji hello kullan:</span><span class="sxs-lookup"><span data-stu-id="2f624-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="2f624-145">Bu komut hello kümede hello örnek WordCount topolojisini başlatır.</span><span class="sxs-lookup"><span data-stu-id="2f624-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="2f624-146">Bu topoloji rastgele oluşturmak cümleleri ve her sözcüğün sayısı hello oluşma hello cümlelerde.</span><span class="sxs-lookup"><span data-stu-id="2f624-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f624-147">Topoloji toohello küme gönderirken, ilk hello kullanmadan önce hello kümeyi içeren hello jar dosyasını kopyalamanız gerekir `storm` komutu.</span><span class="sxs-lookup"><span data-stu-id="2f624-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="2f624-148">toocopy hello dosya toohello kümesi hello kullanabileceğiniz `scp` komutu.</span><span class="sxs-lookup"><span data-stu-id="2f624-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="2f624-149">Örneğin, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="2f624-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="2f624-150">Merhaba WordCount örneği ve diğer storm starter örnekleri zaten eklenir konumunda kümenize `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="2f624-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="2f624-151">Bir topoloji gönderin: program aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="2f624-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="2f624-152">Hdınsight'ta bir topoloji tooStorm hello kümenizdeki barındırılan Nimbus hizmeti ile iletişim kurarak programlı olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f624-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="2f624-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) gösteren bir Java uygulama örneğidir nasıl toodeploy ve hello Nimbus hizmeti aracılığıyla bir topoloji başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f624-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="2f624-154">İzleme ve yönetme: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f624-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="2f624-155">Bir topoloji Visual Studio kullanarak başarıyla gönderildi, hello **Storm topolojilerini** hello küme görünür görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="2f624-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="2f624-156">Merhaba topoloji hello listesi tooview topoloji çalıştıran hello bilgilerini seçin.</span><span class="sxs-lookup"><span data-stu-id="2f624-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![Visual studio İzleyicisi](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="2f624-158">De görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini** genişleterek **Azure** > **Hdınsight**ve Hdınsight kümesinde bir Storm sağ tıklayıp seçerek **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="2f624-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="2f624-159">Merhaba spout'lar ya da bu bileşenler hakkında bilgi tooview Cıvatalar hello şekli seçin.</span><span class="sxs-lookup"><span data-stu-id="2f624-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="2f624-160">Yeni bir pencere için seçilen her öğenin açar.</span><span class="sxs-lookup"><span data-stu-id="2f624-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="2f624-161">Devre dışı bırakın ve yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="2f624-161">Deactivate and reactivate</span></span>

<span data-ttu-id="2f624-162">Sonlandırıldı veya yeniden kadar bir topoloji devre dışı bırakma, duraklatır.</span><span class="sxs-lookup"><span data-stu-id="2f624-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="2f624-163">tooperform şu işlemleri kullanın hello __devre dışı bırak__ ve __yeniden__ hello hello üstündeki düğmeleri __topoloji özeti__.</span><span class="sxs-lookup"><span data-stu-id="2f624-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="2f624-164">Yeniden dengelemeniz</span><span class="sxs-lookup"><span data-stu-id="2f624-164">Rebalance</span></span>

<span data-ttu-id="2f624-165">Bir topoloji dengelenmesi hello sistem toorevise hello paralellik hello topolojisinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f624-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="2f624-166">Daha fazla Not hello küme tooadd yeniden boyutlandırılabilir, örneğin, yeniden dengelenmesi bir topoloji toosee hello yeni düğümler imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="2f624-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="2f624-167">toorebalance bir topoloji kullanmak hello __yeniden dengelemeniz__ düğmesi hello hello üstündeki __topoloji özeti__.</span><span class="sxs-lookup"><span data-stu-id="2f624-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="2f624-168">Bir topoloji ilk dengelenmesi hello topoloji, devre dışı bırakır çalışanları hello küme arasında eşit olarak yeniden dağıtır, sonra son olarak yeniden dengelenmesi oluşmadan önce durumla hello topoloji toohello durum döndürür.</span><span class="sxs-lookup"><span data-stu-id="2f624-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="2f624-169">Hello topolojisi etkin olduğunda, bu nedenle onu yeniden etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="2f624-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="2f624-170">Devre dışı bırakıldı, devre dışı kalır.</span><span class="sxs-lookup"><span data-stu-id="2f624-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="2f624-171">Bir topoloji Sonlandır</span><span class="sxs-lookup"><span data-stu-id="2f624-171">Kill a topology</span></span>

<span data-ttu-id="2f624-172">Storm topolojilerini durdurulmuş veya hello küme silinene kadar çalışmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="2f624-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="2f624-173">toostop bir topoloji kullanmak hello __KILL__ düğmesi hello hello üstündeki __topoloji özeti__.</span><span class="sxs-lookup"><span data-stu-id="2f624-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="2f624-174">İzleme ve yönetme: SSH ve hello komutu Storm</span><span class="sxs-lookup"><span data-stu-id="2f624-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="2f624-175">Merhaba `storm` yardımcı programı topolojileri hello komut satırından çalıştırma ile toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f624-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="2f624-176">Kullanım `storm -h` komutları tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="2f624-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="2f624-177">Liste topolojileri</span><span class="sxs-lookup"><span data-stu-id="2f624-177">List topologies</span></span>

<span data-ttu-id="2f624-178">Komut toolist aşağıdaki hello tüm çalışan topolojileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="2f624-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="2f624-179">Bu komut, metin aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="2f624-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="2f624-180">Devre dışı bırakın ve yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="2f624-180">Deactivate and reactivate</span></span>

<span data-ttu-id="2f624-181">Sonlandırıldı veya yeniden kadar bir topoloji devre dışı bırakma, duraklatır.</span><span class="sxs-lookup"><span data-stu-id="2f624-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="2f624-182">Komut toodeactivate aşağıdaki hello kullanın ve yeniden etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f624-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="2f624-183">Çalışan bir topoloji Sonlandır</span><span class="sxs-lookup"><span data-stu-id="2f624-183">Kill a running topology</span></span>

<span data-ttu-id="2f624-184">Storm topolojileri, başlatıldığında, devam durdurulana kadar çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="2f624-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="2f624-185">toostop bir topoloji hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2f624-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="2f624-186">Yeniden dengelemeniz</span><span class="sxs-lookup"><span data-stu-id="2f624-186">Rebalance</span></span>

<span data-ttu-id="2f624-187">Bir topoloji dengelenmesi hello sistem toorevise hello paralellik hello topolojisinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f624-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="2f624-188">Daha fazla Not hello küme tooadd yeniden boyutlandırılabilir, örneğin, yeniden dengelenmesi bir topoloji toosee hello yeni düğümler imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="2f624-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="2f624-189">Bir topoloji ilk dengelenmesi hello topoloji, devre dışı bırakır çalışanları hello küme arasında eşit olarak yeniden dağıtır, sonra son olarak yeniden dengelenmesi oluşmadan önce durumla hello topoloji toohello durum döndürür.</span><span class="sxs-lookup"><span data-stu-id="2f624-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="2f624-190">Hello topolojisi etkin olduğunda, bu nedenle onu yeniden etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="2f624-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="2f624-191">Devre dışı bırakıldı, devre dışı kalır.</span><span class="sxs-lookup"><span data-stu-id="2f624-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="2f624-192">İzleme ve yönetme: Storm kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="2f624-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="2f624-193">Merhaba Storm kullanıcı Arabirimi çalışan topolojilerle çalışmaya yönelik bir web arabirimi sağlar ve Hdınsight kümenize dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="2f624-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="2f624-194">tooview hello Storm kullanıcı Arabirimi, bir web tarayıcısı tooopen kullanmak **https://CLUSTERNAME.azurehdinsight.net/stormui**, burada **CLUSTERNAME** hello kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="2f624-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="2f624-195">Hello Yöneticisi (Yönetici) ve ne zaman kullanılan parola tooprovide bir kullanıcı adı ve parola istenirse, girin oluşturma hello küme.</span><span class="sxs-lookup"><span data-stu-id="2f624-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="2f624-196">Ana sayfa</span><span class="sxs-lookup"><span data-stu-id="2f624-196">Main page</span></span>

<span data-ttu-id="2f624-197">Merhaba Storm kullanıcı Arabirimi ana sayfasının Hello bilgisinden hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f624-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="2f624-198">**Küme Özet**: hello Storm kümesi hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="2f624-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="2f624-199">**Topoloji özeti**: topolojileri çalışan bir listesi.</span><span class="sxs-lookup"><span data-stu-id="2f624-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="2f624-200">Bu bölümde tooview Hello bağlantıları belirli topolojileri hakkında daha fazla bilgi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="2f624-201">**Yönetici Özeti**: hello Storm İdarecisi hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="2f624-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="2f624-202">**Nimbus yapılandırma**: hello küme Nimbus yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="2f624-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="2f624-203">Topoloji özeti</span><span class="sxs-lookup"><span data-stu-id="2f624-203">Topology summary</span></span>

<span data-ttu-id="2f624-204">Merhaba bir bağlantı seçme **topoloji özeti** bölümü hello topolojisi hakkında bilgi aşağıdaki hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="2f624-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="2f624-205">**Topoloji özeti**: hello topolojisi hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="2f624-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="2f624-206">**Topoloji eylemleri**: hello topolojisi gerçekleştirebilen yönetim işlemleri.</span><span class="sxs-lookup"><span data-stu-id="2f624-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="2f624-207">**Etkinleştirme**: devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="2f624-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="2f624-208">**Devre dışı**: çalışan topolojiyi duraklatır.</span><span class="sxs-lookup"><span data-stu-id="2f624-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="2f624-209">**Yeniden dengelemeniz**: hello hello topolojisinin paralelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2f624-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="2f624-210">Merhaba hello kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f624-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="2f624-211">Bu işlem hello topoloji tooadjust paralellik toocompensate hello için artırılabilir veya hello kümedeki düğüm sayısını azaltılabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f624-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="2f624-212">Daha fazla bilgi için bkz: <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">hello bir Storm topolojisinin paralelliğini anlama</a>.</span><span class="sxs-lookup"><span data-stu-id="2f624-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="2f624-213">**KILL**: hello belirtilen zaman aşımı sonra Storm topolojisini sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="2f624-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="2f624-214">**Topoloji istatistikleri**: hello topoloji hakkındaki istatistiklerdir.</span><span class="sxs-lookup"><span data-stu-id="2f624-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="2f624-215">tooset girişleri hello sayfasında kalan hello ilişkin zaman çerçevesini Merhaba, hello hello bağlantıları kullanın **penceresi** sütun.</span><span class="sxs-lookup"><span data-stu-id="2f624-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="2f624-216">**Spout'lar**: Merhaba spout'lar hello topolojisi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f624-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="2f624-217">Bu bölümde tooview Hello bağlantıları belirli spout'lar hakkında daha fazla bilgi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="2f624-218">**Cıvatalar**: Merhaba Cıvatalar hello topolojisi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f624-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="2f624-219">Bu bölümde tooview Hello bağlantıları belirli Cıvatalar hakkında daha fazla bilgi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="2f624-220">**Topoloji Yapılandırması**: Seçili hello topolojisinin hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="2f624-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="2f624-221">Spout ve Cıvata özeti</span><span class="sxs-lookup"><span data-stu-id="2f624-221">Spout and Bolt summary</span></span>

<span data-ttu-id="2f624-222">Bir spout hello seçme **Spout'lar** veya **Cıvatalar** bölümleri hello seçili öğe hakkında bilgileri aşağıdaki hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="2f624-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="2f624-223">**Bileşen özeti**: Merhaba spout veya Cıvata hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="2f624-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="2f624-224">**Spout/Cıvata istatistikleri**: hello hakkındaki istatistiklerdir spout veya Cıvata.</span><span class="sxs-lookup"><span data-stu-id="2f624-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="2f624-225">tooset girişleri hello sayfasında kalan hello ilişkin zaman çerçevesini Merhaba, hello hello bağlantıları kullanın **penceresi** sütun.</span><span class="sxs-lookup"><span data-stu-id="2f624-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="2f624-226">**Giriş İstatistikleri** (yalnızca Cıvata): hello hakkında bilgi giriş hello Cıvata tarafından kullanılan akışı.</span><span class="sxs-lookup"><span data-stu-id="2f624-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="2f624-227">**Çıkış istatistikleri**: spout veya Cıvata bu tarafından gösterilen hello akışları hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="2f624-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="2f624-228">**Yürütücüler**: hello örneklerini hello spout veya Cıvata hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="2f624-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="2f624-229">Select hello **bağlantı noktası** girişi belirli Yürütücü tooview için tanılama bilgileri günlüğünü üretilen Bu örneği için.</span><span class="sxs-lookup"><span data-stu-id="2f624-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="2f624-230">**Hataları**: Bu hata bilgilerini spout veya Cıvata.</span><span class="sxs-lookup"><span data-stu-id="2f624-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="2f624-231">İzleme ve yönetme: REST API'si</span><span class="sxs-lookup"><span data-stu-id="2f624-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="2f624-232">benzer yönetim ve izleme işlevselliği hello REST API kullanarak gerçekleştirebilmek için hello Storm kullanıcı Arabirimi REST API hello üzerinde oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2f624-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="2f624-233">Merhaba REST API toocreate özel araçlar yönetmek ve Storm topolojilerini izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f624-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="2f624-234">Daha fazla bilgi için bkz: [Storm kullanıcı Arabirimi REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="2f624-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="2f624-235">Merhaba aşağıdaki bilgiler belirli toousing hello Hdınsight üzerinde Apache Storm ile REST API sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f624-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f624-236">Merhaba Storm REST API genel kullanıma açık değil üzerinde Internet hello ve bir SSH tünel toohello Hdınsight küme baş düğümüne kullanarak erişilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f624-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="2f624-237">Oluşturma ve SSH tüneli kullanma hakkında daha fazla bilgi için bkz: [kullanım SSH tünel tooaccess Ambari web kullanıcı Arabirimi, ResourceManager, kaynak, iş, Oozie ve diğer web Uı'lar](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="2f624-238">Taban URI</span><span class="sxs-lookup"><span data-stu-id="2f624-238">Base URI</span></span>

<span data-ttu-id="2f624-239">Merhaba Linux tabanlı Hdınsight kümelerinde hello REST API için taban URI hello baş düğümü üzerinde kullanılabilir **API/https://HEADNODEFQDN:8744/v1/**.</span><span class="sxs-lookup"><span data-stu-id="2f624-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="2f624-240">Merhaba etki alanı adı hello baş düğümü küme oluşturma sırasında oluşturulur ve statik değil.</span><span class="sxs-lookup"><span data-stu-id="2f624-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="2f624-241">Merhaba küme baş düğümüne hello tam etki alanı adı (FQDN) birkaç farklı şekilde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f624-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="2f624-242">**Bir SSH oturumundan**: hello komutunu `headnode -f` bir SSH oturumu toohello kümeden.</span><span class="sxs-lookup"><span data-stu-id="2f624-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="2f624-243">**Ambari Web**: seçin **Hizmetleri** hello sayfa hello üstten seçip **Storm**.</span><span class="sxs-lookup"><span data-stu-id="2f624-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="2f624-244">Merhaba gelen **Özet** sekmesine **Storm kullanıcı Arabirimi sunucu**.</span><span class="sxs-lookup"><span data-stu-id="2f624-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="2f624-245">Merhaba hello Storm kullanıcı Arabirimi ve REST API çalışıyor hello düğümü FQDN'sini hello hello sayfanın başında ' dir.</span><span class="sxs-lookup"><span data-stu-id="2f624-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="2f624-246">**Ambari REST API öğesinden**: hello komutunu `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` üzerinde çalışan Storm kullanıcı Arabirimi ve REST API hello hello düğüm hakkında tooretrieve bilgi.</span><span class="sxs-lookup"><span data-stu-id="2f624-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="2f624-247">Değiştir **parola** hello küme hello yönetici parolası ile.</span><span class="sxs-lookup"><span data-stu-id="2f624-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="2f624-248">Değiştir **CLUSTERNAME** hello küme adı ile.</span><span class="sxs-lookup"><span data-stu-id="2f624-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="2f624-249">Merhaba yanıtta hello hello düğümü FQDN'sini hello "host_name" giriş içeriyor.</span><span class="sxs-lookup"><span data-stu-id="2f624-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="2f624-250">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2f624-250">Authentication</span></span>

<span data-ttu-id="2f624-251">REST API kullanmalıdır istekleri toohello **temel kimlik doğrulaması**, hello Hdınsight Küme Yönetici adı ve parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="2f624-252">Temel kimlik doğrulaması düz metin kullanarak gönderildiğinden, aşağıdakileri yapmalısınız **her zaman** hello kümeyle HTTPS toosecure iletişimleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f624-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f624-253">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="2f624-253">Return values</span></span>

<span data-ttu-id="2f624-254">Hello REST API yalnızca hello küme içinde kullanılabilir olabilir veya sanal makinelerde hello küme aynı Azure sanal ağ hello döndürülen bilgi.</span><span class="sxs-lookup"><span data-stu-id="2f624-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="2f624-255">Örneğin, Zookeeper sunucuları için döndürülen hello tam etki alanı adı (FQDN) olduğu değil Internet hello erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="2f624-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f624-256">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="2f624-256">Next Steps</span></span>

<span data-ttu-id="2f624-257">Storm panosunu kullanarak toodeploy ve İzleyici topolojileri nasıl hello öğrendiğinize göre nasıl çok öğrenin[Maven kullanarak geliştirme Java tabanlı topolojiler](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="2f624-258">Daha fazla örnek topolojileri listesi için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2f624-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
