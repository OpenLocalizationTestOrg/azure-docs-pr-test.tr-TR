---
title: "Azure Hdınsight Linux üzerinde Presto aaaInstall kümeleri | Microsoft Docs"
description: "Nasıl tooinstall Presto ve Linux tabanlı Hdınsight Hadoop üzerinde Airpal betik eylemleri kullanarak kümelerini öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="5baac-103">Yükleme ve Presto Hdınsight Hadoop kümeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="5baac-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="5baac-104">Bu konuda, betik eylemi kullanarak nasıl tooinstall Presto üzerinde Hdınsight Hadoop kümeleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5baac-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="5baac-105">Da bilgi nasıl tooinstall Airpal varolan Presto Hdınsight kümesinde.</span><span class="sxs-lookup"><span data-stu-id="5baac-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5baac-106">Merhaba bu belgedeki adımlar gerektiren bir **Hdınsight 3.5 Hadoop kümesi** Linux kullanır.</span><span class="sxs-lookup"><span data-stu-id="5baac-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="5baac-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="5baac-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5baac-108">Daha fazla bilgi için bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="5baac-109">Presto nedir?</span><span class="sxs-lookup"><span data-stu-id="5baac-109">What is Presto?</span></span>
<span data-ttu-id="5baac-110">[Presto](https://prestodb.io/overview.html) bir hızlı dağıtılmış SQL sorgu alt büyük veri yapısıdır.</span><span class="sxs-lookup"><span data-stu-id="5baac-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="5baac-111">Presto etkileşimli veri petabaytlarca sorgulamak için uygundur.</span><span class="sxs-lookup"><span data-stu-id="5baac-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="5baac-112">Presto ve nasıl çalıştıkları hello bileşenler hakkında daha fazla bilgi için bkz: [Presto kavramları](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="5baac-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="5baac-113">Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="5baac-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="5baac-114">Presto gibi özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="5baac-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="5baac-115">Merhaba sorunu çözmek veya tooengage kullanılabilir kanalları hello için bu teknoloji derin uzmanlık bulunduğu kaynak teknolojileri açtığınız isteyen neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="5baac-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="5baac-116">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5baac-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="5baac-117">Betik eylemi kullanarak Presto yükleyin</span><span class="sxs-lookup"><span data-stu-id="5baac-117">Install Presto using script action</span></span>

<span data-ttu-id="5baac-118">Bu bölümde, nasıl kullanarak yeni bir küme oluştururken, toouse hello örnek betik hello üzerinde Azure portal yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="5baac-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="5baac-119">Merhaba adımları kullanarak bir küme hazırlama Başlat [sağlama Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="5baac-120">Hello kullanarak hello küme oluşturduğunuzdan emin olun **özel** küme oluşturma akış.</span><span class="sxs-lookup"><span data-stu-id="5baac-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="5baac-121">Oluşturduğunuz bu hello küme hello gereksinimleri aşağıdaki karşıladığından emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="5baac-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="5baac-122">a.</span><span class="sxs-lookup"><span data-stu-id="5baac-122">a.</span></span> <span data-ttu-id="5baac-123">Bir Hadoop kümesine Hdınsight sürüm 3.5 ile olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5baac-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="5baac-124">b.</span><span class="sxs-lookup"><span data-stu-id="5baac-124">b.</span></span> <span data-ttu-id="5baac-125">Azure Storage hello veri deposu olarak kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5baac-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="5baac-126">Azure Data Lake Store hello depolama seçeneği olarak kullanan bir kümede presto kullanarak henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5baac-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Özel seçenekleri kullanarak Hdınsight kümesi oluşturma](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="5baac-128">Merhaba üzerinde **Gelişmiş ayarları** dikey penceresinde, select **betik eylemleri**ve aşağıdaki hello bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="5baac-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="5baac-129">**AD**: hello betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5baac-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="5baac-130">**Bash betiği URI’si**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="5baac-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="5baac-131">**HEAD**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5baac-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="5baac-132">**ÇALIŞAN**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5baac-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="5baac-133">**ZOOKEEPER**: Bu onay kutusunu temizleyin</span><span class="sxs-lookup"><span data-stu-id="5baac-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="5baac-134">**PARAMETRELERİ**: Bu alanı boş bırakın</span><span class="sxs-lookup"><span data-stu-id="5baac-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="5baac-135">Merhaba hello sonundaki **betik eylemleri** dikey penceresinde hello tıklatın **seçin** düğme toosave hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="5baac-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="5baac-136">Son olarak, hello tıklatın **seçin** hello hello sonundaki düğmesi **Gelişmiş ayarlar** dikey toosave hello yapılandırma bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5baac-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="5baac-137">Bölümünde açıklandığı gibi Hello küme hazırlama devam [sağlama Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5baac-138">Azure PowerShell, hello Azure CLI, hello Hdınsight .NET SDK veya Azure Resource Manager şablonları kullanılan tooapply betik eylemleri de olabilir.</span><span class="sxs-lookup"><span data-stu-id="5baac-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="5baac-139">Betik eylemleri tooalready kümeleri çalıştıran uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="5baac-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="5baac-140">Daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="5baac-141">Hdınsight ile presto kullanma</span><span class="sxs-lookup"><span data-stu-id="5baac-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="5baac-142">Yukarıda açıklanan başlangıç adımları kullanarak yükledikten sonra bir Hdınsight kümesindeki adımları toouse Presto aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5baac-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="5baac-143">SSH kullanarak toohello Hdınsight kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="5baac-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5baac-144">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="5baac-145">Merhaba Presto Kabuk komut aşağıdaki hello kullanarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="5baac-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="5baac-146">Bir örnek tablo sorgusu **hivesampletable**, varsayılan olarak tüm Hdınsight kümeleri üzerinde kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="5baac-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="5baac-147">Varsayılan olarak, [Hive](https://prestodb.io/docs/current/connector/hive.html) ve [TPCH](https://prestodb.io/docs/current/connector/tpch.html) bağlayıcıları Presto için zaten yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="5baac-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="5baac-148">Hive tüm hello tablolardan Presto içinde otomatik olarak görünür olacak şekilde hive yapılandırılmış toouse hello varsayılan olarak yüklenen Hive yükleme Bağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5baac-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="5baac-149">Presto nasıl kullanabileceğiniz hakkında ayrıntılı bir açıklaması için bkz: [Presto belgelerine](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="5baac-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="5baac-150">Airpal Presto ile kullanma</span><span class="sxs-lookup"><span data-stu-id="5baac-150">Use Airpal with Presto</span></span>

<span data-ttu-id="5baac-151">[Airpal](https://github.com/airbnb/airpal#airpal) Presto için bir açık kaynak web tabanlı sorgu arabirimdir.</span><span class="sxs-lookup"><span data-stu-id="5baac-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="5baac-152">Airpal hakkında daha fazla bilgi için bkz: [Airpal belgelerine](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="5baac-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="5baac-153">Bu bölümde, biz hello adımları çok Ara**Airpal hello edgenode üzerinde yükleme** Presto önceden sahip olan bir Hdınsight Hadoop kümesini yüklü.</span><span class="sxs-lookup"><span data-stu-id="5baac-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="5baac-154">Bu, hello Airpal web sorgu arabirimi hello Internet kullanılabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="5baac-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="5baac-155">SSH kullanarak, toohello headnode Presto yüklediği hello Hdınsight kümesinin Bağlan:</span><span class="sxs-lookup"><span data-stu-id="5baac-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5baac-156">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5baac-157">Bağlandıktan sonra komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5baac-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="5baac-158">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5baac-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="5baac-159">Merhaba çıktısını hello için başlangıç değerini not edin **değeri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="5baac-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="5baac-160">Bu, üzerinde hello küme edgenode Airpal yüklenirken gerekir.</span><span class="sxs-lookup"><span data-stu-id="5baac-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="5baac-161">İhtiyacınız olacak hello değerin üzerinde hello çıktısından olan **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="5baac-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="5baac-162">Merhaba şablonu kullan  **[burada](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate bir Hdınsight edgenode küme ve hello ekran aşağıdaki gösterildiği gibi hello değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5baac-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![Hdınsight yükle Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="5baac-164">**Satın al**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5baac-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="5baac-165">Merhaba değişiklikleri uygulanan toohello küme yapılandırması olduktan sonra aşağıdaki adımları hello kullanarak hello Airpal web arabirimi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="5baac-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="5baac-166">a.</span><span class="sxs-lookup"><span data-stu-id="5baac-166">a.</span></span> <span data-ttu-id="5baac-167">Merhaba küme dikey penceresinden tıklayın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5baac-167">From hello cluster blade, click **Applications**.</span></span>

    ![Hdınsight başlatılırken Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="5baac-169">b.</span><span class="sxs-lookup"><span data-stu-id="5baac-169">b.</span></span> <span data-ttu-id="5baac-170">Merhaba gelen **yüklü uygulamalar** dikey penceresinde tıklatın **Portal** airpal karşı.</span><span class="sxs-lookup"><span data-stu-id="5baac-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Hdınsight başlatılırken Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="5baac-172">c.</span><span class="sxs-lookup"><span data-stu-id="5baac-172">c.</span></span> <span data-ttu-id="5baac-173">İstendiğinde, hello Hdınsight Hadoop kümesi oluşturulurken belirtilen hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5baac-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="5baac-174">Hdınsight kümesinde Presto yüklemeyi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5baac-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="5baac-175">Bir Hdınsight Hadoop kümesinde Presto yükledikten sonra hello yükleme toomake değişiklikleri güncelleştirme bellek ayarları gibi özelleştirin, bağlayıcılar, vb. değiştirin. Adımları toodo şekilde aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5baac-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="5baac-176">SSH kullanarak, toohello headnode Presto yüklediği hello Hdınsight kümesinin Bağlan:</span><span class="sxs-lookup"><span data-stu-id="5baac-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5baac-177">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5baac-178">Yapılandırma değişiklik hello dosyasında `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="5baac-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="5baac-179">Presto yapılandırma hakkında daha fazla bilgi için bkz: [YARN tabanlı kümeler için Presto yapılandırma](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="5baac-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="5baac-180">Durdurun ve hello geçerli çalışan örneği Presto sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="5baac-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="5baac-181">Presto yeni bir örneğini hello özelleştirme ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="5baac-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="5baac-182">Merhaba yeni örnek toobe için hazır bekleyin ve presto Düzenleyicisi adresi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5baac-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="5baac-183">Kıyaslama verileri Presto çalıştırmak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5baac-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="5baac-184">TPC DS birçok karar destek büyük veri sistemlerini sistemlerle hello performansını ölçmek için standart hello endüstri standardıdır.</span><span class="sxs-lookup"><span data-stu-id="5baac-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="5baac-185">Hdınsight kümeleri toogenerate verileri Presto kullanın ve nasıl kendi Hdınsight Kıyaslama verilerle karşılaştırır değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="5baac-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="5baac-186">Daha fazla bilgi için bkz: [burada](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="5baac-187">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="5baac-187">See also</span></span>
* <span data-ttu-id="5baac-188">[Yükleme ve Hdınsight kümelerinde ton kullanma](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="5baac-189">Hue web çalışması kolay toocreate kolaylaştırır kullanıcı Arabirimi olan ve Pig ve Hive işleri de olarak hello varsayılan depolama Hdınsight kümeniz için göz atın.</span><span class="sxs-lookup"><span data-stu-id="5baac-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="5baac-190">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="5baac-191">Giraph üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın.</span><span class="sxs-lookup"><span data-stu-id="5baac-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5baac-192">Giraph tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5baac-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="5baac-193">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5baac-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="5baac-194">Solr üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın.</span><span class="sxs-lookup"><span data-stu-id="5baac-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5baac-195">Solr tooperform güçlü arama işlemleri depolanan verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5baac-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
