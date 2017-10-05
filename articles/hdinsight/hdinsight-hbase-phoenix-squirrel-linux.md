---
title: "Apache kullanmak Phoenix & HBase - Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Hdınsight'ta Apache Phoenix kullanmayı ve yüklemek ve hdınsight'ta HBase kümesi bağlanmak için istasyonunuzda SQuirreL yapılandırmak nasıl öğrenin."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="ae608-103">Hdınsight'ta Linux tabanlı HBase kümeleriyle Apache Phoenix kullanın</span><span class="sxs-lookup"><span data-stu-id="ae608-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="ae608-104">Nasıl kullanacağınızı öğrenin [Apache Phoenix](http://phoenix.apache.org/) ve SQLLine kullanma.</span><span class="sxs-lookup"><span data-stu-id="ae608-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="ae608-105">Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="ae608-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="ae608-106">Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="ae608-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="ae608-107">Phoenix sürümünü hdınsight'ta bilgi için [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ae608-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="ae608-108">SQLLine kullanın</span><span class="sxs-lookup"><span data-stu-id="ae608-108">Use SQLLine</span></span>
<span data-ttu-id="ae608-109">[SQLLine](http://sqlline.sourceforge.net/) SQL yürütülecek bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="ae608-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ae608-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ae608-110">Prerequisites</span></span>
<span data-ttu-id="ae608-111">SQLLine kullanmadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ae608-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="ae608-112">**Hdınsight'ta HBase kümesi**.</span><span class="sxs-lookup"><span data-stu-id="ae608-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="ae608-113">Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="ae608-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="ae608-114">**Uzak Masaüstü Protokolü aracılığıyla HBase kümesi bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="ae608-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="ae608-115">Yönergeler için bkz: [yönetmek Hdınsight'ta Hadoop kümeleri Azure portalını kullanarak][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="ae608-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="ae608-116">Bir HBase kümesi bağlandığınızda, Zookeepers birine bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae608-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="ae608-117">Her Hdınsight kümesi üç Zookeepers sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ae608-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="ae608-118">**Zookeeper ana bilgisayar adı bulunamıyor**</span><span class="sxs-lookup"><span data-stu-id="ae608-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="ae608-119">Açık Ambari göz atarak **https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="ae608-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="ae608-120">Oturum açma için HTTP (küme) kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="ae608-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="ae608-121">Tıklatın **ZooKeeper** sol menüden.</span><span class="sxs-lookup"><span data-stu-id="ae608-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="ae608-122">Üç gördüğünüz **ZooKeeper sunucusu** listelenir.</span><span class="sxs-lookup"><span data-stu-id="ae608-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="ae608-123">Birini tıklatın **ZooKeeper sunucusu** listelenir.</span><span class="sxs-lookup"><span data-stu-id="ae608-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="ae608-124">Özet bölmesinde, bulma **ana bilgisayar adı**.</span><span class="sxs-lookup"><span data-stu-id="ae608-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="ae608-125">Aşağıdakine benzer *zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="ae608-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="ae608-126">**SQLLine kullanmak için**</span><span class="sxs-lookup"><span data-stu-id="ae608-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="ae608-127">SSH kullanarak kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ae608-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="ae608-128">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ae608-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ae608-129">SSH, SQLLine çalıştırmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ae608-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="ae608-130">Bir HBase tablosu oluşturmak için aşağıdaki komutları çalıştırın ve bazı verileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae608-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="ae608-131">Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="ae608-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae608-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ae608-132">Next steps</span></span>
<span data-ttu-id="ae608-133">Bu makalede, Hdınsight'ta Apache Phoenix kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="ae608-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="ae608-134">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="ae608-134">To learn more, see:</span></span>

* <span data-ttu-id="ae608-135">[HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="ae608-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="ae608-136">[Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: uygulamalar HBase ile iletişim kurabilmesi için sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın dağıtılabilir doğrudan.</span><span class="sxs-lookup"><span data-stu-id="ae608-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="ae608-137">[Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): HBase çoğaltmayı iki Azure veri merkezi arasında yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ae608-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="ae608-138">[Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: Gerçek zamanlı nasıl [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.</span><span class="sxs-lookup"><span data-stu-id="ae608-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
