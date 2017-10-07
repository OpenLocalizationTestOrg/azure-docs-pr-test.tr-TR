---
title: "aaaInstall ve Hdınsight (Hadoop) - Azure Giraph kullanma | Microsoft Docs"
description: "Betik eylemleri kullanılarak nasıl tooinstall Giraph Linux tabanlı hdınsight kümeleri hakkında bilgi edinin. Betik eylemleri toocustomize hello küme oluşturma sırasında küme yapılandırmasını değiştirme veya hizmetleri ve yardımcı programları yükleme sağlar."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="c42c1-104">Giraph Hdınsight Hadoop kümelerine yükleme ve Giraph tooprocess büyük ölçekli grafikleri kullanma</span><span class="sxs-lookup"><span data-stu-id="c42c1-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="c42c1-105">Bilgi nasıl tooinstall Apache Giraph Hdınsight kümesinde.</span><span class="sxs-lookup"><span data-stu-id="c42c1-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="c42c1-106">hdınsight Hello betik eylemi özelliği sağlar, toocustomize bash komut dosyası çalıştırarak, küme.</span><span class="sxs-lookup"><span data-stu-id="c42c1-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="c42c1-107">Komut dosyaları kullanılan toocustomize kümeleri sırasında ve Küme oluşturulduktan sonra olabilir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c42c1-108">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c42c1-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c42c1-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c42c1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="c42c1-111"><a name="whatis"></a>Giraph nedir</span><span class="sxs-lookup"><span data-stu-id="c42c1-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="c42c1-112">[Apache Giraph](http://giraph.apache.org/) tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="c42c1-113">Grafik nesneleri arasındaki ilişkiler model.</span><span class="sxs-lookup"><span data-stu-id="c42c1-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="c42c1-114">Örneğin, Internet veya sosyal ağlar üzerindeki kişiler arasındaki ilişkileri hello gibi büyük bir ağ yönlendiricileri arasındaki bağlantıları hello.</span><span class="sxs-lookup"><span data-stu-id="c42c1-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="c42c1-115">Grafik işleme hello bir grafik nesneleri arasındaki ilişkiler hakkında tooreason gibi sağlar:</span><span class="sxs-lookup"><span data-stu-id="c42c1-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="c42c1-116">Geçerli ilişkilere dayanan olası arkadaş tanımlama.</span><span class="sxs-lookup"><span data-stu-id="c42c1-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="c42c1-117">Merhaba kısa rotayı bir ağda iki bilgisayar arasında tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="c42c1-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="c42c1-118">Web sayfalarının Hello sayfa derecesini hesaplama.</span><span class="sxs-lookup"><span data-stu-id="c42c1-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="c42c1-119">Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenen - Microsoft Support tooisolate yardımcı olur ve sorunları ilgili toothese bileşenler çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="c42c1-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="c42c1-120">Giraph gibi özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="c42c1-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="c42c1-121">Microsoft Support mümkün tooresolving hello sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="c42c1-122">Aksi durumda, bu teknoloji derin uzmanlık bulunduğu açık kaynak toplulukları başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="c42c1-123">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="c42c1-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="c42c1-124">Hangi hello komut dosyası gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="c42c1-124">What hello script does</span></span>

