---
title: "aaaUse Apache Phoenix & HBase - Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Bilgi nasıl toouse, hdınsight'ta Apache Phoenix ve nasıl tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta yapılandırın."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="f6174-103">Hdınsight'ta Linux tabanlı HBase kümeleriyle Apache Phoenix kullanın</span><span class="sxs-lookup"><span data-stu-id="f6174-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="f6174-104">Bilgi nasıl toouse [Apache Phoenix](http://phoenix.apache.org/) , hdınsight'ta ve nasıl toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="f6174-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="f6174-105">Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="f6174-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="f6174-106">Hello Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="f6174-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="f6174-107">Hello hdınsight'ta Phoenix sürüm bilgileri için bkz: [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f6174-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="f6174-108">SQLLine kullanın</span><span class="sxs-lookup"><span data-stu-id="f6174-108">Use SQLLine</span></span>
<span data-ttu-id="f6174-109">[SQLLine](http://sqlline.sourceforge.net/) komut satırı yardımcı programını tooexecute SQL değil.</span><span class="sxs-lookup"><span data-stu-id="f6174-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f6174-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f6174-110">Prerequisites</span></span>
<span data-ttu-id="f6174-111">SQLLine kullanmadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f6174-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="f6174-112">**Hdınsight'ta HBase kümesi**.</span><span class="sxs-lookup"><span data-stu-id="f6174-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="f6174-113">Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="f6174-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="f6174-114">**Toohello HBase kümesi hello Uzak Masaüstü Protokolü aracılığıyla bağlanma**.</span><span class="sxs-lookup"><span data-stu-id="f6174-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="f6174-115">Yönergeler için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="f6174-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="f6174-116">Tooan HBase kümesi bağlandığınızda, hello Zookeepers, tooconnect tooone gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6174-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="f6174-117">Her Hdınsight kümesi üç Zookeepers sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f6174-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="f6174-118">**toofind hello Zookeeper ana bilgisayar adı çıkışı**</span><span class="sxs-lookup"><span data-stu-id="f6174-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="f6174-119">Açık Ambari çok göz atarak**https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="f6174-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="f6174-120">Merhaba HTTP (küme) kullanıcı adı ve parola toologin girin.</span><span class="sxs-lookup"><span data-stu-id="f6174-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="f6174-121">Tıklatın **ZooKeeper** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="f6174-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="f6174-122">Üç gördüğünüz **ZooKeeper sunucusu** listelenir.</span><span class="sxs-lookup"><span data-stu-id="f6174-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="f6174-123">Merhaba birini tıklatın **ZooKeeper sunucusu** listelenir.</span><span class="sxs-lookup"><span data-stu-id="f6174-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="f6174-124">Merhaba Özet bölmesinde hello bulur **ana bilgisayar adı**.</span><span class="sxs-lookup"><span data-stu-id="f6174-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="f6174-125">Çok benzer*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="f6174-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="f6174-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="f6174-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="f6174-127">SSH kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="f6174-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="f6174-128">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f6174-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f6174-129">SSH'den aşağıdaki komutları toorun SQLLine hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f6174-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="f6174-130">Bir HBase tablosu komutları toocreate aşağıdaki hello çalıştırın ve bazı verileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f6174-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="f6174-131">Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="f6174-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6174-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6174-132">Next steps</span></span>
<span data-ttu-id="f6174-133">Bu makalede, öğrendiğiniz nasıl toouse hdınsight'ta Apache Phoenix.</span><span class="sxs-lookup"><span data-stu-id="f6174-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="f6174-134">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="f6174-134">toolearn more, see:</span></span>

* <span data-ttu-id="f6174-135">[HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="f6174-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="f6174-136">[Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın böylece dağıtılan toohello olabilir uygulamalar ile iletişim kurabilir Doğrudan HBase.</span><span class="sxs-lookup"><span data-stu-id="f6174-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="f6174-137">[Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): öğrenin nasıl tooconfigure HBase çoğaltmayı iki Azure veri merkezleri arasında.</span><span class="sxs-lookup"><span data-stu-id="f6174-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="f6174-138">[Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: öğrenin nasıl toodo gerçek zamanlı [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.</span><span class="sxs-lookup"><span data-stu-id="f6174-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
