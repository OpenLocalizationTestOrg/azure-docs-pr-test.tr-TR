---
title: "Visual Studio - Azure Hdınsight (Hadoop) Data Lake araçları ile aaaHive | Microsoft Docs"
description: "Toouse hello Data Lake Visual Studio toorun için Apache Hive sorguları Azure hdınsight'ta Apache Hadoop ile nasıl araçları hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="5e903-103">Merhaba Data Lake araçları için Visual Studio kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5e903-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="5e903-104">Visual Studio tooquery için Apache Hive nasıl toouse hello Data Lake araçları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="5e903-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="5e903-105">Merhaba Data Lake araçları tooeasily izin oluşturma, gönderme ve Azure hdınsight'ta Hive sorguları tooHadoop izleyin.</span><span class="sxs-lookup"><span data-stu-id="5e903-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="5e903-106"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5e903-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="5e903-107">Azure Hdınsight (Hadoop hdınsight) kümesi</span><span class="sxs-lookup"><span data-stu-id="5e903-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5e903-108">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="5e903-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5e903-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5e903-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5e903-110">Visual Studio (sürümleri aşağıdaki hello biri):</span><span class="sxs-lookup"><span data-stu-id="5e903-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="5e903-111">Visual Studio 2013 Community/Professional/Premium/Ultimate güncelleştirme 4 ile</span><span class="sxs-lookup"><span data-stu-id="5e903-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="5e903-112">Visual Studio 2015 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="5e903-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="5e903-113">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="5e903-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="5e903-114">Visual Studio ya da Azure Data Lake araçları Visual Studio için Hdınsight araçları.</span><span class="sxs-lookup"><span data-stu-id="5e903-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="5e903-115">Bkz: [Hdınsight için Visual Studio Hadoop araçlarını kullanmaya başlamanıza](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme ve yapılandırma hello araçlar hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5e903-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="5e903-116"><a id="run"></a>Merhaba Visual Studio kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5e903-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="5e903-117">Açık **Visual Studio** seçip **yeni** > **proje** > **Azure Data Lake**  >   **HIVE** > **Hive uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="5e903-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="5e903-118">Bu proje için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5e903-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="5e903-119">Açık hello **Script.hql** bu proje ve aşağıdaki HiveQL ifadelerini hello Yapıştır ile oluşturulan dosyası:</span><span class="sxs-lookup"><span data-stu-id="5e903-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="5e903-120">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5e903-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5e903-121">`DROP TABLE`: Bu bildirimi Hello tablo zaten varsa, onu siler.</span><span class="sxs-lookup"><span data-stu-id="5e903-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="5e903-122">`CREATE EXTERNAL TABLE`: Yeni bir 'external' tablo kovanında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5e903-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="5e903-123">Dış tablolara hello tablo tanımı Hive (Merhaba veri hello özgün konumunda bırakılır) yalnızca depolayın.</span><span class="sxs-lookup"><span data-stu-id="5e903-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="5e903-124">Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e903-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="5e903-125">Örneğin, bir MapReduce işi veya Azure hizmeti.</span><span class="sxs-lookup"><span data-stu-id="5e903-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="5e903-126">Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="5e903-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="5e903-127">`ROW FORMAT`: Hello verilerin nasıl biçimlendirilmiş Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="5e903-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="5e903-128">Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="5e903-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="5e903-129">`STORED AS TEXTFILE LOCATION`: Hive hello burada verilerin depolandığı söyler (Merhaba örnek/veri dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="5e903-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="5e903-130">`SELECT`: Tüm satırların sayımını seçme Burada sütun `t4` hello değeri içeren `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="5e903-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="5e903-131">Bu ifade değerini döndürür `3` çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="5e903-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="5e903-132">`INPUT__FILE__NAME LIKE '%.log'`-Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini bildirir. günlük.</span><span class="sxs-lookup"><span data-stu-id="5e903-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="5e903-133">Bu yan tümce hello verileri içeren hello arama toohello sample.log dosyası kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="5e903-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="5e903-134">Merhaba Hello araç çubuğundan seçin **Hdınsight kümesi** bu sorgu için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="5e903-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="5e903-135">Seçin **gönderme** toorun hello deyimleri Hive işi.</span><span class="sxs-lookup"><span data-stu-id="5e903-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Gönderme çubuğu](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="5e903-137">Merhaba **Hive işi Özet** görünür ve hello işi hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5e903-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="5e903-138">Kullanım hello **yenileme** bağlantı hello kadar toorefresh hello iş bilgileri **iş durumu** çok değiştirir**tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="5e903-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![İş özeti tamamlanmış bir iş görüntüleme](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="5e903-140">Kullanım hello **iş çıktısı** bağlantı bu işin tooview hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="5e903-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="5e903-141">Görüntülediği `[ERROR] 3`, bu sorgu tarafından döndürülen hello değeri olduğu.</span><span class="sxs-lookup"><span data-stu-id="5e903-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="5e903-142">Ayrıca, bir proje oluşturmadan Hive sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e903-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="5e903-143">Kullanarak **Sunucu Gezgini**, genişletin **Azure** > **Hdınsight**Hdınsight sunucunuzun sağ tıklayın ve ardından **Hive sorgusu Yaz** .</span><span class="sxs-lookup"><span data-stu-id="5e903-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="5e903-144">Merhaba, **temp.hql** görünür, belge aşağıdaki HiveQL ifadelerini hello ekleme:</span><span class="sxs-lookup"><span data-stu-id="5e903-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="5e903-145">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5e903-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5e903-146">`CREATE TABLE IF NOT EXISTS`: Zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5e903-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="5e903-147">Çünkü hello `EXTERNAL` anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5e903-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="5e903-148">İç tablolar hello Hive veri ambarında depolanır ve Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="5e903-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5e903-149">Farklı `EXTERNAL` tablolar, bir iç tablosu da bırakarak hello alttaki verileri siler.</span><span class="sxs-lookup"><span data-stu-id="5e903-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="5e903-150">`STORED AS ORC`: En iyi duruma getirilmiş satır sütunlu (ORC) biçimindeki verileri depoları hello.</span><span class="sxs-lookup"><span data-stu-id="5e903-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="5e903-151">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="5e903-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="5e903-152">`INSERT OVERWRITE ... SELECT`: Hello satırları seçer `log4jLogs` içeren tablo `[ERROR]`, eklemeleri veri hello hello sonra `errorLogs` tablo.</span><span class="sxs-lookup"><span data-stu-id="5e903-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="5e903-153">Merhaba araç çubuğundan seçin **gönderme** toorun hello işi.</span><span class="sxs-lookup"><span data-stu-id="5e903-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="5e903-154">Kullanım hello **iş durumu** toodetermine o hello işi başarıyla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e903-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="5e903-155">Merhaba tablo, kullanım oluşturulan iş hello tooverify **Sunucu Gezgini** ve genişletin **Azure** > **Hdınsight** > Hdınsight kümenize > **Hive veritabanları** > **varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="5e903-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="5e903-156">Merhaba **günlüklerini** tablo ve hello **log4jLogs** tablo listelenir.</span><span class="sxs-lookup"><span data-stu-id="5e903-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="5e903-157"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e903-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5e903-158">Gördüğünüz gibi Visual Studio için Hdınsight araçları hello Hdınsight'ta Hive sorguları kolay bir yolu toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e903-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="5e903-159">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="5e903-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="5e903-160">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="5e903-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="5e903-161">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5e903-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5e903-162">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="5e903-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="5e903-163">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="5e903-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5e903-164">Merhaba hakkında daha fazla bilgi için Visual Studio için Hdınsight araçları:</span><span class="sxs-lookup"><span data-stu-id="5e903-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="5e903-165">Visual Studio için Hdınsight araçlarını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5e903-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
