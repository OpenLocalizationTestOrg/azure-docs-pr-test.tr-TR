---
title: "Dağıtma ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme | Microsoft Docs"
description: "Dağıtma, izleme ve Linux tabanlı Hdınsight üzerinde Storm panosunu kullanarak Apache Storm topolojilerini yönetme öğrenin. Visual Studio Hadoop araçlarını kullanın."
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="4601a-104">Dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="4601a-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="4601a-105">Bu belgede, yönetme ve izleme üzerinde Storm Hdınsight kümelerinde çalışan Storm topolojilerini temellerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4601a-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4601a-106">Bu makaledeki adımlarda Hdınsight kümesinde Linux tabanlı Storm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4601a-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="4601a-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="4601a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4601a-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4601a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="4601a-109">Dağıtma ve Windows tabanlı Hdınsight üzerinde topolojileri izleme hakkında daha fazla bilgi için bkz: [dağıtma ve Windows tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="4601a-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4601a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4601a-110">Prerequisites</span></span>

* <span data-ttu-id="4601a-111">**Hdınsight kümesinde Linux tabanlı Storm**: bkz [Hdınsight üzerinde Apache Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md) küme oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="4601a-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="4601a-112">(İsteğe bağlı) **SSH ve SCP**: daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="4601a-113">(İsteğe bağlı) **Visual Studio**: Azure SDK'sı 2.5.1 ya da daha yeni ve Visual Studio için Data Lake araçları.</span><span class="sxs-lookup"><span data-stu-id="4601a-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="4601a-114">Daha fazla bilgi için bkz: [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="4601a-115">Visual Studio aşağıdaki sürümlerinden biri:</span><span class="sxs-lookup"><span data-stu-id="4601a-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="4601a-116">Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="4601a-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="4601a-117">Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="4601a-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="4601a-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4601a-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="4601a-119">Visual Studio 2015 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="4601a-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="4601a-120">Visual Studio 2017 (herhangi bir sürümünü).</span><span class="sxs-lookup"><span data-stu-id="4601a-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="4601a-121">Visual Studio 2017 için Data Lake araçları, Azure iş yükü bir parçası olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4601a-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="4601a-122">Bir topoloji gönderin: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4601a-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="4601a-123">Hdınsight araçları C# veya karma topolojiler Storm kümenize göndermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4601a-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="4601a-124">Örnek bir uygulamayı aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-124">The following steps use a sample application.</span></span> <span data-ttu-id="4601a-125">Hdınsight araçları kullanarak kendi topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio için Hdınsight araçları kullanarak C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="4601a-126">Visual Studio için Data Lake Araçları'nın en son sürümünü yüklemediyseniz, bkz: [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4601a-127">Visual Studio için Data Lake araçları Visual Studio için Hdınsight araçları adıysa.</span><span class="sxs-lookup"><span data-stu-id="4601a-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="4601a-128">Visual Studio için Data Lake araçları dahil edilmiştir __Azure iş yükü__ Visual Studio 2017 için.</span><span class="sxs-lookup"><span data-stu-id="4601a-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="4601a-129">Visual Studio'ni açın, **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="4601a-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="4601a-130">İçinde **yeni proje** iletişim kutusunda, genişletin **yüklü** > **şablonları**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="4601a-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="4601a-131">Şablonları listesinden seçin **Storm örnek**.</span><span class="sxs-lookup"><span data-stu-id="4601a-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="4601a-132">İletişim kutusunun altında uygulama için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="4601a-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![Görüntü](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="4601a-134">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve seçin **Hdınsight üzerinde Storm Gönder**.</span><span class="sxs-lookup"><span data-stu-id="4601a-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4601a-135">İstenirse, Azure aboneliğiniz için oturum açma kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="4601a-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="4601a-136">Birden fazla aboneliğiniz varsa, Hdınsight kümesi üzerinde Storm'a içeren oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4601a-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="4601a-137">Hdınsight küme üzerinde Storm'a seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="4601a-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="4601a-138">Gönderim kullanarak başarılı olup olmadığını izleyebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4601a-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="4601a-139">Bir topoloji gönderin: SSH ve Storm komutu</span><span class="sxs-lookup"><span data-stu-id="4601a-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="4601a-140">SSH Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="4601a-141">Değiştir **kullanıcıadı** SSH oturum açma adı.</span><span class="sxs-lookup"><span data-stu-id="4601a-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="4601a-142">Değiştir **CLUSTERNAME** Hdınsight küme adıyla:</span><span class="sxs-lookup"><span data-stu-id="4601a-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="4601a-143">Hdınsight kümenize bağlanmak için SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4601a-144">Örnek bir topoloji başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4601a-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="4601a-145">Bu komut kümede örnek WordCount topolojisini başlatır.</span><span class="sxs-lookup"><span data-stu-id="4601a-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="4601a-146">Bu topoloji, rastgele cümleleri oluşturun ve cümleleri her sözcüğün geçtiği sayısı.</span><span class="sxs-lookup"><span data-stu-id="4601a-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4601a-147">Kümeye topoloji gönderirken `storm` komutunu kullanmadan önce kümeyi içeren jar dosyasını kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4601a-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="4601a-148">Dosyayı kümeye kopyalamak için kullanabileceğiniz `scp` komutu.</span><span class="sxs-lookup"><span data-stu-id="4601a-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="4601a-149">Örneğin, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="4601a-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="4601a-150">WordCount örneği ve diğer storm starter örnekleri `/usr/hdp/current/storm-client/contrib/storm-starter/` konumunda kümenize zaten dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4601a-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="4601a-151">Bir topoloji gönderin: program aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="4601a-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="4601a-152">Bir topoloji Hdınsight üzerinde Storm için kümenizdeki barındırılan Nimbus hizmeti ile iletişim kurarak programlı olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4601a-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="4601a-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) nasıl dağıtıp Nimbus hizmeti aracılığıyla bir topoloji başlatmak gösteren bir Java uygulama örneğidir.</span><span class="sxs-lookup"><span data-stu-id="4601a-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="4601a-154">İzleme ve yönetme: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4601a-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="4601a-155">Bir topoloji Visual Studio kullanarak başarıyla gönderildi, **Storm topolojilerini** küme görünür görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="4601a-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="4601a-156">Topoloji çalışan topolojisi ile ilgili bilgileri görüntülemek için listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="4601a-156">Select the topology from the list to view information about the running topology.</span></span>

![Visual studio İzleyicisi](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="4601a-158">De görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini** genişleterek **Azure** > **Hdınsight**ve Hdınsight kümesinde bir Storm sağ tıklayıp seçerek **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="4601a-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="4601a-159">Şekil spout'lar veya Cıvatalar bu bileşenler hakkındaki bilgileri görüntülemek için seçin.</span><span class="sxs-lookup"><span data-stu-id="4601a-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="4601a-160">Yeni bir pencere için seçilen her öğenin açar.</span><span class="sxs-lookup"><span data-stu-id="4601a-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="4601a-161">Devre dışı bırakın ve yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="4601a-161">Deactivate and reactivate</span></span>

<span data-ttu-id="4601a-162">Sonlandırıldı veya yeniden kadar bir topoloji devre dışı bırakma, duraklatır.</span><span class="sxs-lookup"><span data-stu-id="4601a-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="4601a-163">Bu işlemleri gerçekleştirmek için kullanın __etkinliğini__ ve __yeniden__ üst tarafındaki düğmeleri __topoloji özeti__.</span><span class="sxs-lookup"><span data-stu-id="4601a-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="4601a-164">Yeniden dengelemeniz</span><span class="sxs-lookup"><span data-stu-id="4601a-164">Rebalance</span></span>

<span data-ttu-id="4601a-165">Bir topoloji dengelenmesi topolojisinin paralellik gözden geçirmek sistem izin verir.</span><span class="sxs-lookup"><span data-stu-id="4601a-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="4601a-166">Daha fazla Not eklemek için küme yeniden boyutlandırılabilir, örneğin, yeniden dengelenmesi yeni düğümleri görmek için topoloji imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="4601a-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="4601a-167">Bir topoloji amacıyla kullanmak __yeniden dengelemeniz__ en üstündeki düğmesi __topoloji özeti__.</span><span class="sxs-lookup"><span data-stu-id="4601a-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="4601a-168">Bir topoloji ilk dengelenmesi topoloji, devre dışı bırakır çalışanları eşit bir kümede yeniden dağıtır, sonra son olarak yeniden dengelenmesi oluşmadan önce durumla durum topoloji döndürür.</span><span class="sxs-lookup"><span data-stu-id="4601a-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="4601a-169">Topoloji etkin olduğunda, bu nedenle onu yeniden etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="4601a-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="4601a-170">Devre dışı bırakıldı, devre dışı kalır.</span><span class="sxs-lookup"><span data-stu-id="4601a-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="4601a-171">Bir topoloji Sonlandır</span><span class="sxs-lookup"><span data-stu-id="4601a-171">Kill a topology</span></span>

<span data-ttu-id="4601a-172">Storm topolojilerini durdurulmuş veya küme silinene kadar çalıştırmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="4601a-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="4601a-173">Bir topoloji durdurmak için kullanma __KILL__ en üstündeki düğmesi __topoloji özeti__.</span><span class="sxs-lookup"><span data-stu-id="4601a-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="4601a-174">İzleme ve yönetme: SSH ve Storm komutu</span><span class="sxs-lookup"><span data-stu-id="4601a-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="4601a-175">`storm` Yardımcı program komut satırından çalışan topolojilerle çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4601a-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="4601a-176">Kullanım `storm -h` komutları tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="4601a-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="4601a-177">Liste topolojileri</span><span class="sxs-lookup"><span data-stu-id="4601a-177">List topologies</span></span>

<span data-ttu-id="4601a-178">Çalışan topolojilerle tüm listelemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4601a-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="4601a-179">Bu komutun aşağıdaki metne benzer bilgiler döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4601a-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="4601a-180">Devre dışı bırakın ve yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="4601a-180">Deactivate and reactivate</span></span>

<span data-ttu-id="4601a-181">Sonlandırıldı veya yeniden kadar bir topoloji devre dışı bırakma, duraklatır.</span><span class="sxs-lookup"><span data-stu-id="4601a-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="4601a-182">Devre dışı bırakın ve yeniden etkinleştirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4601a-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="4601a-183">Çalışan bir topoloji Sonlandır</span><span class="sxs-lookup"><span data-stu-id="4601a-183">Kill a running topology</span></span>

<span data-ttu-id="4601a-184">Storm topolojileri, başlatıldığında, devam durdurulana kadar çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="4601a-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="4601a-185">Bir topoloji durdurmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4601a-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="4601a-186">Yeniden dengelemeniz</span><span class="sxs-lookup"><span data-stu-id="4601a-186">Rebalance</span></span>

<span data-ttu-id="4601a-187">Bir topoloji dengelenmesi topolojisinin paralellik gözden geçirmek sistem izin verir.</span><span class="sxs-lookup"><span data-stu-id="4601a-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="4601a-188">Daha fazla Not eklemek için küme yeniden boyutlandırılabilir, örneğin, yeniden dengelenmesi yeni düğümleri görmek için topoloji imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="4601a-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="4601a-189">Bir topoloji ilk dengelenmesi topoloji, devre dışı bırakır çalışanları eşit bir kümede yeniden dağıtır, sonra son olarak yeniden dengelenmesi oluşmadan önce durumla durum topoloji döndürür.</span><span class="sxs-lookup"><span data-stu-id="4601a-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="4601a-190">Topoloji etkin olduğunda, bu nedenle onu yeniden etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="4601a-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="4601a-191">Devre dışı bırakıldı, devre dışı kalır.</span><span class="sxs-lookup"><span data-stu-id="4601a-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="4601a-192">İzleme ve yönetme: Storm kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="4601a-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="4601a-193">Storm Kullanıcı Arabirimi çalışan topolojilerle çalışmaya yönelik bir web arabirimi sağlar ve HDInsight kümenize dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="4601a-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="4601a-194">Storm kullanıcı arabirimini görüntülemek için açmak üzere bir web tarayıcısı kullanın **https://CLUSTERNAME.azurehdinsight.net/stormui**, burada **CLUSTERNAME** kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="4601a-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4601a-195">Bir kullanıcı adı ve parola girmeniz istenirse kümeyi oluştururken kullandığınız küme yöneticisi (yönetici) ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="4601a-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="4601a-196">Ana sayfa</span><span class="sxs-lookup"><span data-stu-id="4601a-196">Main page</span></span>

<span data-ttu-id="4601a-197">Storm kullanıcı Arabirimi ana sayfasında aşağıdaki bilgileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="4601a-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="4601a-198">**Küme Özet**: Storm kümesi hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="4601a-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="4601a-199">**Topoloji özeti**: topolojileri çalışan bir listesi.</span><span class="sxs-lookup"><span data-stu-id="4601a-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="4601a-200">Belirli topolojileri hakkında daha fazla bilgi görüntülemek için bu bölümdeki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="4601a-201">**Yönetici Özeti**: Storm İdarecisi hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="4601a-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="4601a-202">**Nimbus yapılandırma**: kümenin Nimbus yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="4601a-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="4601a-203">Topoloji özeti</span><span class="sxs-lookup"><span data-stu-id="4601a-203">Topology summary</span></span>

<span data-ttu-id="4601a-204">Bir bağlantıdan seçme **topoloji özeti** bölüm topolojisi hakkında aşağıdaki bilgileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="4601a-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="4601a-205">**Topoloji özeti**: topolojisi hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="4601a-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="4601a-206">**Topoloji eylemleri**: topolojisini gerçekleştirdiğiniz yönetim işlemleri.</span><span class="sxs-lookup"><span data-stu-id="4601a-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="4601a-207">**Etkinleştirme**: devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="4601a-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="4601a-208">**Devre dışı**: çalışan topolojiyi duraklatır.</span><span class="sxs-lookup"><span data-stu-id="4601a-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="4601a-209">**Yeniden dengelemeniz**: topolojisinin paralelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4601a-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="4601a-210">Kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4601a-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="4601a-211">Bu işlem düğümleri artan veya azalan sayısını dengelemek üzere paralelliği ayarlamaya imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="4601a-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="4601a-212">Daha fazla bilgi için bkz. <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Bir Storm topolojisinin paralelliğini anlama</a>.</span><span class="sxs-lookup"><span data-stu-id="4601a-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="4601a-213">**KILL**: belirtilen zaman aşımından sonra Storm topolojisini sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="4601a-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="4601a-214">**Topoloji istatistikleri**: topoloji hakkındaki istatistiklerdir.</span><span class="sxs-lookup"><span data-stu-id="4601a-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="4601a-215">Sayfada diğer girdiler için zaman dilimini ayarlamak için bağlantıları kullanın **penceresi** sütun.</span><span class="sxs-lookup"><span data-stu-id="4601a-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="4601a-216">**Spout'lar**: topolojisi tarafından kullanılan spout'lar.</span><span class="sxs-lookup"><span data-stu-id="4601a-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="4601a-217">Belirli spout'lar hakkında daha fazla bilgi görüntülemek için bu bölümdeki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="4601a-218">**Cıvatalar**: topolojisi tarafından kullanılan Cıvatalar.</span><span class="sxs-lookup"><span data-stu-id="4601a-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="4601a-219">Belirli Cıvatalar hakkında daha fazla bilgi görüntülemek için bu bölümdeki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="4601a-220">**Topoloji Yapılandırması**: Seçili topoloji yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="4601a-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="4601a-221">Spout ve Cıvata özeti</span><span class="sxs-lookup"><span data-stu-id="4601a-221">Spout and Bolt summary</span></span>

<span data-ttu-id="4601a-222">Spout gelen seçme **Spout'lar** veya **Cıvatalar** bölümleri seçili öğe hakkında aşağıdaki bilgileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="4601a-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="4601a-223">**Bileşen özeti**: spout veya Cıvata hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="4601a-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="4601a-224">**Spout/Cıvata istatistikleri**: spout veya Cıvata hakkındaki istatistiklerdir.</span><span class="sxs-lookup"><span data-stu-id="4601a-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="4601a-225">Sayfada diğer girdiler için zaman dilimini ayarlamak için bağlantıları kullanın **penceresi** sütun.</span><span class="sxs-lookup"><span data-stu-id="4601a-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="4601a-226">**Giriş İstatistikleri** (yalnızca Cıvata): Cıvata tarafından kullanılan giriş akışları hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="4601a-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="4601a-227">**Çıkış istatistikleri**: spout veya Cıvata bu tarafından gösterilen akışları hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="4601a-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="4601a-228">**Yürütücüler**: spout veya Cıvata örnekleri hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="4601a-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="4601a-229">Seçin **bağlantı noktası** tanılama bilgilerinin günlüğünü görüntülemek belirli bir yürütücü için giriş üretilen Bu örneği için.</span><span class="sxs-lookup"><span data-stu-id="4601a-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="4601a-230">**Hataları**: Bu hata bilgilerini spout veya Cıvata.</span><span class="sxs-lookup"><span data-stu-id="4601a-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="4601a-231">İzleme ve yönetme: REST API'si</span><span class="sxs-lookup"><span data-stu-id="4601a-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="4601a-232">Benzer yönetim ve izleme işlevselliği REST API'sini kullanarak gerçekleştirebilmek için Storm kullanıcı Arabirimi REST API üzerinde oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="4601a-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="4601a-233">REST API, yönetmek ve Storm topolojilerini izlemek için özel araçlar oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4601a-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="4601a-234">Daha fazla bilgi için bkz: [Storm kullanıcı Arabirimi REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="4601a-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="4601a-235">Aşağıdaki bilgiler, REST API kullanarak hdınsight'ta Apache Storm özeldir.</span><span class="sxs-lookup"><span data-stu-id="4601a-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4601a-236">Storm REST API internet üzerinden genel kullanıma açık değildir ve Hdınsight küme baş düğümüne SSH tüneli kullanılarak erişilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4601a-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="4601a-237">Oluşturma ve SSH tüneli kullanma hakkında daha fazla bilgi için bkz: [kullanım SSH Ambari web kullanıcı Arabirimi, ResourceManager, kaynak, iş, Oozie ve diğer web Uı'lar erişmek için tünel](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="4601a-238">Taban URI</span><span class="sxs-lookup"><span data-stu-id="4601a-238">Base URI</span></span>

<span data-ttu-id="4601a-239">Linux tabanlı Hdınsight kümeleri REST API için taban URI konumundaki baş düğüm üzerinde kullanılabilir **API/https://HEADNODEFQDN:8744/v1/**.</span><span class="sxs-lookup"><span data-stu-id="4601a-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="4601a-240">Baş düğüm etki alanı adı, küme oluşturma sırasında oluşturulur ve statik değil.</span><span class="sxs-lookup"><span data-stu-id="4601a-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="4601a-241">Küme baş düğüm için tam etki alanı adı (FQDN) birkaç farklı şekilde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4601a-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="4601a-242">**Bir SSH oturumundan**: komutunu `headnode -f` küme için bir SSH oturumundan.</span><span class="sxs-lookup"><span data-stu-id="4601a-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="4601a-243">**Ambari Web**: seçin **Hizmetleri** sayfanın üst kısmından seçip **Storm**.</span><span class="sxs-lookup"><span data-stu-id="4601a-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="4601a-244">Gelen **Özet** sekmesine **Storm kullanıcı Arabirimi sunucu**.</span><span class="sxs-lookup"><span data-stu-id="4601a-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="4601a-245">Storm kullanıcı Arabirimi ve REST API çalıştığı düğüm sayfanın en üstünde FQDN'sidir.</span><span class="sxs-lookup"><span data-stu-id="4601a-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="4601a-246">**Ambari REST API öğesinden**: komutunu `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` Storm kullanıcı Arabirimi ve REST API çalıştığı düğüm hakkında bilgi almak için.</span><span class="sxs-lookup"><span data-stu-id="4601a-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="4601a-247">Değiştir **parola** küme için yönetici parolası ile.</span><span class="sxs-lookup"><span data-stu-id="4601a-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="4601a-248">Değiştir **CLUSTERNAME** küme adı ile.</span><span class="sxs-lookup"><span data-stu-id="4601a-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="4601a-249">Yanıtta, düğümün FQDN'sini "host_name" giriş içeriyor.</span><span class="sxs-lookup"><span data-stu-id="4601a-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="4601a-250">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="4601a-250">Authentication</span></span>

<span data-ttu-id="4601a-251">REST API istekleri kullanmalıdır **temel kimlik doğrulaması**, Hdınsight Küme Yönetici adı ve parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="4601a-252">Temel kimlik doğrulaması düz metin kullanarak gönderildiğinden, aşağıdakileri yapmalısınız **her zaman** küme ile iletişimin güvenliğini sağlamak için HTTPS kullanın.</span><span class="sxs-lookup"><span data-stu-id="4601a-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="4601a-253">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="4601a-253">Return values</span></span>

<span data-ttu-id="4601a-254">REST API öğesinden geri döndürülen bilgiler, yalnızca küme ya da sanal makineleri aynı Azure sanal ağ üzerinde küme içinde kullanılabilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="4601a-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="4601a-255">Örneğin, Zookeeper sunucuları için döndürülen tam etki alanı adı (FQDN), Internet'ten erişilemez.</span><span class="sxs-lookup"><span data-stu-id="4601a-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4601a-256">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4601a-256">Next Steps</span></span>

<span data-ttu-id="4601a-257">Artık nasıl dağıtmak ve Storm panosunu kullanarak topolojileri izlemek, öğrenme öğrendiğinize göre nasıl [Maven kullanarak geliştirme Java tabanlı topolojiler](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="4601a-258">Daha fazla örnek topolojileri listesi için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4601a-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
