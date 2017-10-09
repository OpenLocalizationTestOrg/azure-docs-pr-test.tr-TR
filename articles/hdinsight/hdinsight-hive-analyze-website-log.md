---
title: "Web sitesi günlüğü analizi - Azure Hdınsight için Hadoop ile Hive aaaUse | Microsoft Docs"
description: "Toouse Hive Hdınsight tooanalyze Web sitesiyle nasıl günlüğe yazacağını öğrenin. Bir Hdınsight tabloya giriş olarak bir günlük dosyasını kullanın ve HiveQL tooquery hello verileri kullanmak."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="35816-104">Web siteleri tooanalyze günlüklerinden Windows tabanlı Hdınsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="35816-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="35816-105">Bir Web sitesinden toouse HiveQL Hdınsight tooanalyze ile nasıl oturum öğrenin.</span><span class="sxs-lookup"><span data-stu-id="35816-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="35816-106">Web sitesi günlüğü analizi kullanılan toosegment kitlenizi benzer etkinliklere dayalı olması, site ziyaretçilerini demografisine ve toofind görüntüledikleri hello içerik, geliyor hello Web siteleri ve benzeri tarafından kategorilere ayırma.</span><span class="sxs-lookup"><span data-stu-id="35816-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35816-107">Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları.</span><span class="sxs-lookup"><span data-stu-id="35816-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="35816-108">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35816-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="35816-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="35816-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="35816-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="35816-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="35816-111">Bu örnekte, bir günde bir Hdınsight kümesi tooanalyze Web sitesi günlük dosyaları tooget fikirler dış Web sitelerini ziyaret toohello sitesinden hello sıklığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="35816-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="35816-112">Ayrıca hello kullanıcı deneyimi Web sitesi hatalarının özetini oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="35816-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="35816-113">Şunları öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="35816-113">You will learn how to:</span></span>

* <span data-ttu-id="35816-114">Tooa Web sitesinin günlük dosyalarını içeren Azure Blob depolama alanına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="35816-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="35816-115">Oluşturma HIVE tabloları tooquery Bu günlükleri.</span><span class="sxs-lookup"><span data-stu-id="35816-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="35816-116">HIVE sorguları tooanalyze hello veri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35816-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="35816-117">Microsoft Excel tooconnect tooHDInsight kullanın (açık veritabanı bağlantısı (ODBC) tooretrieve analiz hello verileri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="35816-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="35816-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35816-119">Prerequisites</span></span>
* <span data-ttu-id="35816-120">Azure Hdınsight Hadoop kümesinde sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="35816-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="35816-121">Yönergeler için bkz: [sağlama Hdınsight kümeleri][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="35816-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="35816-122">Excel 2010 yüklü veya Microsoft Excel 2013 yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35816-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="35816-123">Bilmeniz gereken [Microsoft Hive ODBC sürücüsü](http://www.microsoft.com/download/details.aspx?id=40886) Hive Excel'e tooimport verileri.</span><span class="sxs-lookup"><span data-stu-id="35816-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="35816-124">toorun hello örnek</span><span class="sxs-lookup"><span data-stu-id="35816-124">toorun hello sample</span></span>
1. <span data-ttu-id="35816-125">Merhaba gelen [Azure Portal](https://portal.azure.com/), Hello ifadesini (Merhaba küme sabitlenmiş varsa) sabitlemek istediğiniz toorun hello örnek hello küme kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35816-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="35816-126">Hello dikey penceresinde altında küme **hızlı bağlantılar**, tıklatın **küme Panosu**ve sonra hello **küme Panosu** dikey penceresinde'ı tıklatın **Hdınsight kümesi Pano**.</span><span class="sxs-lookup"><span data-stu-id="35816-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="35816-127">Alternatif olarak, URL aşağıdaki hello kullanarak hello Pano doğrudan açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="35816-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="35816-128">İstendiğinde, hello yönetici kullanıcı adını ve hello küme hazırlama sırasında kullanılan parola kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="35816-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="35816-129">Hello web açan sayfasından hello tıklatın **alma başlatıldı galeri** sekmesinde hello altında ve **örnek verilerle çözümleri** kategorisi, hello tıklatın **Web sitesi günlüğü analizi** örnek.</span><span class="sxs-lookup"><span data-stu-id="35816-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="35816-130">Merhaba web sayfası toofinish hello örnek üzerinde sağlanan hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="35816-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35816-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35816-131">Next steps</span></span>
<span data-ttu-id="35816-132">Aşağıdaki örnek hello deneyin: [Hdınsight ile Hive kullanma algılayıcı verilerini çözümleme](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="35816-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
