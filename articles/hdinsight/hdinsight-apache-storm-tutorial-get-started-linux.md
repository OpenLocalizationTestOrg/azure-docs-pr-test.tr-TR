---
title: "Apache Storm hdınsight'ta - Azure aaaStorm başlangıç örneklerine | Microsoft Docs"
description: "Bilgi nasıl toodo büyük veri analizi ve gerçek zamanlı verileri işlemek Apache Storm kullanarak Hdınsight üzerinde storm-starter örnekleri hello."
keywords: "Storm-starter, Apache Storm örneği"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="87fc8-104">Merhaba storm starter örneklerini kullanarak Hdınsight üzerinde Apache Storm kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="87fc8-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="87fc8-105">Nasıl kullanarak Hdınsight'ta Apache Storm toouse hello storm-starter örnekleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="87fc8-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="87fc8-106">Apache Storm, veri akışlarını işlemeye yönelik ölçeklenebilir, hataya dayanıklı, dağıtılmış ve gerçek zamanlı bir işlem sistemidir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="87fc8-107">Azure HDInsight’ta Storm ile büyük veri analizini gerçek zamanlı olarak gerçekleştiren bulut tabanlı bir Storm kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87fc8-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87fc8-108">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="87fc8-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="87fc8-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87fc8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="87fc8-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="87fc8-111">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="87fc8-111">**An Azure subscription**.</span></span> <span data-ttu-id="87fc8-112">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="87fc8-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="87fc8-113">**SSH ve SCP hakkında bilgi**.</span><span class="sxs-lookup"><span data-stu-id="87fc8-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="87fc8-114">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="87fc8-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="87fc8-115">Storm kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="87fc8-115">Create a Storm cluster</span></span>

