---
title: "aaaUse Hadoop Hive ve Hdınsight - Azure de Uzak Masaüstü | Microsoft Docs"
description: "Nasıl tooconnect tooHadoop küme Hdınsight'ta Uzak Masaüstü'nü kullanarak öğrenin ve Hive sorguları hello Hive komut satırı arabirimi kullanarak çalıştırın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="ff5d7-103">Uzak Masaüstü kullanarak hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ff5d7-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ff5d7-104">Bu makalede, Hdınsight Uzak Masaüstü'nü kullanarak küme ve Hive çalıştırmak tooconnect tooan hello Hive komut satırı arabirimi (CLI) kullanarak nasıl sorgular öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff5d7-105">Uzak Masaüstü, Windows hello işletim sistemi olarak kullanma Hdınsight kümelerinde yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="ff5d7-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ff5d7-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ff5d7-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="ff5d7-108">Hdınsight 3.4 veya büyük, bkz [Hdınsight ve Beeline ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md) Hive sorguları doğrudan hello kümede bir komut satırından çalıştırma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="ff5d7-109"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ff5d7-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="ff5d7-110">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="ff5d7-111">Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi</span><span class="sxs-lookup"><span data-stu-id="ff5d7-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="ff5d7-112">Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar</span><span class="sxs-lookup"><span data-stu-id="ff5d7-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="ff5d7-113"><a id="connect"></a>İle Uzak Masaüstü Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="ff5d7-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="ff5d7-114">Merhaba Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin, ardından hello yönergeleri izleyerek tooit bağlayın [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="ff5d7-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="ff5d7-115"><a id="hive"></a>Merhaba Hive komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="ff5d7-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="ff5d7-116">Merhaba Hdınsight kümesi için toohello Masaüstü bağlıyken adımları toowork Hive ile aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="ff5d7-117">Merhaba Hello Hdınsight masaüstünden başlatmak **Hadoop komut satırı**.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="ff5d7-118">Komut toostart hello Hive CLI aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="ff5d7-119">Merhaba CLI başlatıldığında göreceğiniz hello Hive CLI istemi: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="ff5d7-120">Merhaba, CLI kullanarak girin deyimleri toocreate adlı yeni bir tablo aşağıdaki hello **log4jLogs** örnek verileri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="ff5d7-121">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="ff5d7-122">**DROP TABLE**: siler hello tablo ve hello veri dosyası hello tablo zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="ff5d7-123">**Dış tablo oluştur**: kovanında yeni bir 'external' tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="ff5d7-124">Dış tablolara yalnızca hello tablo tanımı Hive (Merhaba veri hello özgün konumunda bırakılır) depolayın.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="ff5d7-125">Dış tablolar, bir dış kaynağa (örneğin, bir otomatik veri karşıya yükleme işlemi) veya başka bir MapReduce işlemi tarafından güncelleştirilen veri toobe temel hello beklediğiniz ancak her zaman toouse hello en son verileri Hive sorguları istediğiniz zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="ff5d7-126">Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="ff5d7-127">**SATIR biçimi**: hello veri biçimlendirilmiş nasıl Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="ff5d7-128">Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="ff5d7-129">**AS TEXTFILE konumu DEPOLANAN**: söyler hello veri nerede Hive depolanan (Merhaba örnek/veri dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="ff5d7-130">**SEÇİN**: tüm satırların sayımını seçer Burada sütun **t4** hello değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="ff5d7-131">Bu değeri döndürmelidir **3** çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="ff5d7-132">**INPUT__FILE__NAME gibi '%.log'** -biz yalnızca veri biten dosyalarından döndürmelidir Hive söyler. günlük.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="ff5d7-133">Merhaba verileri içeren ve verileri diğer örnekten tanımladığımız hello şema eşleşmiyor veri dosyalarını döndürmesini tutar hello arama toohello sample.log dosyası kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="ff5d7-134">Aşağıdaki deyimleri toocreate adlı yeni bir 'iç' tablo kullanım hello **günlüklerini**:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="ff5d7-135">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="ff5d7-136">**Tablo IF değil var oluşturmak**: zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="ff5d7-137">Çünkü hello **dış** anahtar sözcüğü kullanılmaz, hello Hive veri ambarında depolanır ve Hive tamamen yönetilen bir iç tablosu budur.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ff5d7-138">Farklı **dış** tablolar, bir iç tablosu da bırakarak hello alttaki verileri siler.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="ff5d7-139">**AS ORC DEPOLANAN**: en iyi duruma getirilmiş satır sütun (ORC) biçiminde hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="ff5d7-140">Kovan verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimde budur.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="ff5d7-141">**INSERT ÜZERİNE... SEÇİN**: hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, eklemeleri veri hello hello sonra **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="ff5d7-142">yalnızca, satırları tooverify içeren **[Hata]** sütun t4 saklı toohello olan **günlüklerini** tablo, tüm satırları hello deyimi tooreturn aşağıdaki hello kullan **günlüklerini**:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="ff5d7-143">SEÇİN * günlüklerini; gelen</span><span class="sxs-lookup"><span data-stu-id="ff5d7-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="ff5d7-144">Üç veri satırı döndürülmesi, tüm içeren **[Hata]** sütun t4 içinde.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="ff5d7-145"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="ff5d7-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="ff5d7-146">Gördüğünüz gibi hello hello Hive komutu Hive sorguları bir Hdınsight kümesi üzerinde çalışan bir kolay bir yolu toointeractively sağlar, İzleyicisi Merhaba durumu iş ve hello çıkış almak.</span><span class="sxs-lookup"><span data-stu-id="ff5d7-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="ff5d7-147"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff5d7-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="ff5d7-148">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="ff5d7-149">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ff5d7-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ff5d7-150">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ff5d7-151">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="ff5d7-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ff5d7-152">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="ff5d7-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ff5d7-153">Tez Hive ile kullanıyorsanız, belgeleri hata ayıklama bilgileri için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="ff5d7-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="ff5d7-154">Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın</span><span class="sxs-lookup"><span data-stu-id="ff5d7-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="ff5d7-155">Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın</span><span class="sxs-lookup"><span data-stu-id="ff5d7-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
