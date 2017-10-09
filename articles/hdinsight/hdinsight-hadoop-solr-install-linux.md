---
title: "aaaUse betik eylemi tooinstall hdınsight'ta Linux tabanlı - Azure Solr | Microsoft Docs"
description: "Betik eylemleri kullanılarak nasıl tooinstall Solr üzerinde Linux tabanlı Hdınsight Hadoop kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="cb270-103">Yükleme ve Solr Hdınsight Hadoop kümeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="cb270-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="cb270-104">Bilgi nasıl betik eylemi kullanarak Azure hdınsight'ta Solr tooinstall.</span><span class="sxs-lookup"><span data-stu-id="cb270-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="cb270-105">Solr güçlü arama platformudur ve Hadoop tarafından yönetilen veri kuruluş düzeyinde arama yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb270-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="cb270-106">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cb270-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="cb270-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="cb270-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cb270-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cb270-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb270-109">Bu belgede kullanılan hello örnek betik, belirli bir yapılandırmayla Solr 4.9 yükler.</span><span class="sxs-lookup"><span data-stu-id="cb270-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="cb270-110">Farklı Koleksiyonlara, parça, şemalar, çoğaltmalar, vb. ile tooconfigure hello Solr kümesi istiyorsanız hello komut dosyası ve Solr ikili dosyaları değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb270-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="cb270-111"><a name="whatis"></a>Solr nedir</span><span class="sxs-lookup"><span data-stu-id="cb270-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="cb270-112">[Apache Solr](http://lucene.apache.org/solr/features.html) güçlü tam metin araması verileri sağlayan bir kurumsal arama platformudur.</span><span class="sxs-lookup"><span data-stu-id="cb270-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="cb270-113">Hadoop depolamak ve çok büyük miktarda veri yönetme olanak sağlarken, Apache Solr tooquickly hello verileri almak hello arama yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb270-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="cb270-114">Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak Microsoft tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cb270-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="cb270-115">Solr gibi özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="cb270-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="cb270-116">Microsoft destek özel bileşenlerle mümkün tooresolve sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb270-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="cb270-117">Yardım için tooengage hello açık kaynak toplulukları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="cb270-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="cb270-118">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="cb270-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="cb270-119">Hangi hello komut dosyası gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="cb270-119">What hello script does</span></span>