<span data-ttu-id="c42c1-125">Bu komut dosyası hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="c42c1-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="c42c1-126">Giraph çok yükler`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="c42c1-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="c42c1-127">Kopya hello `giraph-examples.jar` dosya kümenizin toodefault storage (WASB):`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="c42c1-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="c42c1-128"><a name="install"></a>Betik eylemleri kullanılarak Giraph yükleyin</span><span class="sxs-lookup"><span data-stu-id="c42c1-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="c42c1-129">Hdınsight kümesinde bir örnek komut dosyası tooinstall Giraph konumu aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="c42c1-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="c42c1-130">Bu bölümde, nasıl toouse hello örnek betik hello Azure portal kullanarak hello küme oluşturulurken hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c42c1-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="c42c1-131">Betik eylemi, yöntemler aşağıdaki hello birini kullanarak uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="c42c1-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="c42c1-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c42c1-132">Azure PowerShell</span></span>
> * <span data-ttu-id="c42c1-133">Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c42c1-133">hello Azure CLI</span></span>
> * <span data-ttu-id="c42c1-134">Merhaba Hdınsight .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="c42c1-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="c42c1-135">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="c42c1-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="c42c1-136">Betik eylemleri tooalready kümeleri çalıştıran uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="c42c1-137">Daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c42c1-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="c42c1-138">Merhaba adımları kullanarak bir küme oluşturmaya başlamak [oluşturma Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md), ancak oluşturma tamamlamayın.</span><span class="sxs-lookup"><span data-stu-id="c42c1-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="c42c1-139">Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **betik eylemleri**ve aşağıdaki bilgilerle hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="c42c1-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="c42c1-140">**AD**: hello betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c42c1-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="c42c1-141">**BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="c42c1-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="c42c1-142">**HEAD**: Bu girişi denetleyin</span><span class="sxs-lookup"><span data-stu-id="c42c1-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="c42c1-143">**ÇALIŞAN**: Bu girdi işaretlemeden bırakın</span><span class="sxs-lookup"><span data-stu-id="c42c1-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="c42c1-144">**ZOOKEEPER**: Bu girdi işaretlemeden bırakın</span><span class="sxs-lookup"><span data-stu-id="c42c1-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="c42c1-145">**PARAMETRELERİ**: Bu alanı boş bırakın</span><span class="sxs-lookup"><span data-stu-id="c42c1-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="c42c1-146">Merhaba hello sonundaki **betik eylemleri**, hello kullan **seçin** düğme toosave hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="c42c1-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="c42c1-147">Son olarak, hello kullan **seçin** düğmesi hello hello sonundaki **isteğe bağlı yapılandırma** dikey toosave hello isteğe bağlı yapılandırma bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c42c1-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="c42c1-148">Bölümünde açıklandığı gibi Hello küme oluşturmaya devam [oluşturma Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c42c1-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="c42c1-149"><a name="usegiraph"></a>Hdınsight'ta nasıl Giraph kullanıyor?</span><span class="sxs-lookup"><span data-stu-id="c42c1-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="c42c1-150">Merhaba Küme oluşturulduktan sonra aşağıdaki adımları toorun hello SimpleShortestPathsComputation örneğine Giraph dahil hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c42c1-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="c42c1-151">Bu örnek hello basic kullanan [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) hello en kısa yolu bir grafik nesneler arasındaki bulmak için uygulama.</span><span class="sxs-lookup"><span data-stu-id="c42c1-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="c42c1-152">SSH kullanarak toohello Hdınsight kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="c42c1-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c42c1-153">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c42c1-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c42c1-154">Kullanım hello şu komutu toocreate adlı bir dosya **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="c42c1-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="c42c1-155">Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c42c1-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="c42c1-156">Bu veri hello biçimi kullanarak bir yönlendirilmiş grafik nesneler arasındaki ilişkiyi tanımlayan `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="c42c1-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="c42c1-157">Her satır arasındaki bir ilişkiyi temsil eden bir `source_id` nesne ve bir veya daha fazla `dest_id` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="c42c1-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="c42c1-158">Merhaba `edge_value` , hello gücü veya hello bağlantı uzaklığı olarak düşünülebilir `source_id` ve `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="c42c1-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="c42c1-159">Çıkış çizilmiş ve nesneleri arasındaki hello uzaklığı olarak hello değeri (veya ağırlık) kullanarak, hello veri diyagramı aşağıdaki hello gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="c42c1-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![Daireler arasında değişen uzaklığı satır olarak çizilen tiny_graph.txt](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="c42c1-161">toosave hello dosya, kullanım **Ctrl + X**, ardından **Y**ve son olarak **Enter** tooaccept hello dosya adı.</span><span class="sxs-lookup"><span data-stu-id="c42c1-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="c42c1-162">Hdınsight kümeniz için birincil depolama alanına toostore hello veri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c42c1-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="c42c1-163">Merhaba SimpleShortestPathsComputation örnek komut aşağıdaki hello kullanarak çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c42c1-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="c42c1-164">Bu komutla birlikte kullanılan hello parametreleri aşağıdaki tablonun hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="c42c1-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="c42c1-165">Parametre</span><span class="sxs-lookup"><span data-stu-id="c42c1-165">Parameter</span></span> | <span data-ttu-id="c42c1-166">Neler yapar?</span><span class="sxs-lookup"><span data-stu-id="c42c1-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="c42c1-167">Merhaba örnekleri içeren hello jar dosyasını.</span><span class="sxs-lookup"><span data-stu-id="c42c1-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="c42c1-168">Merhaba sınıfı toostart hello örnekler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c42c1-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="c42c1-169">kullanılan Merhaba örneği.</span><span class="sxs-lookup"><span data-stu-id="c42c1-169">hello example that is used.</span></span> <span data-ttu-id="c42c1-170">Bu örnekte, hello en kısa yolu kimliği 1 ile Merhaba Grafikteki tüm diğer kimlikleri arasında hesaplar.</span><span class="sxs-lookup"><span data-stu-id="c42c1-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="c42c1-171">Merhaba headnode hello kümesi için.</span><span class="sxs-lookup"><span data-stu-id="c42c1-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="c42c1-172">Merhaba giriş biçimi toouse hello giriş verileri için.</span><span class="sxs-lookup"><span data-stu-id="c42c1-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="c42c1-173">Merhaba giriş veri dosyasını.</span><span class="sxs-lookup"><span data-stu-id="c42c1-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="c42c1-174">Merhaba çıktı biçimi.</span><span class="sxs-lookup"><span data-stu-id="c42c1-174">hello output format.</span></span> <span data-ttu-id="c42c1-175">Bu örnek, kimlik ve düz metin olarak değeri.</span><span class="sxs-lookup"><span data-stu-id="c42c1-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="c42c1-176">Merhaba çıkış konumu.</span><span class="sxs-lookup"><span data-stu-id="c42c1-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="c42c1-177">Çalışanlar toouse Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="c42c1-177">hello number of workers toouse.</span></span> <span data-ttu-id="c42c1-178">Bu örnekte, 2.</span><span class="sxs-lookup"><span data-stu-id="c42c1-178">In this example, 2.</span></span> |

    <span data-ttu-id="c42c1-179">Bu ve Giraph örnekleri ile kullanılan diğer parametreleri hakkında daha fazla bilgi için bkz: Merhaba [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="c42c1-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="c42c1-180">Merhaba işi tamamlandıktan sonra hello sonuçları hello depolanır **/example/out/shotestpaths** dizini.</span><span class="sxs-lookup"><span data-stu-id="c42c1-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="c42c1-181">Merhaba çıktı dosyası adları ile başlayan **bölümü-m -** ve vb. dosya hello ilk olarak, ikinci olarak, belirten bir sayı ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="c42c1-182">Komut tooview hello çıktısı aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c42c1-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="c42c1-183">Merhaba çıkış metnini izleyen benzer toohello görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c42c1-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="c42c1-184">Merhaba SimpleShortestPathComputation örnek nesne kimliği 1 ile sabit kodlanmış toostart olan ve hello en kısa yolu tooother nesneleri bulun.</span><span class="sxs-lookup"><span data-stu-id="c42c1-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="c42c1-185">Merhaba çıktı hello biçiminde olduğunu `destination_id` ve `distance`.</span><span class="sxs-lookup"><span data-stu-id="c42c1-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="c42c1-186">Merhaba `distance` hello değeri (veya ağırlık) seyahat hello kenarları nesne kimliği 1 ile Merhaba hedef kimliği arasında olmalıdır</span><span class="sxs-lookup"><span data-stu-id="c42c1-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="c42c1-187">Bu veri görselleştirme, hello kısa yolları kimliği 1 ile tüm diğer nesnelerin arasında seyahat hello sonuçları doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c42c1-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="c42c1-188">Merhaba en kısa yolu kimliği 1 ile kimliği 4 arasında 5'tir.</span><span class="sxs-lookup"><span data-stu-id="c42c1-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="c42c1-189">Bu değer arasındaki hello toplam uzaklığı: <span style="color:orange">kimliği 1 ve 3</span>ve ardından <span style="color:red">kimliği 3 ve 4</span>.</span><span class="sxs-lookup"><span data-stu-id="c42c1-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Nesnelerin arasında çizilmiş kısa yolları daireler olarak çizme](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="c42c1-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c42c1-191">Next steps</span></span>

* <span data-ttu-id="c42c1-192">[Yükleme ve Hdınsight kümelerinde ton kullanma](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c42c1-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="c42c1-193">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c42c1-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
