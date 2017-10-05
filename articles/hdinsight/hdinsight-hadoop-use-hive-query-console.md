---
title: "Sorgu konsolunda hdınsight'ta - Azure Hadoop Hive kullanma | Microsoft Docs"
description: "Web tabanlı sorgu konsol tarayıcınızdan bir Hdınsight Hadoop kümesindeki Hive sorguları çalıştırmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="2a673-103">Sorgu konsolunu kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2a673-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2a673-104">Bu makalede, Hdınsight sorgu konsol tarayıcınızdan bir Hdınsight Hadoop kümesindeki Hive sorguları çalıştırmak için nasıl kullanılacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2a673-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a673-105">Hdınsight sorgu konsolu yalnızca Windows tabanlı Hdınsight kümelerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a673-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2a673-106">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="2a673-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2a673-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2a673-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="2a673-108">Hdınsight 3.4 veya büyük, bkz [Hive sorgularını çalıştırma Ambari Hive görünümünde](hdinsight-hadoop-use-hive-ambari-view.md) bir web tarayıcısından Hive sorguları çalıştırma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="2a673-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="2a673-109"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2a673-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="2a673-110">Bu makaledeki adımları tamamlamak için aşağıdakiler gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a673-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="2a673-111">Windows tabanlı Hdınsight Hadoop kümesi</span><span class="sxs-lookup"><span data-stu-id="2a673-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="2a673-112">Modern bir web tarayıcısı</span><span class="sxs-lookup"><span data-stu-id="2a673-112">A modern web browser</span></span>

## <span data-ttu-id="2a673-113"><a id="run"></a>Sorgu konsolunu kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2a673-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="2a673-114">Bir web tarayıcısı açın ve gidin **https://CLUSTERNAME.azurehdinsight.net**, burada **CLUSTERNAME** Hdınsight kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="2a673-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="2a673-115">İstenirse, kullanıcı adını ve küme oluştururken kullandığınız parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="2a673-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="2a673-116">Sayfanın üstündeki bağlantılardan birini seçin **Hive Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="2a673-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="2a673-117">Bu, Hdınsight kümesinde çalıştırmak istediğiniz HiveQL ifadelerini girmek için kullanılan bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2a673-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![hive düzenleyicisinin](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="2a673-119">Metnin yerine `Select * from hivesampletable` aşağıdaki HiveQL ifadelerini ile:</span><span class="sxs-lookup"><span data-stu-id="2a673-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="2a673-120">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a673-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2a673-121">**DROP TABLE**: Tablo zaten varsa, tablo ve veri dosyasını siler.</span><span class="sxs-lookup"><span data-stu-id="2a673-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="2a673-122">**Dış tablo oluştur**: kovanında yeni bir 'external' tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2a673-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="2a673-123">Dış tablolara yalnızca tablo tanımı kovanında depolamak; veriler özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="2a673-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2a673-124">Bir dış kaynağa (örneğin, bir otomatik veri karşıya yükleme işlemi) veya başka bir MapReduce işlemi tarafından güncelleştirilecek temel alınan veri beklediğiniz dış tablolara kullanılması gereken, ancak her zaman en son verileri kullanmak üzere Hive sorguları istiyor.</span><span class="sxs-lookup"><span data-stu-id="2a673-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="2a673-125">Bir dış tablo bırakma mu **değil** verileri, yalnızca tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="2a673-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="2a673-126">**SATIR biçimi**: verileri nasıl biçimlendirildiğini Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="2a673-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="2a673-127">Bu durumda, her günlüğün içinde alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="2a673-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="2a673-128">**AS TEXTFILE konumu DEPOLANAN**: (örneğin/veri dizini) depolanan verileri nerede Hive bildirir ve metin olarak depolanır</span><span class="sxs-lookup"><span data-stu-id="2a673-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="2a673-129">**SEÇİN**: tüm satırların sayımını seçin burada sütun **t4** değerini içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="2a673-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="2a673-130">Bu değeri döndürmelidir **3** çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="2a673-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="2a673-131">**INPUT__FILE__NAME gibi '%.log'** -biz yalnızca veri biten dosyalarından döndürmelidir Hive söyler. günlük.</span><span class="sxs-lookup"><span data-stu-id="2a673-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="2a673-132">Bu arama verileri içeren ve verileri diğer örnekten tanımladığımız şema eşleşmiyor veri dosyalarını döndürmesini tutar sample.log dosyasına kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="2a673-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="2a673-133">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="2a673-133">Click **Submit**.</span></span> <span data-ttu-id="2a673-134">**Proje oturumunu** sayfasının en altında işe yönelik ayrıntıları görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a673-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="2a673-135">Zaman **durum** alan değişiklikleri **tamamlandı**seçin **ayrıntıları görüntüle** iş için.</span><span class="sxs-lookup"><span data-stu-id="2a673-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="2a673-136">Ayrıntıları sayfasında **iş çıktısı** içeren `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="2a673-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="2a673-137">Kullanabileceğiniz **karşıdan** düğmesi iş çıkışını içeren bir dosyayı indirmek için bu alanı altında.</span><span class="sxs-lookup"><span data-stu-id="2a673-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="2a673-138"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="2a673-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="2a673-139">Gördüğünüz gibi sorgu konsolu bir Hdınsight kümesi Hive sorgularını çalıştırma, iş durumunu izleyebilir ve çıkış almak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a673-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="2a673-140">Hive işlerini çalıştırmak için Hive sorgusu konsolunu kullanma hakkında daha fazla bilgi için seçin **Başlarken** sorgu konsol üst kısmında, ardından sağlanan örnekleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a673-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="2a673-141">Her örnek örnekte kullanılan HiveQL ifadelerini hakkında açıklamalar dahil verileri analiz etmek için Hive kullanma sürecinde size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="2a673-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="2a673-142"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a673-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="2a673-143">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="2a673-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="2a673-144">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="2a673-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2a673-145">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a673-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2a673-146">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="2a673-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2a673-147">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="2a673-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="2a673-148">Tez Hive ile kullanıyorsanız, hata ayıklama bilgileri için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="2a673-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="2a673-149">Windows tabanlı Hdınsight üzerinde Tez kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="2a673-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="2a673-150">Linux tabanlı Hdınsight üzerinde Ambari Tez görünümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="2a673-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
