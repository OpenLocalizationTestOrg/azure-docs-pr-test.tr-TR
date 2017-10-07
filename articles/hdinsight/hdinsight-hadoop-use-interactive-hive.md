---
title: "aaaUse etkileşimli Hive hdınsight'ta - Azure | Microsoft Docs"
description: "Bilgi nasıl toouse etkileşimli (Hive LLAP üzerinde) hdınsight'ta Hive."
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
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="4ee42-103">(Önizleme) hdınsight'ta etkileşimli Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="4ee42-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="4ee42-104">Etkileşimli (paketini yığını</span><span class="sxs-lookup"><span data-stu-id="4ee42-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="4ee42-105">[Canlı uzun ve işlem](https://cwiki.apache.org/confluence/display/Hive/LLAP)) yeni bir Hdınsight olan [küme türü](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="4ee42-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="4ee42-106">Etkileşimli Hive bellek çok daha etkileşimli ve daha hızlı Hive sorgularını yapan önbelleğe alma de sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ee42-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="4ee42-107">Bu yeni özellik Hdınsight hello birini dünyanın çoğu kullanıcı, esnek ve açık büyük veri çözümleri hello buluttaki (Hive ve Spark kullanarak) bellek içi önbellek ile yapar ve Gelişmiş analitikler R hizmetleriyle derin tümleştirme aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="4ee42-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="4ee42-108">Merhaba etkileşimli Hive küme hello Hadoop kümeden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="4ee42-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="4ee42-109">Yalnızca hello Hive hizmeti de içerir.</span><span class="sxs-lookup"><span data-stu-id="4ee42-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="4ee42-110">MapReduce, Pig, Sqoop, Oozie ve diğer hizmetler bu küme türü ile yakında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="4ee42-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="4ee42-111">Merhaba hello etkileşimli Hive küme Hive hizmetinde yalnızca hello Ambari Hive görünümünü, Beeline ve Hive ODBC erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="4ee42-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="4ee42-112">Hive konsol, Templeton, Azure CLI ve Azure PowerShell erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="4ee42-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="4ee42-113">Etkileşimli Hive kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ee42-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="4ee42-114">Etkileşimli Hive küme yalnızca Linux tabanlı kümelerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4ee42-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="4ee42-115">Hdınsight kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4ee42-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="4ee42-116">Etkileşimli kovanından Hive yürütme</span><span class="sxs-lookup"><span data-stu-id="4ee42-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="4ee42-117">Vardır farklı Hive sorguları nasıl yürütebilir seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="4ee42-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="4ee42-118">Merhaba Ambari Hive görünümünü kullanarak Hive çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4ee42-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="4ee42-119">Merhaba bilgi hello Hive görünümü kullanma hakkında bkz [kullanım hello hdınsight'ta Hadoop ile Hive görünümü](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="4ee42-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="4ee42-120">Hive Beeline kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4ee42-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="4ee42-121">Beeline kullanarak hello hakkında bilgi için bkz: [Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="4ee42-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="4ee42-122">Beeline hello headnode veya boş kenar düğümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ee42-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="4ee42-123">Bir boş kenar düğümden Beeline kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="4ee42-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="4ee42-124">Boş bir edgenode ile Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="4ee42-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="4ee42-125">Hive ODBC kullanarak Hive çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4ee42-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="4ee42-126">Hive ODBC kullanarak hello hakkında bilgi için bkz: [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="4ee42-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="4ee42-127">**toofind hello JDBC bağlantı dizesi:**</span><span class="sxs-lookup"><span data-stu-id="4ee42-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="4ee42-128">Üzerinde tooAmbari URL aşağıdaki hello kullanarak oturum açın: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="4ee42-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="4ee42-129">Tıklatın **Hive** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="4ee42-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="4ee42-130">Vurgulanan hello simgesi toocopy hello URL'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="4ee42-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![Hdınsight Hadoop etkileşimli Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="4ee42-132">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="4ee42-132">See also</span></span>
* <span data-ttu-id="4ee42-133">[Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight'ta nasıl toocreate etkileşimli Hive kümeleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4ee42-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="4ee42-134">[Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md): öğrenin nasıl toouse Beeline toosubmit Hive sorguları.</span><span class="sxs-lookup"><span data-stu-id="4ee42-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="4ee42-135">[Excel tooHadoop hello Microsoft Hive ODBC sürücüsü ile bağlantı](hdinsight-connect-excel-hive-odbc-driver.md): öğrenin nasıl tooconnect Excel tooHive.</span><span class="sxs-lookup"><span data-stu-id="4ee42-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

