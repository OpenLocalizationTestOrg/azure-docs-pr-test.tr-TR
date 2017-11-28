---
title: "Hadoop kümesi - Azure üzerinde aaaUse betik eylemi tooinstall Solr | Microsoft Docs"
description: "Toocustomize Hdınsight ile betik eylemi kullanarak Solr nasıl küme öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="9350f-103">Yükleme ve Windows tabanlı Hdınsight kümelerinde Solr kullanma</span><span class="sxs-lookup"><span data-stu-id="9350f-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="9350f-104">Toocustomize Windows tabanlı Hdınsight kümesi nasıl ile betik eylemi kullanarak Solr ve nasıl öğrenin toouse Solr toosearch veri.</span><span class="sxs-lookup"><span data-stu-id="9350f-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9350f-105">Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları.</span><span class="sxs-lookup"><span data-stu-id="9350f-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9350f-106">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9350f-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="9350f-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="9350f-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9350f-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9350f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="9350f-109">Linux tabanlı bir kümeyle Solr kullanma hakkında daha fazla bilgi için bkz: [yükleme ve kullanma Solr Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9350f-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="9350f-110">Solr Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde kullanarak yükleyebileceğiniz *betik eylemi*.</span><span class="sxs-lookup"><span data-stu-id="9350f-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="9350f-111">Hdınsight kümesinde bir örnek komut dosyası tooinstall Solr salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="9350f-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="9350f-112">Merhaba örnek betik yalnızca Hdınsight küme sürümü ile 3.1 çalışır.</span><span class="sxs-lookup"><span data-stu-id="9350f-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="9350f-113">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9350f-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="9350f-114">Bu konuda kullanılan hello örnek betik, belirli bir yapılandırmayla Windows tabanlı Solr küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9350f-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="9350f-115">Farklı Koleksiyonlara, parça, şemalar, çoğaltmalar, vb. ile tooconfigure hello Solr kümesi istiyorsanız hello komut dosyası ve Solr ikili dosyaları uygun şekilde değiştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9350f-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="9350f-116">**İlgili makaleler**</span><span class="sxs-lookup"><span data-stu-id="9350f-116">**Related articles**</span></span>

* [<span data-ttu-id="9350f-117">Yükleme ve Solr Hdınsight Hadoop kümeleri (Linux) kullanma</span><span class="sxs-lookup"><span data-stu-id="9350f-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="9350f-118">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="9350f-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="9350f-119">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="9350f-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="9350f-120">[Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="9350f-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="9350f-121">Solr nedir?</span><span class="sxs-lookup"><span data-stu-id="9350f-121">What is Solr?</span></span>
<span data-ttu-id="9350f-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> güçlü tam metin araması verileri sağlayan bir kurumsal arama platformudur.</span><span class="sxs-lookup"><span data-stu-id="9350f-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="9350f-123">Hadoop depolamak ve çok büyük miktarda veri yönetme olanak sağlarken, Apache Solr tooquickly hello verileri almak hello arama yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9350f-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="9350f-124">Portal kullanarak Solr yükleyin</span><span class="sxs-lookup"><span data-stu-id="9350f-124">Install Solr using portal</span></span>
1. <span data-ttu-id="9350f-125">Hello kullanarak bir küme oluşturmaya başlamak **özel Oluştur** konusunda açıklandığı gibi seçeneği [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9350f-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="9350f-126">Hello üzerinde **betik eylemleri** sayfa hello Sihirbazı'nın tıklatın **betik eylemi eklemek** tooprovide aşağıda gösterildiği gibi hello betik eylemi hakkında ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="9350f-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="9350f-127">![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "kullanım betik eylemi toocustomize küme")</span><span class="sxs-lookup"><span data-stu-id="9350f-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="9350f-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="9350f-128">Property</span></span></th><th><span data-ttu-id="9350f-129">Değer</span><span class="sxs-lookup"><span data-stu-id="9350f-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="9350f-130">Ad</span><span class="sxs-lookup"><span data-stu-id="9350f-130">Name</span></span></td>
            <td><span data-ttu-id="9350f-131">Merhaba betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="9350f-131">Specify a name for hello script action.</span></span> <span data-ttu-id="9350f-132">Örneğin, <b>yükleme Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="9350f-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="9350f-133">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="9350f-133">Script URI</span></span></td>
            <td><span data-ttu-id="9350f-134">Çağrılan toocustomize hello küme hello Tekdüzen Kaynak Tanımlayıcısı (URI) toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9350f-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="9350f-135">Örneğin, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="9350f-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="9350f-136">Düğüm Türü</span><span class="sxs-lookup"><span data-stu-id="9350f-136">Node Type</span></span></td>
            <td><span data-ttu-id="9350f-137">Merhaba özelleştirme betik çalıştığı hello düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="9350f-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="9350f-138">Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>yalnızca çalışan düğümleri</b>.</span><span class="sxs-lookup"><span data-stu-id="9350f-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="9350f-139">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9350f-139">Parameters</span></span></td>
            <td><span data-ttu-id="9350f-140">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="9350f-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="9350f-141">Bunu boş bırakabilirsiniz şekilde hello betik tooinstall Solr herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="9350f-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="9350f-142">Birden fazla betik eylemi tooinstall hello kümede birden çok bileşen ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9350f-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="9350f-143">Merhaba komut dosyaları ekledikten sonra hello küme oluşturma hello onay işareti toostart tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9350f-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="9350f-144">Solr kullanma</span><span class="sxs-lookup"><span data-stu-id="9350f-144">Use Solr</span></span>
<span data-ttu-id="9350f-145">Bazı veri dosyalarıyla Solr dizin ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9350f-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="9350f-146">Bu gibi durumlarda, Solr toorun arama sorguları sonra dizine hello verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9350f-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="9350f-147">Bir Hdınsight kümesindeki adımları toouse Solr aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9350f-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="9350f-148">**Uzak Masaüstü Protokolü (RDP) tooremote hello Hdınsight kümesine yüklü Solr ile kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="9350f-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="9350f-149">Azure portal Hello Uzak Masaüstü Solr yüklü ve ardından uzak içine hello kümesi ile oluşturulan hello küme için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9350f-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="9350f-150">Yönergeler için bkz: [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="9350f-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="9350f-151">**Dizin veri dosyaları yükleyerek Solr**.</span><span class="sxs-lookup"><span data-stu-id="9350f-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="9350f-152">Solr dizin oluşturduğunuzda üzerinde toosearch gerekebilir, belgeleri yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="9350f-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="9350f-153">tooindex Solr, kullanım RDP tooremote hello kümesine toohello Masaüstü gidin, hello Hadoop komut satırı açın ve çok gidin**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="9350f-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="9350f-154">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9350f-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="9350f-155">Çıktı hello konsolda aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="9350f-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="9350f-156">Merhaba post.jar yardımcı programı, iki örnek belgelerle Solr dizinler **solr.xml** ve **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="9350f-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="9350f-157">Merhaba post.jar yardımcı programı ve hello örnek belgeler Solr yükleme ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9350f-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="9350f-158">**Kullanım hello Solr Pano toosearch hello içinde dizine belgeleri**.</span><span class="sxs-lookup"><span data-stu-id="9350f-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="9350f-159">Merhaba RDP oturumu toohello Hdınsight küme, Internet Explorer'ı açın ve hello Solr Panosu'nda başlatın **solr/http://headnodehost:8983 / #/**.</span><span class="sxs-lookup"><span data-stu-id="9350f-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="9350f-160">Merhaba gelen hello sol bölmesinde **çekirdek Seçici** açılan listesinde, select **collection1**, tıklatıp, içinde **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="9350f-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="9350f-161">Bir örnek, tooselect ve return olarak Solr, içindeki tüm hello belgeleri değerleri aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="9350f-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="9350f-162">Merhaba, **q** metin kutusuna  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="9350f-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="9350f-163">Bu dizini tüm hello belgeleri Solr döndürür.</span><span class="sxs-lookup"><span data-stu-id="9350f-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="9350f-164">Belirli bir dizeyi hello belgelerde toosearch istiyorsanız, o dizeyi buraya girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9350f-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="9350f-165">Merhaba, **wt** metin kutusunda, select hello çıktı biçimi.</span><span class="sxs-lookup"><span data-stu-id="9350f-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="9350f-166">Varsayılan değer **json**.</span><span class="sxs-lookup"><span data-stu-id="9350f-166">Default is **json**.</span></span> <span data-ttu-id="9350f-167">Tıklatın **sorgu yürütme**.</span><span class="sxs-lookup"><span data-stu-id="9350f-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="9350f-168">![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Solr Panoda bir sorgu çalıştırın")</span><span class="sxs-lookup"><span data-stu-id="9350f-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="9350f-169">Merhaba çıktı hello için dizin oluşturma Solr kullandık iki belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9350f-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="9350f-170">Merhaba çıktı hello aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="9350f-170">hello output resembles hello following:</span></span>

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
4. <span data-ttu-id="9350f-171">**Önerilen: Hello yedekleme Solr tooAzure hello Hdınsight kümesi ile ilişkili Blob Depolama verileri dizine**.</span><span class="sxs-lookup"><span data-stu-id="9350f-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="9350f-172">İyi bir uygulama hello Solr küme düğümlerinden Azure Blob Depolama üzerine dizine hello verileri yedeklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9350f-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="9350f-173">Adımları toodo şekilde aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9350f-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="9350f-174">Merhaba RDP oturumu, Internet Explorer ve noktası URL aşağıdaki toohello açın:</span><span class="sxs-lookup"><span data-stu-id="9350f-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="9350f-175">Şuna benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="9350f-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="9350f-176">Merhaba uzak oturumda çok gidin {SOLR_HOME}\{koleksiyonu} \data.</span><span class="sxs-lookup"><span data-stu-id="9350f-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="9350f-177">Merhaba örnek komut dosyası oluşturulan hello küme için bu olmalıdır **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="9350f-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="9350f-178">Bu konumda bir adla çok benzer oluşturulmuş bir anlık görüntü klasörü görmelisiniz**anlık görüntü.* zaman damgası***.</span><span class="sxs-lookup"><span data-stu-id="9350f-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="9350f-179">Başlangıç anlık görüntü klasörü zip ve tooAzure Blob storage'ı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9350f-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="9350f-180">Merhaba Hadoop komut satırından komutu aşağıdaki hello kullanarak toohello hello anlık görüntü klasörü konumunu gidin:</span><span class="sxs-lookup"><span data-stu-id="9350f-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="9350f-181">Kopya anlık görüntü çok/örnek/data hello/hello varsayılan depolama hello kapsayıcıda altında hello kümesi ile ilişkili hesap bu komutu.</span><span class="sxs-lookup"><span data-stu-id="9350f-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="9350f-182">Solr işlemleri PowerShell kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="9350f-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="9350f-183">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="9350f-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="9350f-184">Merhaba örnek gösterilmektedir nasıl tooinstall Azure PowerShell kullanarak Spark.</span><span class="sxs-lookup"><span data-stu-id="9350f-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="9350f-185">Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="9350f-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="9350f-186">.NET SDK kullanarak Solr yükleyin</span><span class="sxs-lookup"><span data-stu-id="9350f-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="9350f-187">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="9350f-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="9350f-188">Merhaba örnek gösterilmektedir nasıl tooinstall Spark hello .NET SDK kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9350f-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="9350f-189">Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="9350f-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="9350f-190">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9350f-190">See also</span></span>
* [<span data-ttu-id="9350f-191">Yükleme ve Solr Hdınsight Hadoop kümeleri (Linux) kullanma</span><span class="sxs-lookup"><span data-stu-id="9350f-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="9350f-192">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="9350f-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="9350f-193">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="9350f-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="9350f-194">[Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="9350f-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="9350f-195">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: Spark yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="9350f-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="9350f-196">[Hdınsight kümelerinde R yüklemek][hdinsight-install-r]: betik eylemi örnek r yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="9350f-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="9350f-197">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install.md): Giraph yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="9350f-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
