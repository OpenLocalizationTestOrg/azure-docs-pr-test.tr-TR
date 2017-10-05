---
title: "Azure Hdınsight Linux kümelerinde presto yükleme | Microsoft Docs"
description: "Presto ve Airpal betik eylemleri kullanarak Linux tabanlı Hdınsight Hadoop kümeleri üzerinde nasıl yükleneceğini öğrenin."
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
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="d94b3-103">Yükleme ve Presto Hdınsight Hadoop kümeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="d94b3-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="d94b3-104">Bu konuda, nasıl betik eylemi kullanarak Hdınsight Hadoop kümeleri üzerinde Presto yükleyeceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="d94b3-105">Ayrıca varolan bir Presto Hdınsight kümesinde Airpal yüklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d94b3-106">Bu belgede yer alan adımlar gerektiren bir **Hdınsight 3.5 Hadoop kümesi** Linux kullanır.</span><span class="sxs-lookup"><span data-stu-id="d94b3-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="d94b3-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d94b3-108">Daha fazla bilgi için bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="d94b3-109">Presto nedir?</span><span class="sxs-lookup"><span data-stu-id="d94b3-109">What is Presto?</span></span>
<span data-ttu-id="d94b3-110">[Presto](https://prestodb.io/overview.html) bir hızlı dağıtılmış SQL sorgu alt büyük veri yapısıdır.</span><span class="sxs-lookup"><span data-stu-id="d94b3-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="d94b3-111">Presto etkileşimli veri petabaytlarca sorgulamak için uygundur.</span><span class="sxs-lookup"><span data-stu-id="d94b3-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="d94b3-112">Presto ve nasıl çalıştıkları bileşenler hakkında daha fazla bilgi için bkz: [Presto kavramları](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="d94b3-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="d94b3-113">Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support yalıtmak ve bu bileşenleri ilgili sorunları gidermek için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d94b3-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="d94b3-114">Presto gibi özel bileşenleri daha fazla sorunu gidermeye yardımcı olmak üzere ticari koşulların elverdiği oranda makul desteği alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d94b3-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="d94b3-115">Bu sorunu çözmek veya bu teknoloji derin uzmanlık bulunduğu açık kaynak teknolojileri için kullanılabilir kanalları devreye isteyen neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="d94b3-116">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="d94b3-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="d94b3-117">Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d94b3-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="d94b3-118">Betik eylemi kullanarak Presto yükleyin</span><span class="sxs-lookup"><span data-stu-id="d94b3-118">Install Presto using script action</span></span>

<span data-ttu-id="d94b3-119">Bu bölümde Azure Portalı'nı kullanarak yeni bir küme oluştururken, örnek komut dosyası kullanma hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d94b3-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="d94b3-120">' Ndaki adımları kullanarak bir küme hazırlama Başlat [sağlama Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="d94b3-121">Küme kullanarak oluşturduğunuz emin olun **özel** küme oluşturma akış.</span><span class="sxs-lookup"><span data-stu-id="d94b3-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="d94b3-122">Oluşturduğunuz küme aşağıdaki gereksinimleri karşıladığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="d94b3-123">a.</span><span class="sxs-lookup"><span data-stu-id="d94b3-123">a.</span></span> <span data-ttu-id="d94b3-124">Bir Hadoop kümesine Hdınsight sürüm 3.5 ile olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d94b3-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="d94b3-125">b.</span><span class="sxs-lookup"><span data-stu-id="d94b3-125">b.</span></span> <span data-ttu-id="d94b3-126">Veri deposu olarak Azure Storage kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="d94b3-127">Azure Data Lake Store depolama seçeneği olarak kullanan bir kümede presto kullanarak henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d94b3-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![Özel seçenekleri kullanarak Hdınsight kümesi oluşturma](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="d94b3-129">Üzerinde **Gelişmiş ayarları** dikey penceresinde, select **betik eylemleri**ve aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="d94b3-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="d94b3-130">**AD**: betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="d94b3-131">**Bash betiği URI’si**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="d94b3-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="d94b3-132">**HEAD**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="d94b3-133">**ÇALIŞAN**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="d94b3-134">**ZOOKEEPER**: Bu onay kutusunu temizleyin</span><span class="sxs-lookup"><span data-stu-id="d94b3-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="d94b3-135">**PARAMETRELERİ**: Bu alanı boş bırakın</span><span class="sxs-lookup"><span data-stu-id="d94b3-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="d94b3-136">Ekranın alt kısmındaki **betik eylemleri** dikey penceresinde tıklatın **seçin** yapılandırmayı kaydetmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d94b3-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="d94b3-137">Son olarak, tıklatın **seçin** alt kısmındaki düğmesi **Gelişmiş ayarları** yapılandırma bilgilerini kaydetmek için dikey penceresini.</span><span class="sxs-lookup"><span data-stu-id="d94b3-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="d94b3-138">Bölümünde açıklandığı gibi küme hazırlama devam [sağlama Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d94b3-139">Azure PowerShell, Azure CLI, Hdınsight .NET SDK veya Azure Resource Manager şablonları betik eylemleri uygulamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="d94b3-140">Zaten çalışan kümeler için betik eylemleri de uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d94b3-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="d94b3-141">Daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="d94b3-142">Hdınsight ile presto kullanma</span><span class="sxs-lookup"><span data-stu-id="d94b3-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="d94b3-143">Yukarıda açıklanan adımları kullanarak yükledikten sonra bir Hdınsight küme Presto kullanmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="d94b3-144">SSH kullanarak HDInsight kümesine bağlanma:</span><span class="sxs-lookup"><span data-stu-id="d94b3-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="d94b3-145">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="d94b3-146">Aşağıdaki komutu kullanarak Presto Kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="d94b3-147">Bir örnek tablo sorgusu **hivesampletable**, varsayılan olarak tüm Hdınsight kümeleri üzerinde kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="d94b3-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="d94b3-148">Varsayılan olarak, [Hive](https://prestodb.io/docs/current/connector/hive.html) ve [TPCH](https://prestodb.io/docs/current/connector/tpch.html) bağlayıcıları Presto için zaten yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="d94b3-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="d94b3-149">Hive bağlayıcı Hive tüm tablolardan Presto içinde otomatik olarak görünür olması için varsayılan olarak yüklenen Hive yükleme kullanmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d94b3-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="d94b3-150">Presto nasıl kullanabileceğiniz hakkında ayrıntılı bir açıklaması için bkz: [Presto belgelerine](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="d94b3-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="d94b3-151">Airpal Presto ile kullanma</span><span class="sxs-lookup"><span data-stu-id="d94b3-151">Use Airpal with Presto</span></span>

<span data-ttu-id="d94b3-152">[Airpal](https://github.com/airbnb/airpal#airpal) Presto için bir açık kaynak web tabanlı sorgu arabirimdir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="d94b3-153">Airpal hakkında daha fazla bilgi için bkz: [Airpal belgelerine](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="d94b3-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="d94b3-154">Bu bölümde, aşağıdaki adımları olarak ele **Airpal üzerinde edgenode yükleme** Presto önceden sahip olan bir Hdınsight Hadoop kümesini yüklü.</span><span class="sxs-lookup"><span data-stu-id="d94b3-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="d94b3-155">Bu Airpal web sorgu arabirimi Internet üzerinden kullanılabilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d94b3-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="d94b3-156">SSH kullanarak, Presto yüklü olduğu Hdınsight küme headnode için Bağlan:</span><span class="sxs-lookup"><span data-stu-id="d94b3-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="d94b3-157">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d94b3-158">Bağlandıktan sonra aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="d94b3-159">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d94b3-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="d94b3-160">Çıktıdan değeri Not **değeri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="d94b3-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="d94b3-161">Bu, küme edgenode Airpal yüklenirken gerekir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="d94b3-162">Yukarıdaki çıktısını ihtiyacınız olacak değerdir **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="d94b3-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="d94b3-163">Şablon kullanmak  **[burada](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  bir Hdınsight kümesi edgenode oluşturma ve aşağıdaki ekran görüntüsünde gösterildiği gibi değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![Hdınsight yükle Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="d94b3-165">**Satın al**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="d94b3-166">Küme yapılandırmasında değişiklikler uygulandıktan sonra aşağıdaki adımları kullanarak Airpal web arabirimi erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d94b3-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="d94b3-167">a.</span><span class="sxs-lookup"><span data-stu-id="d94b3-167">a.</span></span> <span data-ttu-id="d94b3-168">Küme dikey penceresinden tıklayın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d94b3-168">From the cluster blade, click **Applications**.</span></span>

    ![Hdınsight başlatılırken Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="d94b3-170">b.</span><span class="sxs-lookup"><span data-stu-id="d94b3-170">b.</span></span> <span data-ttu-id="d94b3-171">Gelen **yüklü uygulamalar** dikey penceresinde tıklatın **Portal** airpal karşı.</span><span class="sxs-lookup"><span data-stu-id="d94b3-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Hdınsight başlatılırken Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="d94b3-173">c.</span><span class="sxs-lookup"><span data-stu-id="d94b3-173">c.</span></span> <span data-ttu-id="d94b3-174">İstendiğinde, Hdınsight Hadoop kümesi oluşturulurken belirtilen yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="d94b3-175">Hdınsight kümesinde Presto yüklemeyi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="d94b3-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="d94b3-176">Bir Hdınsight Hadoop kümesinde Presto yükledikten sonra yüklemenin bellek ayarlarını güncelleştirmek, Değiştir bağlayıcılar, vb. gibi değişiklik için özelleştirebilirsiniz. Bunu yapmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="d94b3-177">SSH kullanarak, Presto yüklü olduğu Hdınsight küme headnode için Bağlan:</span><span class="sxs-lookup"><span data-stu-id="d94b3-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="d94b3-178">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d94b3-179">Yapılandırma değişiklik dosyasında `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="d94b3-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="d94b3-180">Presto yapılandırma hakkında daha fazla bilgi için bkz: [YARN tabanlı kümeler için Presto yapılandırma](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="d94b3-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="d94b3-181">Durdurun ve Presto geçerli çalışan örneği sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="d94b3-182">Presto yeni bir örneğini özelleştirme ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="d94b3-183">Presto Düzenleyicisi adresini not ve hazır olması için yeni örnek bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d94b3-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="d94b3-184">Kıyaslama verileri Presto çalıştırmak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d94b3-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="d94b3-185">TPC DS birçok karar destek büyük veri sistemlerini sistemlerle performansını ölçmek için endüstri standardıdır.</span><span class="sxs-lookup"><span data-stu-id="d94b3-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="d94b3-186">Hdınsight kümelerinde Presto veriler oluşturulmasına neden ve nasıl kendi Hdınsight Kıyaslama verilerle karşılaştırır değerlendirmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d94b3-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="d94b3-187">Daha fazla bilgi için bkz: [burada](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="d94b3-188">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d94b3-188">See also</span></span>
* <span data-ttu-id="d94b3-189">[Yükleme ve Hdınsight kümelerinde ton kullanma](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="d94b3-190">Hue web oluşturmak, çalıştırmak ve Pig ve Hive işleri, Hdınsight için varsayılan depolama Gözat yanı sıra küme daha kolay hale getirir UI ' dir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="d94b3-191">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="d94b3-192">Küme özelleştirme Giraph Hdınsight Hadoop kümelerine yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d94b3-193">Giraph Hadoop kullanarak işleme grafik işlemleri yapmanıza olanak tanır ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d94b3-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="d94b3-194">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d94b3-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="d94b3-195">Küme özelleştirme Solr Hdınsight Hadoop kümelerine yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d94b3-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d94b3-196">Solr, depolanan verileri güçlü arama işlemleri olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d94b3-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
