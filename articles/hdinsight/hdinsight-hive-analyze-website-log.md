---
title: "Web sitesi günlüğü analizi - Azure Hdınsight Hadoop ile Hive kullanma | Microsoft Docs"
description: "Web sitesi günlüklerini çözümlemek için Hdınsight ile Hive kullanma öğrenin. Bir Hdınsight tabloya giriş olarak bir günlük dosyası kullanmak ve verileri sorgulamak için HiveQL kullanma."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="d5893-104">Web sitesi günlüklerini çözümlemek için Windows tabanlı Hdınsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="d5893-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="d5893-105">Bir Web sitesi günlüklerini çözümlemek için Hdınsight ile HiveQL kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d5893-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="d5893-106">Web sitesi günlüğü analizi benzer etkinliklere dayalı kitlenizi segmentlere, site ziyaretçilerini demografisine göre kategorilere ayırmak ve bulmak için içeriği teslim bunlar görünümü, Web siteleri geliyor ve benzeri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5893-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5893-107">Bu belgede yer alan adımlar, yalnızca Windows tabanlı Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="d5893-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d5893-108">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5893-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="d5893-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="d5893-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d5893-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d5893-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d5893-111">Bu örnekte, ziyaretlerin sıklığını Web sitesine dış Web sitelerinden bir gün içinde bir anlayış almak için Web sitesinin günlük dosyalarını çözümlemek için Hdınsight kümesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d5893-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="d5893-112">Ayrıca, kullanıcının karşılaştığı Web sitesi hatalarının özetini oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d5893-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="d5893-113">Şunları öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="d5893-113">You will learn how to:</span></span>

* <span data-ttu-id="d5893-114">Web sitesinin günlük dosyalarını içeren ve Azure Blob Depolama birimine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d5893-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="d5893-115">HIVE tablolarını Bu günlükleri sorgu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d5893-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="d5893-116">Verileri çözümlemek için HIVE sorguları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d5893-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="d5893-117">Hdınsight'a (açık veritabanı bağlantısı (ODBC) çözümlenen verileri almak üzere kullanarak. bağlanmak için Microsoft Excel kullanın</span><span class="sxs-lookup"><span data-stu-id="d5893-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="d5893-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d5893-119">Prerequisites</span></span>
* <span data-ttu-id="d5893-120">Azure Hdınsight Hadoop kümesinde sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5893-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="d5893-121">Yönergeler için bkz: [sağlama Hdınsight kümeleri][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="d5893-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="d5893-122">Excel 2010 yüklü veya Microsoft Excel 2013 yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5893-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="d5893-123">Bilmeniz gereken [Microsoft Hive ODBC sürücüsü](http://www.microsoft.com/download/details.aspx?id=40886) kovanından Excel'e veri almak için.</span><span class="sxs-lookup"><span data-stu-id="d5893-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="d5893-124">Örneği çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="d5893-124">To run the sample</span></span>
1. <span data-ttu-id="d5893-125">Gelen [Azure Portal](https://portal.azure.com/), (küme var. sabitlenmiş varsa) Sabitle gelen istediğiniz örneği çalıştırmak küme kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5893-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="d5893-126">Küme dikey penceresinden altında **hızlı bağlantılar**, tıklatın **küme Panosu**ve sonra **küme Panosu** dikey penceresinde tıklatın **Hdınsight küme Panosu**.</span><span class="sxs-lookup"><span data-stu-id="d5893-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="d5893-127">Alternatif olarak, aşağıdaki URL'yi kullanarak Pano doğrudan açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d5893-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="d5893-128">İstendiğinde, yönetici kullanıcı adını ve küme hazırlama sırasında kullanılan parola kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="d5893-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="d5893-129">Web açan sayfasından tıklatın **alma başlatıldı galeri** sekmesi ve ardından **örnek verilerle çözümleri** kategorisi, tıklatın **Web sitesi günlüğü analizi** örnek.</span><span class="sxs-lookup"><span data-stu-id="d5893-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="d5893-130">Örnek tamamlamak için web sayfasında sağlanan yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d5893-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5893-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5893-131">Next steps</span></span>
<span data-ttu-id="d5893-132">Aşağıdaki örnek deneyin: [Hdınsight ile Hive kullanma algılayıcı verilerini çözümleme](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="d5893-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
