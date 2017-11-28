---
title: "Linux tabanlı Hdınsight üzerinde - Azure Solr yüklemek için betik eylemi kullanın | Microsoft Docs"
description: "Betik eylemleri kullanarak Linux tabanlı Hdınsight Hadoop kümeleri üzerinde Solr yüklemeyi öğrenin."
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
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="13fcb-103">Yükleme ve Solr Hdınsight Hadoop kümeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="13fcb-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="13fcb-104">Betik eylemi kullanarak Azure Hdınsight'ta Solr yüklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="13fcb-105">Solr güçlü arama platformudur ve Hadoop tarafından yönetilen veri kuruluş düzeyinde arama yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="13fcb-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="13fcb-106">Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="13fcb-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="13fcb-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="13fcb-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13fcb-109">Bu belgede kullanılan örnek betik, belirli bir yapılandırmayla Solr 4.9 yükler.</span><span class="sxs-lookup"><span data-stu-id="13fcb-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="13fcb-110">Farklı Koleksiyonlara, parça, şemalar, çoğaltmalar, vb. ile Solr küme yapılandırmak istiyorsanız, Solr ikili dosyaları ve komut dosyasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="13fcb-111"><a name="whatis"></a>Solr nedir</span><span class="sxs-lookup"><span data-stu-id="13fcb-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="13fcb-112">[Apache Solr](http://lucene.apache.org/solr/features.html) güçlü tam metin araması verileri sağlayan bir kurumsal arama platformudur.</span><span class="sxs-lookup"><span data-stu-id="13fcb-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="13fcb-113">Hadoop depolamak ve çok büyük miktarda veri yönetme olanak sağlarken, Apache Solr hızlı bir şekilde veri almak için arama yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="13fcb-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="13fcb-114">Hdınsight kümesi ile sağlanan bileşenler tam olarak Microsoft tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="13fcb-115">Özel bileşenleri, Solr, örneğin, daha fazla sorun gidermenize yardımcı olması için ticari koşulların elverdiği oranda makul destek alırsınız.</span><span class="sxs-lookup"><span data-stu-id="13fcb-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="13fcb-116">Microsoft destek özel bileşenlerle sorunları gidermek mümkün olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="13fcb-117">Yardım için açık kaynak toplulukları devreye gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="13fcb-118">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="13fcb-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="13fcb-119">Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="13fcb-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="13fcb-120">Betiğin yaptığı</span><span class="sxs-lookup"><span data-stu-id="13fcb-120">What the script does</span></span>

<span data-ttu-id="13fcb-121">Bu komut, Hdınsight kümesine aşağıdaki değişiklikleri yapar:</span><span class="sxs-lookup"><span data-stu-id="13fcb-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="13fcb-122">Solr 4.9 içine yükler`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="13fcb-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="13fcb-123">Bir kullanıcı oluşturur **solrusr**, Solr hizmetini çalıştırmak için kullanılan</span><span class="sxs-lookup"><span data-stu-id="13fcb-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="13fcb-124">Ayarlar **solruser** sahibi olarak`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="13fcb-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="13fcb-125">Ekler bir [Upstart](http://upstart.ubuntu.com/) Solr otomatik olarak başlar yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="13fcb-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="13fcb-126"><a name="install"></a>Betik eylemleri kullanılarak Solr yükleyin</span><span class="sxs-lookup"><span data-stu-id="13fcb-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="13fcb-127">Solr bir Hdınsight kümesine yüklemek için örnek komut dosyası şu konumda kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="13fcb-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="13fcb-128">Solr yüklü olan bir küme oluşturmak için adımlarda kullanın [Hdınsight kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md) belge.</span><span class="sxs-lookup"><span data-stu-id="13fcb-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="13fcb-129">Oluşturma işlemi sırasında Solr yüklemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="13fcb-130">Gelen __küme Özet__ dikey penceresinde, select__Advanced settings__, ardından __betik eylemleri__.</span><span class="sxs-lookup"><span data-stu-id="13fcb-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="13fcb-131">Form doldurmak için aşağıdaki bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="13fcb-132">**AD**: betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="13fcb-133">**BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="13fcb-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="13fcb-134">**HEAD**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="13fcb-135">**ÇALIŞAN**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="13fcb-136">**ZOOKEEPER**: Zookeeper düğümüne yüklemek için bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="13fcb-137">**PARAMETRELERİ**: Bu alanı boş bırakın</span><span class="sxs-lookup"><span data-stu-id="13fcb-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="13fcb-138">Ekranın alt kısmındaki **betik eylemleri** dikey penceresinde, kullanım **seçin** yapılandırmayı kaydetmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="13fcb-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="13fcb-139">Son olarak, **sonraki** geri dönmek için düğmesini __küme özeti__</span><span class="sxs-lookup"><span data-stu-id="13fcb-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="13fcb-140">Gelen __küme Özet__ sayfasında, __oluşturma__ küme oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="13fcb-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="13fcb-141"><a name="usesolr"></a>Hdınsight'ta nasıl Solr kullanıyor</span><span class="sxs-lookup"><span data-stu-id="13fcb-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13fcb-142">Bu bölümdeki adımları temel Solr işlevleri göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="13fcb-143">Solr kullanma hakkında daha fazla bilgi için bkz: [Apache Solr site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="13fcb-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="13fcb-144">Dizin verileri</span><span class="sxs-lookup"><span data-stu-id="13fcb-144">Index data</span></span>

<span data-ttu-id="13fcb-145">Solr için örnek veri eklemek için aşağıdaki adımları kullanın ve ardından sorgu:</span><span class="sxs-lookup"><span data-stu-id="13fcb-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="13fcb-146">SSH kullanarak HDInsight kümesine bağlanma:</span><span class="sxs-lookup"><span data-stu-id="13fcb-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="13fcb-147">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="13fcb-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="13fcb-148">Adımları bu belgenin sonraki bölümlerinde SSL tüneli Solr web kullanıcı Arabirimine bağlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="13fcb-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="13fcb-149">Bu adımları kullanabilmek için bir SSL tünel oluşturmak ve daha sonra kullanmak için tarayıcınızı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="13fcb-150">Daha fazla bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="13fcb-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="13fcb-151">Solr dizin örnek veri sağlamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="13fcb-152">Aşağıdaki çıktıyı konsola verilir:</span><span class="sxs-lookup"><span data-stu-id="13fcb-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="13fcb-153">`post.jar` Yardımcı programı ekler **solr.xml** ve **monitor.xml** dizine belgeleri.</span><span class="sxs-lookup"><span data-stu-id="13fcb-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="13fcb-154">Solr REST API sorgulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="13fcb-155">Bu komut arar **collection1** eşleşen herhangi bir belgeniz için  **\*:\***  (olarak kodlanmış \*% 3A\* sorgu dizesinde).</span><span class="sxs-lookup"><span data-stu-id="13fcb-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="13fcb-156">Aşağıdaki JSON belgesi, yanıt örneğidir:</span><span class="sxs-lookup"><span data-stu-id="13fcb-156">The following JSON document is an example of the response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, the Enterprise Search Server",
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
                      "Scalability - Efficient Replication to other Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over the e)"
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

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="13fcb-157">Solr panosunu kullanma</span><span class="sxs-lookup"><span data-stu-id="13fcb-157">Using the Solr dashboard</span></span>

<span data-ttu-id="13fcb-158">Solr Pano web tarayıcınız üzerinden Solr ile çalışmanıza olanak sağlayan kullanıcı Arabirimi bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="13fcb-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="13fcb-159">Solr Pano doğrudan Internet'ten, Hdınsight kümesi üzerinde açık değil.</span><span class="sxs-lookup"><span data-stu-id="13fcb-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="13fcb-160">SSH tüneli erişmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13fcb-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="13fcb-161">SSH tüneli kullanma hakkında daha fazla bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="13fcb-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="13fcb-162">SSH tüneli kurduktan sonra Solr panoyu kullanmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="13fcb-163">Birincil headnode ana bilgisayar adını belirleyin:</span><span class="sxs-lookup"><span data-stu-id="13fcb-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="13fcb-164">SSH küme baş düğümüne bağlanmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="13fcb-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="13fcb-165">Örneğin, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="13fcb-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="13fcb-166">SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="13fcb-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="13fcb-167">Tam ana bilgisayar adı almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="13fcb-168">Bu komutu aşağıdaki ana bilgisayar adı için benzer bir değer döndürür:</span><span class="sxs-lookup"><span data-stu-id="13fcb-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="13fcb-169">Daha sonra kullanılmak üzere döndürdü, değer kaydedin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="13fcb-170">Tarayıcınızda, bağlanmak **solr/http://HOSTNAME:8983 / #/**, burada **ana bilgisayar adı** önceki adımlarda belirlenen adıdır.</span><span class="sxs-lookup"><span data-stu-id="13fcb-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="13fcb-171">İstek, kümenizde Solr Web Arabirimine SSH tüneli üzerinden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="13fcb-172">Sayfa aşağıdaki görüntüye benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="13fcb-172">The page appears similar to the following image:</span></span>

    ![Solr Pano görüntüsü](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="13fcb-174">Sol bölmeden kullanmak **çekirdek Seçici** seçmek için açılır **collection1**.</span><span class="sxs-lookup"><span data-stu-id="13fcb-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="13fcb-175">Birden çok girişi bunları altında görünmelidir **collection1**.</span><span class="sxs-lookup"><span data-stu-id="13fcb-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="13fcb-176">Girişlerden **collection1**seçin **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="13fcb-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="13fcb-177">Arama sayfası doldurmak için aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="13fcb-178">İçinde **q** metin kutusuna  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="13fcb-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="13fcb-179">Bu sorgu Solr dizini tüm belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="13fcb-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="13fcb-180">Belirli bir dizeyi belgelerde arama yapmak istiyorsanız, o dizeyi buraya girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13fcb-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="13fcb-181">İçinde **wt** metin kutusunda, çıktı biçimi seçin.</span><span class="sxs-lookup"><span data-stu-id="13fcb-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="13fcb-182">Varsayılan değer **json**.</span><span class="sxs-lookup"><span data-stu-id="13fcb-182">Default is **json**.</span></span>

     <span data-ttu-id="13fcb-183">Son olarak, seçin **sorgu yürütme** arama pate sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="13fcb-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Bir küme özelleştirmek için betik eylemi kullanın](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="13fcb-185">Çıktı dizini daha önce eklediğimiz iki belge döndürür.</span><span class="sxs-lookup"><span data-stu-id="13fcb-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="13fcb-186">Çıktı aşağıdaki JSON belgesi benzer:</span><span class="sxs-lookup"><span data-stu-id="13fcb-186">The output is similar to the following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
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
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="13fcb-187">Başlatma ve durdurma Solr</span><span class="sxs-lookup"><span data-stu-id="13fcb-187">Starting and stopping Solr</span></span>

<span data-ttu-id="13fcb-188">El ile durdurun ve Solr başlatmak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="13fcb-189">Veri yedekleme dizini</span><span class="sxs-lookup"><span data-stu-id="13fcb-189">Backup indexed data</span></span>

<span data-ttu-id="13fcb-190">Kümeniz için varsayılan depolama Solr verileri yedeklemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="13fcb-191">SSH kullanarak kümeye bağlanın, ardından baş düğüm için ana bilgisayar adı almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="13fcb-192">Dizinli verilerin bir anlık görüntüsünü oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="13fcb-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="13fcb-193">Değiştir **ana bilgisayar adı** önceki komuttan döndürülen adı ile:</span><span class="sxs-lookup"><span data-stu-id="13fcb-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="13fcb-194">Yanıt aşağıdaki XML'e benzer:</span><span class="sxs-lookup"><span data-stu-id="13fcb-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="13fcb-195">Değiştirme dizinleri `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="13fcb-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="13fcb-196">Bir alt burada her koleksiyon için yoktur.</span><span class="sxs-lookup"><span data-stu-id="13fcb-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="13fcb-197">Her koleksiyon dizini içeren bir `data` koleksiyonu için anlık görüntü içeren dizini.</span><span class="sxs-lookup"><span data-stu-id="13fcb-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="13fcb-198">Sıkıştırılmış bir anlık görüntü klasörü arşiv oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13fcb-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="13fcb-199">Değiştir `snapshot.20150806185338855` koleksiyonunuz için anlık görüntü adı değerlerle.</span><span class="sxs-lookup"><span data-stu-id="13fcb-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="13fcb-200">Bu komut, adlandırılmış bir arşiv oluşturur **snapshot.20150806185338855.tgz**, içeriğini içeren **snapshot.20150806185338855** dizini.</span><span class="sxs-lookup"><span data-stu-id="13fcb-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="13fcb-201">Ardından aşağıdaki komutu kullanarak kümenin birincil depolama arşive depolayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="13fcb-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="13fcb-202">Solr yedekleme ve geri yükleme ile çalışma hakkında daha fazla bilgi için bkz: [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="13fcb-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13fcb-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13fcb-203">Next steps</span></span>

* <span data-ttu-id="13fcb-204">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="13fcb-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="13fcb-205">Küme özelleştirme Giraph Hdınsight Hadoop kümelerine yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="13fcb-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="13fcb-206">Giraph Hadoop kullanarak işleme grafik işlemleri yapmanıza olanak tanır ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="13fcb-207">[Hdınsight kümelerinde Hue yüklemek](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="13fcb-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="13fcb-208">Küme özelleştirme Hdınsight Hadoop kümeleri üzerinde Hue yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="13fcb-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="13fcb-209">Hue Hadoop kümeyle etkileşim kurmak için kullanılan Web uygulamaları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="13fcb-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