<span data-ttu-id="cb270-120">Bu komut dosyası değişiklikleri toohello Hdınsight kümesi aşağıdaki hello yapar:</span><span class="sxs-lookup"><span data-stu-id="cb270-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="cb270-121">Solr 4.9 içine yükler`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="cb270-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="cb270-122">Bir kullanıcı oluşturur **solrusr**, kullanılan toorun hello Solr hizmet olduğu</span><span class="sxs-lookup"><span data-stu-id="cb270-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="cb270-123">Ayarlar **solruser** hello sahibi olarak`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="cb270-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="cb270-124">Ekler bir [Upstart](http://upstart.ubuntu.com/) Solr otomatik olarak başlar yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="cb270-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="cb270-125"><a name="install"></a>Betik eylemleri kullanılarak Solr yükleyin</span><span class="sxs-lookup"><span data-stu-id="cb270-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="cb270-126">Hdınsight kümesinde bir örnek komut dosyası tooinstall Solr konumu aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="cb270-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="cb270-127">toocreate Solr yüklü olan bir küme, kullanım hello adımları hello [Hdınsight kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md) belge.</span><span class="sxs-lookup"><span data-stu-id="cb270-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="cb270-128">Merhaba oluşturma işlemi sırasında aşağıdaki adımları tooinstall Solr hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="cb270-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="cb270-129">Merhaba gelen __küme Özet__ dikey penceresinde, select__Advanced settings__, ardından __betik eylemleri__.</span><span class="sxs-lookup"><span data-stu-id="cb270-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="cb270-130">Bilgi toopopulate hello formu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="cb270-131">**AD**: hello betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="cb270-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="cb270-132">**BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="cb270-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="cb270-133">**HEAD**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="cb270-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="cb270-134">**ÇALIŞAN**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="cb270-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="cb270-135">**ZOOKEEPER**: Bu seçenek tooinstall hello Zookeeper düğümde denetleyin</span><span class="sxs-lookup"><span data-stu-id="cb270-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="cb270-136">**PARAMETRELERİ**: Bu alanı boş bırakın</span><span class="sxs-lookup"><span data-stu-id="cb270-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="cb270-137">Merhaba hello sonundaki **betik eylemleri** dikey penceresinde, kullanım hello **seçin** düğme toosave hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="cb270-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="cb270-138">Son olarak, hello kullan **sonraki** düğmesini tooreturn toohello __küme özeti__</span><span class="sxs-lookup"><span data-stu-id="cb270-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="cb270-139">Merhaba gelen __küme Özet__ sayfasında, __oluşturma__ toocreate hello küme.</span><span class="sxs-lookup"><span data-stu-id="cb270-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="cb270-140"><a name="usesolr"></a>Hdınsight'ta nasıl Solr kullanıyor</span><span class="sxs-lookup"><span data-stu-id="cb270-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb270-141">Bu bölümdeki Hello adımları temel Solr işlevleri göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="cb270-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="cb270-142">Merhaba Solr kullanma hakkında daha fazla bilgi için bkz: [Apache Solr site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="cb270-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="cb270-143">Dizin verileri</span><span class="sxs-lookup"><span data-stu-id="cb270-143">Index data</span></span>

<span data-ttu-id="cb270-144">Aşağıdaki adımları tooadd örnek veri tooSolr hello kullanın ve ardından sorgu:</span><span class="sxs-lookup"><span data-stu-id="cb270-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="cb270-145">SSH kullanarak toohello Hdınsight kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="cb270-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cb270-146">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cb270-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="cb270-147">Adımları bu belgenin sonraki bölümlerinde bir SSL tünel tooconnect toohello Solr web kullanıcı arabirimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb270-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="cb270-148">Aşağıdaki adımları toouse, bir SSL kurmak gerekir tünel ve tarayıcı toouse yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="cb270-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="cb270-149">Daha fazla bilgi için bkz: Merhaba [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="cb270-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="cb270-150">Aşağıdaki komutları toohave Solr dizin örnek verileri hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="cb270-151">Merhaba aşağıdaki çıktı toohello konsol döndürülür:</span><span class="sxs-lookup"><span data-stu-id="cb270-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="cb270-152">Merhaba `post.jar` yardımcı programı ekler hello **solr.xml** ve **monitor.xml** belgeleri toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="cb270-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="cb270-153">Komut tooquery hello Solr REST API aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="cb270-154">Bu komut arar **collection1** eşleşen herhangi bir belgeniz için  **\*:\***  (olarak kodlanmış \*% 3A\* hello sorgu dizesinde).</span><span class="sxs-lookup"><span data-stu-id="cb270-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="cb270-155">JSON belgesini aşağıdaki hello hello yanıt örneğidir:</span><span class="sxs-lookup"><span data-stu-id="cb270-155">hello following JSON document is an example of hello response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="cb270-156">Merhaba Solr panosunu kullanma</span><span class="sxs-lookup"><span data-stu-id="cb270-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="cb270-157">Merhaba Solr Pano web tarayıcınız üzerinden Solr ile toowork veren UI bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="cb270-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="cb270-158">Merhaba Solr Pano doğrudan Hdınsight kümenize gelen hello Internet üzerinde açık değil.</span><span class="sxs-lookup"><span data-stu-id="cb270-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="cb270-159">Bir SSH tünel tooaccess kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb270-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="cb270-160">SSH tüneli kullanma hakkında daha fazla bilgi için bkz: Merhaba [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="cb270-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="cb270-161">SSH tüneli kurduktan sonra aşağıdaki adımları toouse hello Solr Pano hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="cb270-162">Merhaba birincil headnode Hello ana bilgisayar adını belirleyin:</span><span class="sxs-lookup"><span data-stu-id="cb270-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="cb270-163">SSH tooconnect toohello küme baş düğümüne kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb270-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="cb270-164">Örneğin, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="cb270-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="cb270-165">Merhaba SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cb270-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="cb270-166">Tooget hello tam ana bilgisayar adı komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="cb270-167">Bu komut, ana bilgisayar adından bir değer benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="cb270-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="cb270-168">Daha sonra kullanılmak üzere döndürülen, hello değeri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cb270-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="cb270-169">Tarayıcınızda, çok bağlantı**solr/http://HOSTNAME:8983 / #/**, burada **ana bilgisayar adı** hello önceki adımlarda belirlenen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="cb270-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="cb270-170">Merhaba isteği kümenizde hello SSH tünel toohello Solr web kullanıcı Arabirimi üzerinden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="cb270-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="cb270-171">Görüntü aşağıdaki benzer toohello Hello sayfası görünür:</span><span class="sxs-lookup"><span data-stu-id="cb270-171">hello page appears similar toohello following image:</span></span>

    ![Solr Pano görüntüsü](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="cb270-173">Merhaba Hello sol bölmesinden kullanmak **çekirdek Seçici** açılan tooselect **collection1**.</span><span class="sxs-lookup"><span data-stu-id="cb270-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="cb270-174">Birden çok girişi bunları altında görünmelidir **collection1**.</span><span class="sxs-lookup"><span data-stu-id="cb270-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="cb270-175">Aşağıdaki hello girişlerinden **collection1**seçin **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="cb270-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="cb270-176">Değerleri toopopulate hello arama sayfası aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="cb270-177">Merhaba, **q** metin kutusuna  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="cb270-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="cb270-178">Bu sorgu Solr dizini tüm hello belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="cb270-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="cb270-179">Belirli bir dizeyi hello belgelerde toosearch istiyorsanız, o dizeyi buraya girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb270-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="cb270-180">Merhaba, **wt** metin kutusunda, select hello çıktı biçimi.</span><span class="sxs-lookup"><span data-stu-id="cb270-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="cb270-181">Varsayılan değer **json**.</span><span class="sxs-lookup"><span data-stu-id="cb270-181">Default is **json**.</span></span>

     <span data-ttu-id="cb270-182">Son olarak, hello seçin **sorgu yürütme** hello arama pate hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb270-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="cb270-184">Merhaba çıkış iki belge toohello eklenen önceki dizini hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="cb270-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="cb270-185">Merhaba, benzer toohello JSON belgesi aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="cb270-185">hello output is similar toohello following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="cb270-186">Başlatma ve durdurma Solr</span><span class="sxs-lookup"><span data-stu-id="cb270-186">Starting and stopping Solr</span></span>

<span data-ttu-id="cb270-187">Toomanually durdurma ve Solr başlatma komutları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="cb270-188">Veri yedekleme dizini</span><span class="sxs-lookup"><span data-stu-id="cb270-188">Backup indexed data</span></span>

<span data-ttu-id="cb270-189">Solr veri toohello varsayılan depolamayı kümeniz için adımları tooback aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cb270-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="cb270-190">SSH kullanarak toohello kümesine bağlanın, sonra komutu tooget hello ana bilgisayar adı hello baş düğümü için aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="cb270-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="cb270-191">Komut toocreate dizine hello verilerin bir anlık görüntüsünü aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb270-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="cb270-192">Değiştir **ana bilgisayar adı** hello önceki komuttan döndürülen hello adı ile:</span><span class="sxs-lookup"><span data-stu-id="cb270-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="cb270-193">Merhaba yanıt benzer toohello XML aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="cb270-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="cb270-194">Dizinleri çok değiştirin`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="cb270-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="cb270-195">Bir alt burada her koleksiyon için yoktur.</span><span class="sxs-lookup"><span data-stu-id="cb270-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="cb270-196">Her koleksiyon dizini içeren bir `data` hello koleksiyon için başlangıç anlık görüntü içeren dizini.</span><span class="sxs-lookup"><span data-stu-id="cb270-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="cb270-197">toocreate hello anlık görüntü klasörü, komutu aşağıdaki kullanım hello sıkıştırılmış bir arşiv:</span><span class="sxs-lookup"><span data-stu-id="cb270-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="cb270-198">Hello yerine `snapshot.20150806185338855` koleksiyonunuz için başlangıç anlık görüntüsünün hello ad değerlerle.</span><span class="sxs-lookup"><span data-stu-id="cb270-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="cb270-199">Bu komut, adlandırılmış bir arşiv oluşturur **snapshot.20150806185338855.tgz**, hello Merhaba içeriğine içeren **snapshot.20150806185338855** dizini.</span><span class="sxs-lookup"><span data-stu-id="cb270-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="cb270-200">Sonra komutu aşağıdaki hello kullanarak hello arşiv toohello kümenin birincil depolama depolayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cb270-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="cb270-201">Solr yedekleme ve geri yükleme ile çalışma hakkında daha fazla bilgi için bkz: [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="cb270-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb270-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb270-202">Next steps</span></span>

* <span data-ttu-id="cb270-203">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb270-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="cb270-204">Giraph üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb270-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="cb270-205">Giraph tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cb270-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="cb270-206">[Hdınsight kümelerinde Hue yüklemek](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb270-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="cb270-207">Küme özelleştirme tooinstall ton Hdınsight Hadoop kümeleri üzerinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb270-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="cb270-208">Hue Web uygulamaları toointeract Hadoop kümesi ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cb270-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
