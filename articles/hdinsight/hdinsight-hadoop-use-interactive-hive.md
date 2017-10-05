---
title: "Hdınsight'ta - Azure etkileşimli Hive kullanma | Microsoft Docs"
description: "Etkileşimli Hive (Hive LLAP üzerinde) kullanmak Hdınsight'ta öğrenin."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="c30b3-103">(Önizleme) hdınsight'ta etkileşimli Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="c30b3-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="c30b3-104">Etkileşimli (paketini yığını</span><span class="sxs-lookup"><span data-stu-id="c30b3-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="c30b3-105">[Canlı uzun ve işlem](https://cwiki.apache.org/confluence/display/Hive/LLAP)) yeni bir Hdınsight olan [küme türü](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="c30b3-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="c30b3-106">Etkileşimli Hive bellek çok daha etkileşimli ve daha hızlı Hive sorgularını yapan önbelleğe alma de sağlar.</span><span class="sxs-lookup"><span data-stu-id="c30b3-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="c30b3-107">Bu yeni özellik dünyanın, Hdınsight (Hive ve Spark kullanarak) bellek içi önbellek ile çoğu kullanıcı, esnek ve açık büyük veri çözümlerini bulut sağlar ve Gelişmiş analitikler R hizmetleriyle derin tümleştirme aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="c30b3-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="c30b3-108">Etkileşimli Hive küme Hadoop küme farklıdır.</span><span class="sxs-lookup"><span data-stu-id="c30b3-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="c30b3-109">Yalnızca Hive hizmeti de içerir.</span><span class="sxs-lookup"><span data-stu-id="c30b3-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="c30b3-110">MapReduce, Pig, Sqoop, Oozie ve diğer hizmetler bu küme türü ile yakında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="c30b3-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="c30b3-111">Etkileşimli Hive küme Hive hizmetinde yalnızca Ambari Hive görünümü, Beeline ve Hive ODBC erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c30b3-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="c30b3-112">Hive konsol, Templeton, Azure CLI ve Azure PowerShell erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="c30b3-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="c30b3-113">Etkileşimli Hive kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c30b3-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="c30b3-114">Etkileşimli Hive küme yalnızca Linux tabanlı kümelerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c30b3-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="c30b3-115">Hdınsight kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c30b3-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="c30b3-116">Etkileşimli kovanından Hive yürütme</span><span class="sxs-lookup"><span data-stu-id="c30b3-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="c30b3-117">Vardır farklı Hive sorguları nasıl yürütebilir seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="c30b3-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="c30b3-118">Ambari Hive görünümünü kullanarak Hive çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c30b3-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="c30b3-119">Hive görünümünü kullanma hakkında bilgi için bkz: [hdınsight'ta Hadoop ile Hive görünümünü kullanın](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="c30b3-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="c30b3-120">Hive Beeline kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c30b3-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="c30b3-121">Hdınsight üzerinde Beeline kullanma hakkında bilgi için bkz: [Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="c30b3-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="c30b3-122">Beeline headnode veya boş kenar düğümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="c30b3-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="c30b3-123">Bir boş kenar düğümden Beeline kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c30b3-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="c30b3-124">Boş bir edgenode ile Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="c30b3-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="c30b3-125">Hive ODBC kullanarak Hive çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c30b3-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="c30b3-126">Hive ODBC kullanma hakkında bilgi için bkz: [bağlanmak Excel için Microsoft Hive ODBC sürücüsü ile hadoop'a](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="c30b3-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="c30b3-127">**JDBC bağlantı dizesi bulmak için:**</span><span class="sxs-lookup"><span data-stu-id="c30b3-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="c30b3-128">Aşağıdaki URL'yi kullanarak ambarı'na oturum açma: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="c30b3-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="c30b3-129">Tıklatın **Hive** sol menüden.</span><span class="sxs-lookup"><span data-stu-id="c30b3-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="c30b3-130">URL'yi kopyalamak için vurgulanan simgesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c30b3-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![Hdınsight Hadoop etkileşimli Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="c30b3-132">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c30b3-132">See also</span></span>
* <span data-ttu-id="c30b3-133">[Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight'ta etkileşimli Hive kümeleri oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c30b3-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="c30b3-134">[Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md): Beeline Hive sorguları göndermek için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c30b3-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="c30b3-135">[Excel'i Microsoft Hive ODBC sürücüsü ile Hadoop için bağlama](hdinsight-connect-excel-hive-odbc-driver.md): Excel kovana bağlamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c30b3-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