<span data-ttu-id="87fc8-116">Hdınsight kümesinde bir Storm adımları toocreate aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="87fc8-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="87fc8-117">Merhaba gelen [Azure portal](https://portal.azure.com)seçin **+ yeni**, **Intelligence + analiz**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="87fc8-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![HDInsight kümesi oluşturma](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="87fc8-119">Merhaba gelen **Temelleri** dikey penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="87fc8-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="87fc8-120">**Küme adı**: Merhaba Hdınsight kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="87fc8-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="87fc8-121">**Abonelik**: hello abonelik toouse seçin.</span><span class="sxs-lookup"><span data-stu-id="87fc8-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="87fc8-122">**Oturum açma kullanıcı küme** ve **küme oturum açma parolasını**: hello küme HTTPS üzerinden erişirken hello oturum açma.</span><span class="sxs-lookup"><span data-stu-id="87fc8-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="87fc8-123">Bu kimlik bilgileri tooaccess Hizmetleri gibi hello Ambari Web kullanıcı Arabirimi veya REST API'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="87fc8-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="87fc8-124">**Güvenli Kabuk (SSH) kullanıcıadı**: hello küme SSH üzerinden erişirken kullanılan hello oturum açma.</span><span class="sxs-lookup"><span data-stu-id="87fc8-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="87fc8-125">Varsayılan olarak hello parola olduğu hello hello küme oturum açma parolası ile aynı.</span><span class="sxs-lookup"><span data-stu-id="87fc8-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="87fc8-126">**Kaynak grubu**: hello kaynak grubu toocreate hello kümede.</span><span class="sxs-lookup"><span data-stu-id="87fc8-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="87fc8-127">**Konum**: hello Azure bölgesi toocreate hello kümede.</span><span class="sxs-lookup"><span data-stu-id="87fc8-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Abonelik seçme](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="87fc8-129">Seçin **küme türü**, ve ardından kümesi hello aşağıdaki değerleri üzerinde hello **küme yapılandırması** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="87fc8-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="87fc8-130">**Küme Türü**: Storm</span><span class="sxs-lookup"><span data-stu-id="87fc8-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="87fc8-131">**İşletim Sistemi**: Linux</span><span class="sxs-lookup"><span data-stu-id="87fc8-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="87fc8-132">**Sürüm**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="87fc8-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="87fc8-133">**Küme Katmanı**: Standart</span><span class="sxs-lookup"><span data-stu-id="87fc8-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="87fc8-134">Son olarak, hello kullan **seçin** düğmesini toosave ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87fc8-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Küme türü seçme](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="87fc8-136">Merhaba küme türü seçtikten sonra hello kullan __seçin__ düğme tooset hello küme türü.</span><span class="sxs-lookup"><span data-stu-id="87fc8-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="87fc8-137">Ardından, hello kullanın __sonraki__ düğme toofinish temel yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="87fc8-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="87fc8-138">Merhaba gelen **depolama** dikey penceresinde, bir depolama hesabı oluşturun veya seçin.</span><span class="sxs-lookup"><span data-stu-id="87fc8-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="87fc8-139">Bu belgedeki Hello adımlar için bu dikey penceresinde hello varsayılan değerleri diğer alanları hello bırakın.</span><span class="sxs-lookup"><span data-stu-id="87fc8-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="87fc8-140">Kullanım hello __sonraki__ düğme toosave depolama yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="87fc8-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Hdınsight için Hello depolama hesabı ayarlarını belirleme](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="87fc8-142">Merhaba gelen **Özet** dikey penceresinde hello kümesi için hello yapılandırmayı gözden geçir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="87fc8-143">Kullanım hello __Düzenle__ toochange yanlış ayarları bağlar.</span><span class="sxs-lookup"><span data-stu-id="87fc8-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="87fc8-144">Son olarak, the__Create__ düğmesini toocreate hello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="87fc8-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Küme yapılandırma özeti](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="87fc8-146">Too20 dakika toocreate hello küme alabilir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="87fc8-147">HDInsight'ta bir storm-starter örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="87fc8-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="87fc8-148">SSH kullanarak toohello Hdınsight kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="87fc8-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="87fc8-149">SSH kullanıcı hesabınızın parolası toosecure kullandıysanız, istendiğinde tooenter olan bu.</span><span class="sxs-lookup"><span data-stu-id="87fc8-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="87fc8-150">Bir ortak anahtar kullandıysanız, hello kullanabilirsiniz `-i` parametresi toospecify hello eşleşen özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="87fc8-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="87fc8-151">Örneğin, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="87fc8-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="87fc8-152">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="87fc8-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="87fc8-153">Aşağıdaki komut toostart örnek bir topoloji hello kullan:</span><span class="sxs-lookup"><span data-stu-id="87fc8-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="87fc8-154">Hdınsight önceki sürümlerinde hello sınıfı hello topoloji adıdır `storm.starter.WordCountTopology` yerine `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="87fc8-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="87fc8-155">Bu komut, hello kümede 'WordCount' kolay adı ile Merhaba örnek WordCount topolojisini başlatır.</span><span class="sxs-lookup"><span data-stu-id="87fc8-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="87fc8-156">Bu rastgele cümleleri ve her sözcüğün sayısı hello oluşma hello cümlelerde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87fc8-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87fc8-157">Kendi topolojileri toohello küme gönderirken, ilk hello kullanmadan önce hello kümeyi içeren hello jar dosyasını kopyalamanız gerekir `storm` komutu.</span><span class="sxs-lookup"><span data-stu-id="87fc8-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="87fc8-158">Kullanım hello `scp` komut toocopy hello dosyası.</span><span class="sxs-lookup"><span data-stu-id="87fc8-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="87fc8-159">Örneğin, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="87fc8-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="87fc8-160">Merhaba WordCount örneği ve diğer storm starter örnekleri zaten eklenir konumunda kümenize `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="87fc8-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="87fc8-161">Merhaba kaynak hello storm-starter örnekleri için görüntüleme ilgileniyorsanız hello kodu bulabilirsiniz [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="87fc8-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="87fc8-162">Bu bağlantı, HDInsight 3.6 ile birlikte sağlanan Storm 1.1.x içindir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="87fc8-163">Storm diğer sürümleri için hello kullanın __şube__ farklı bir Storm sürüm hello sayfa tooselect hello üstünde düğmesi.</span><span class="sxs-lookup"><span data-stu-id="87fc8-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="87fc8-164">İzleyici hello topolojisi</span><span class="sxs-lookup"><span data-stu-id="87fc8-164">Monitor hello topology</span></span>

<span data-ttu-id="87fc8-165">Merhaba Storm kullanıcı Arabirimi çalışan topolojilerle çalışmaya yönelik bir web arabirimi sağlar ve Hdınsight kümenize dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="87fc8-166">Merhaba Storm kullanıcı arabirimini kullanarak adımları toomonitor hello topolojisi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="87fc8-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="87fc8-167">toodisplay hello Storm kullanıcı Arabirimi, bir web tarayıcısı toohttps://CLUSTERNAME.azurehdinsight.net/stormui açın.</span><span class="sxs-lookup"><span data-stu-id="87fc8-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="87fc8-168">Değiştir **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="87fc8-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87fc8-169">Hello Yöneticisi (Yönetici) ve ne zaman kullanılan parola tooprovide bir kullanıcı adı ve parola istenirse, girin oluşturma hello küme.</span><span class="sxs-lookup"><span data-stu-id="87fc8-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="87fc8-170">Altında **topoloji özeti**seçin hello **wordcount** hello girişi **adı** sütun.</span><span class="sxs-lookup"><span data-stu-id="87fc8-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="87fc8-171">Merhaba topolojisi hakkında bilgi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-171">Information about hello topology is displayed.</span></span>

    ![Storm-starter WordCount topoloji bilgilerini içeren Storm Panosu.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="87fc8-173">Bu sayfa aşağıdaki bilgilerle hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="87fc8-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="87fc8-174">**Topoloji istatistikleri** -temel bilgileri hello topoloji performansı hakkında zaman pencereleri halinde düzenlenmiş.</span><span class="sxs-lookup"><span data-stu-id="87fc8-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="87fc8-175">Merhaba sayfanın diğer bölümlerinde gösterilen bilgileri için belirli bir zaman penceresi değişiklikleri hello zaman penceresi seçme.</span><span class="sxs-lookup"><span data-stu-id="87fc8-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="87fc8-176">**Spout'lar** -her bir spout'un döndürdüğü hello son hata dahil olmak üzere spout'lar hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="87fc8-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="87fc8-177">**Cıvatalar** - Cıvatalar hakkında temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="87fc8-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="87fc8-178">**Topoloji Yapılandırması** -hello topoloji yapılandırması hakkında ayrıntılı bilgi.</span><span class="sxs-lookup"><span data-stu-id="87fc8-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="87fc8-179">Bu sayfa ayrıca hello topolojisine gerçekleştirilecek eylemleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="87fc8-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="87fc8-180">**Etkinleştir** - Devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="87fc8-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="87fc8-181">**Devre dışı bırak** - Çalışan topolojiyi duraklatır.</span><span class="sxs-lookup"><span data-stu-id="87fc8-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="87fc8-182">**Yeniden dengelemeniz** -hello hello topolojisinin paralelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87fc8-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="87fc8-183">Merhaba hello kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="87fc8-184">Dengelenmesi paralellik toocompensate hello artan/azalan düğüm sayısını hello kümedeki için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87fc8-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="87fc8-185">Daha fazla bilgi için bkz: [hello bir Storm topolojisinin paralelliğini anlama](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="87fc8-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="87fc8-186">**KILL** -hello belirtilen zaman aşımı sonra Storm topolojisini sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="87fc8-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="87fc8-187">Bu sayfadan hello bir giriş seçin **Spout'lar** veya **Cıvatalar** bölümü.</span><span class="sxs-lookup"><span data-stu-id="87fc8-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="87fc8-188">Merhaba seçilen bileşenle ilgili bilgileri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="87fc8-188">Information about hello selected component is displayed.</span></span>

    ![Seçili bileşenler hakkında bilgi içeren Storm Panosu.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="87fc8-190">Bu sayfa aşağıdaki bilgilerle hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="87fc8-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="87fc8-191">**Spout/Cıvata istatistikleri** -temel bilgileri hello bileşen performansı hakkında zaman pencereleri halinde düzenlenmiş.</span><span class="sxs-lookup"><span data-stu-id="87fc8-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="87fc8-192">Merhaba sayfanın diğer bölümlerinde gösterilen bilgileri için belirli bir zaman penceresi değişiklikleri hello zaman penceresi seçme.</span><span class="sxs-lookup"><span data-stu-id="87fc8-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="87fc8-193">**Giriş İstatistikleri** (yalnızca Cıvata) - hello Cıvata tarafından kullanılan verileri üreten bileşenler hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="87fc8-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="87fc8-194">**Çıktı istatistikleri** - Bu cıvata tarafından yayılan veriler hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="87fc8-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="87fc8-195">**Yürütücüler** - Bu bileşenin örnekleri hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="87fc8-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="87fc8-196">**Hatalar** - Bu bileşenden kaynaklanan hatalar.</span><span class="sxs-lookup"><span data-stu-id="87fc8-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="87fc8-197">Merhaba spout veya Cıvata ayrıntılarını görüntülerken hello bir girişi seçin **bağlantı noktası** hello sütununda **yürütücüler** bölümünde hello bileşenin belirli bir örneği için tooview ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="87fc8-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="87fc8-198">Bu örnekte, word hello **yedi** sözcüğünün 1493957 kez oluştu.</span><span class="sxs-lookup"><span data-stu-id="87fc8-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="87fc8-199">Bu topoloji başlatıldığından beri hello word karşılaşıldı kaç kez sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="87fc8-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="87fc8-200">Merhaba topolojiyi durdurma</span><span class="sxs-lookup"><span data-stu-id="87fc8-200">Stop hello topology</span></span>

<span data-ttu-id="87fc8-201">Toohello iade **topoloji özeti** sayfasında hello word-count topolojisi için ve hello ardından **KILL** hello düğmesinden **topoloji eylemleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="87fc8-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="87fc8-202">İstendiğinde, 10 hello topolojiyi durdurmadan önce hello saniye toowait için girin.</span><span class="sxs-lookup"><span data-stu-id="87fc8-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="87fc8-203">Merhaba ziyaret ettiğinizde hello zaman aşımı süresinden sonra hello topoloji artık görünür **Storm kullanıcı Arabirimi** başlangıç Panosu bölümü.</span><span class="sxs-lookup"><span data-stu-id="87fc8-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="87fc8-204">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="87fc8-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="87fc8-205">HDInsight kümesi oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="87fc8-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="87fc8-206"><a id="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87fc8-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="87fc8-207">Bu Apache Storm öğreticisinde Hdınsight üzerinde Storm ile çalışmanın temelleri hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="87fc8-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="87fc8-208">Ardından, nasıl çok öğrenin[Maven kullanarak geliştirme Java tabanlı topolojiler](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="87fc8-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="87fc8-209">Zaten Java tabanlı topolojiler geliştirme ile tanıdık ve toodeploy var olan bir topoloji tooHDInsight istiyorsanız, bkz [dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetmek](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="87fc8-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="87fc8-210">.NET geliştiricisiyseniz Visual Studio'yu kullanarak C# veya karma C#/Java topolojileri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87fc8-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="87fc8-211">Daha fazla bilgi edinmek için bkz. [Visual Studio için Hadoop araçlarını kullanarak HDInsight'ta Apache Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="87fc8-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="87fc8-212">Hdınsight üzerinde Storm ile kullanılan örnek Topolojileri için örnek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="87fc8-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="87fc8-213">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="87fc8-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
