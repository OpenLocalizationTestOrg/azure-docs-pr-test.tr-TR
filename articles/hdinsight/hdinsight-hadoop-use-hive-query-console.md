---
title: "Merhaba sorgu konsol hdınsight'ta - Azure üzerinde Hadoop Hive aaaUse | Microsoft Docs"
description: "Nasıl toouse hello web tabanlı sorgu konsol toorun Hive sorguları bir Hdınsight Hadoop üzerinde tarayıcınızdan küme öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="cbae8-103">Merhaba sorgu Konsolu kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cbae8-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="cbae8-104">Bu makalede, nasıl toouse hello Hdınsight sorgu konsol toorun Hive sorguları bir Hdınsight Hadoop üzerinde tarayıcınızdan küme öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="cbae8-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbae8-105">Merhaba Hdınsight sorgu konsolu yalnızca Windows tabanlı Hdınsight kümelerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cbae8-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="cbae8-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="cbae8-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cbae8-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cbae8-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="cbae8-108">Hdınsight 3.4 veya büyük, bkz [Hive sorgularını çalıştırma Ambari Hive görünümünde](hdinsight-hadoop-use-hive-ambari-view.md) bir web tarayıcısından Hive sorguları çalıştırma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="cbae8-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="cbae8-109"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cbae8-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="cbae8-110">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbae8-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="cbae8-111">Windows tabanlı Hdınsight Hadoop kümesi</span><span class="sxs-lookup"><span data-stu-id="cbae8-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="cbae8-112">Modern bir web tarayıcısı</span><span class="sxs-lookup"><span data-stu-id="cbae8-112">A modern web browser</span></span>

## <span data-ttu-id="cbae8-113"><a id="run"></a>Merhaba sorgu Konsolu kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cbae8-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="cbae8-114">Bir web tarayıcısı açın ve çok gidin**https://CLUSTERNAME.azurehdinsight.net**, burada **CLUSTERNAME** Hdınsight kümenize hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="cbae8-115">İstenirse, hello kullanıcı adı ve hello küme oluştururken kullandığınız parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="cbae8-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="cbae8-116">Merhaba sayfanın üst kısmındaki hello Hello bağlantılardan birini seçin **Hive Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="cbae8-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="cbae8-117">Bu, kullanılan tooenter hello HiveQL ifadelerini toorun hello Hdınsight kümesinde istediğiniz olabilir bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="cbae8-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![Merhaba hive Düzenleyicisi](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="cbae8-119">Merhaba metnin yerine `Select * from hivesampletable` aşağıdaki HiveQL ifadelerini hello ile:</span><span class="sxs-lookup"><span data-stu-id="cbae8-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="cbae8-120">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cbae8-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="cbae8-121">**DROP TABLE**: siler hello tablo ve hello veri dosyası hello tablo zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="cbae8-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="cbae8-122">**Dış tablo oluştur**: kovanında yeni bir 'external' tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cbae8-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="cbae8-123">Dış tablolara yalnızca hello tablo tanımı kovanında depolamak; Merhaba veri hello özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cbae8-124">Dış tablolar, bir dış kaynağa (örneğin, bir otomatik veri karşıya yükleme işlemi) veya başka bir MapReduce işlemi tarafından güncelleştirilen veri toobe temel hello beklediğiniz ancak her zaman toouse hello en son verileri Hive sorguları istediğiniz zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="cbae8-125">Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="cbae8-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="cbae8-126">**SATIR biçimi**: hello veri biçimlendirilmiş nasıl Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="cbae8-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="cbae8-127">Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="cbae8-128">**AS TEXTFILE konumu DEPOLANAN**: söyler hello veri nerede Hive depolanan (Merhaba örnek/veri dizini) ve metin olarak depolanır</span><span class="sxs-lookup"><span data-stu-id="cbae8-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="cbae8-129">**SEÇİN**: tüm satırların sayımını seçin burada sütun **t4** hello değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="cbae8-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="cbae8-130">Bu değeri döndürmelidir **3** çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="cbae8-131">**INPUT__FILE__NAME gibi '%.log'** -biz yalnızca veri biten dosyalarından döndürmelidir Hive söyler. günlük.</span><span class="sxs-lookup"><span data-stu-id="cbae8-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="cbae8-132">Merhaba verileri içeren ve verileri diğer örnekten tanımladığımız hello şema eşleşmiyor veri dosyalarını döndürmesini tutar hello arama toohello sample.log dosyası kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="cbae8-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="cbae8-133">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="cbae8-133">Click **Submit**.</span></span> <span data-ttu-id="cbae8-134">Merhaba **proje oturumunu** hello hello sayfanın hello işe yönelik ayrıntıları görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbae8-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="cbae8-135">Ne zaman hello **durum** değişiklikleri alan çok**tamamlandı**seçin **ayrıntıları görüntüle** hello işi için.</span><span class="sxs-lookup"><span data-stu-id="cbae8-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="cbae8-136">Merhaba Ayrıntıları sayfasında hello **iş çıktısı** içeren `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="cbae8-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="cbae8-137">Merhaba kullanabilirsiniz **karşıdan** hello çıktısını hello içeren bir dosyayı bu alan toodownload altında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cbae8-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="cbae8-138"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="cbae8-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="cbae8-139">Gördüğünüz gibi kolay bir yolu toorun sorgu Konsolu sağlar hello Hdınsight kümesinde bir Hive sorguları hello iş durumunu izlemek ve hello çıkış almak.</span><span class="sxs-lookup"><span data-stu-id="cbae8-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="cbae8-140">Hive sorgusu konsol toorun Hive işlerini kullanma hakkında daha fazla toolearn seçin **Başlarken** hello sorgu konsol hello üst kısmında, ardından sağlanan hello örnekleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="cbae8-141">Her örnek Hive tooanalyze verileri hello örnekte kullanılan hello HiveQL ifadelerini hakkında açıklamalar dahil olmak üzere, kullanarak hello işlemi anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cbae8-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="cbae8-142"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbae8-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="cbae8-143">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="cbae8-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="cbae8-144">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="cbae8-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="cbae8-145">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cbae8-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="cbae8-146">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="cbae8-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="cbae8-147">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="cbae8-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="cbae8-148">Tez Hive ile kullanıyorsanız, belgeleri hata ayıklama bilgileri için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cbae8-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="cbae8-149">Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın</span><span class="sxs-lookup"><span data-stu-id="cbae8-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="cbae8-150">Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın</span><span class="sxs-lookup"><span data-stu-id="cbae8-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
