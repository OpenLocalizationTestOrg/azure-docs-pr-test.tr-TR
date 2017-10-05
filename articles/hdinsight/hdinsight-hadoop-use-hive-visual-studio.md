---
title: "Data Lake (Hadoop) araçları ile Visual Studio - Azure Hdınsight Hive | Microsoft Docs"
description: "Azure Hdınsight'ta Apache Hadoop ile Apache Hive sorguları çalıştırmak için Visual Studio için Data Lake araçları kullanmayı öğrenin."
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
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3d4af-103">Visual Studio için Data Lake araçları kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3d4af-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="3d4af-104">Sorgu için Apache Hive Visual Studio için Data Lake araçları kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3d4af-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="3d4af-105">Data Lake araçları, kolayca oluşturmanıza, gönderme ve Azure hdınsight'ta Hadoop Hive sorguları izlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3d4af-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="3d4af-106"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3d4af-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="3d4af-107">Azure Hdınsight (Hadoop hdınsight) kümesi</span><span class="sxs-lookup"><span data-stu-id="3d4af-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3d4af-108">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="3d4af-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3d4af-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3d4af-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3d4af-110">Visual Studio (aşağıdaki sürümlerinden biri):</span><span class="sxs-lookup"><span data-stu-id="3d4af-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="3d4af-111">Visual Studio 2013 Community/Professional/Premium/Ultimate güncelleştirme 4 ile</span><span class="sxs-lookup"><span data-stu-id="3d4af-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="3d4af-112">Visual Studio 2015 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="3d4af-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="3d4af-113">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="3d4af-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="3d4af-114">Visual Studio ya da Azure Data Lake araçları Visual Studio için Hdınsight araçları.</span><span class="sxs-lookup"><span data-stu-id="3d4af-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="3d4af-115">Bkz: [Hdınsight için Visual Studio Hadoop araçlarını kullanmaya başlamanıza](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme ve yapılandırma araçları hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3d4af-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="3d4af-116"><a id="run"></a>Visual Studio kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3d4af-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="3d4af-117">Açık **Visual Studio** seçip **yeni** > **proje** > **Azure Data Lake**  >   **HIVE** > **Hive uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="3d4af-118">Bu proje için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3d4af-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="3d4af-119">Açık **Script.hql** bu proje ve aşağıdaki HiveQL ifadelerini Yapıştır ile oluşturulan dosyası:</span><span class="sxs-lookup"><span data-stu-id="3d4af-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="3d4af-120">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3d4af-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="3d4af-121">`DROP TABLE`: Tablo zaten varsa, bu deyimi bu siler.</span><span class="sxs-lookup"><span data-stu-id="3d4af-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="3d4af-122">`CREATE EXTERNAL TABLE`: Yeni bir 'external' tablo kovanında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d4af-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="3d4af-123">Dış tablolara (verileri özgün konumda bırakılır) Hive tablo tanımı yalnızca depolayın.</span><span class="sxs-lookup"><span data-stu-id="3d4af-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="3d4af-124">Dış kaynak tarafından güncelleştirilecek temel alınan veri beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d4af-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="3d4af-125">Örneğin, bir MapReduce işi veya Azure hizmeti.</span><span class="sxs-lookup"><span data-stu-id="3d4af-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="3d4af-126">Bir dış tablo bırakma mu **değil** verileri, yalnızca tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="3d4af-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="3d4af-127">`ROW FORMAT`: Veri nasıl biçimlendirilmiş Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="3d4af-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="3d4af-128">Bu durumda, her günlüğün içinde alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3d4af-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="3d4af-129">`STORED AS TEXTFILE LOCATION`: Veri depolandığı Hive söyler (örneğin/veri dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="3d4af-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="3d4af-130">`SELECT`: Tüm satırların sayımını seçme Burada sütun `t4` değeri içeren `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="3d4af-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="3d4af-131">Bu ifade değerini döndürür `3` çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="3d4af-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="3d4af-132">`INPUT__FILE__NAME LIKE '%.log'`-Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini bildirir. günlük.</span><span class="sxs-lookup"><span data-stu-id="3d4af-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="3d4af-133">Bu yan tümcesi arama verileri içeren sample.log dosyası kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="3d4af-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="3d4af-134">Araç çubuğundan seçin **Hdınsight kümesi** bu sorgu için kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="3d4af-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="3d4af-135">Seçin **gönderme** deyimleri bir Hive işi olarak çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="3d4af-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Gönderme çubuğu](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="3d4af-137">**Hive işi Özet** görünür ve çalışan iş hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3d4af-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="3d4af-138">Kullanım **yenileme** kadar iş bilgilerini yenilemek için bağlantı **iş durumu** değişikliklerini **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![İş özeti tamamlanmış bir iş görüntüleme](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="3d4af-140">Kullanım **iş çıktısı** bu işin çıktısını görüntülemek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="3d4af-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="3d4af-141">Görüntülediği `[ERROR] 3`, bu sorgu tarafından döndürülen değer olduğu.</span><span class="sxs-lookup"><span data-stu-id="3d4af-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="3d4af-142">Ayrıca, bir proje oluşturmadan Hive sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d4af-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="3d4af-143">Kullanarak **Sunucu Gezgini**, genişletin **Azure** > **Hdınsight**Hdınsight sunucunuzun sağ tıklayın ve ardından **Hive sorgusu Yaz** .</span><span class="sxs-lookup"><span data-stu-id="3d4af-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="3d4af-144">İçinde **temp.hql** görünür, belge aşağıdaki HiveQL ifadelerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d4af-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="3d4af-145">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3d4af-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="3d4af-146">`CREATE TABLE IF NOT EXISTS`: Zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d4af-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="3d4af-147">Çünkü `EXTERNAL` anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d4af-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="3d4af-148">İç tabloları Hive veri ambarında depolanır ve Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="3d4af-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3d4af-149">Farklı `EXTERNAL` tablolar, bir iç tablosu da bırakarak temel alınan verileri siler.</span><span class="sxs-lookup"><span data-stu-id="3d4af-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="3d4af-150">`STORED AS ORC`: En iyi duruma getirilmiş satır sütun (ORC) biçiminde verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="3d4af-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="3d4af-151">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="3d4af-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="3d4af-152">`INSERT OVERWRITE ... SELECT`: Satırları seçer `log4jLogs` içeren tablo `[ERROR]`, verileri ekler `errorLogs` tablo.</span><span class="sxs-lookup"><span data-stu-id="3d4af-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="3d4af-153">Araç çubuğundan seçin **gönderme** işi çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="3d4af-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="3d4af-154">Kullanım **iş durumu** işi başarıyla tamamlandığını belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="3d4af-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="3d4af-155">İş tablo oluştuğunu doğrulamak için kullanmak **Sunucu Gezgini** ve genişletin **Azure** > **Hdınsight** > Hdınsight kümenize >  **Veritabanları hive** > **varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="3d4af-156">**Günlüklerini** tablo ve **log4jLogs** tablo listelenir.</span><span class="sxs-lookup"><span data-stu-id="3d4af-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="3d4af-157"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d4af-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3d4af-158">Gördüğünüz gibi Visual Studio için Hdınsight araçları Hdınsight'ta Hive sorguları ile çalışmak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d4af-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="3d4af-159">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="3d4af-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="3d4af-160">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="3d4af-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="3d4af-161">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3d4af-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3d4af-162">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="3d4af-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="3d4af-163">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="3d4af-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="3d4af-164">Visual Studio için Hdınsight araçları hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="3d4af-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="3d4af-165">Visual Studio için Hdınsight araçlarını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3d4af-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
