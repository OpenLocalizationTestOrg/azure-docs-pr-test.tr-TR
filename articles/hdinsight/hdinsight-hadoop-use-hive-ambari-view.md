---
title: "Hive Hdınsight (Hadoop) - Azure üzerinde çalışmak için Ambari görünümleri kullanma | Microsoft Docs"
description: "Web tarayıcınız Hive görünümünden Hive sorguları göndermek için nasıl kullanılacağını öğrenin. Hive görünümü Ambari Web kullanıcı Arabirimi ile Linux tabanlı Hdınsight kümenizi sağlanan bir parçasıdır."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="ffd07-104">Hdınsight'ta Hadoop ile Hive görünümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="ffd07-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ffd07-105">Ambari Hive görünümünü kullanarak Hive sorguları çalıştırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ffd07-105">Learn how to run Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="ffd07-106">Ambari, yönetim ve izleme yardımcı programı Linux tabanlı Hdınsight kümeleri ile sağlanan ' dir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="ffd07-107">Ambari sağlanan özelliklerden birini Hive sorguları çalıştırmak için kullanılan bir Web UI'dır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-107">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="ffd07-108">Ambari, bu belgede ele alınan değil birçok özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="ffd07-109">Daha fazla bilgi için bkz: [Hdınsight kümelerini yönetme Ambari Web kullanıcı arabirimini kullanarak](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="ffd07-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffd07-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ffd07-110">Prerequisites</span></span>

* <span data-ttu-id="ffd07-111">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="ffd07-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ffd07-112">Küme oluşturma hakkında daha fazla bilgi için bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ffd07-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffd07-113">Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ffd07-114">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ffd07-115">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ffd07-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="ffd07-116">Hive görünümü Aç</span><span class="sxs-lookup"><span data-stu-id="ffd07-116">Open the Hive view</span></span>

<span data-ttu-id="ffd07-117">Ambari görünümleri Azure portalından yapabilirsiniz; Hdınsight kümenize seçin ve ardından **Ambari görünümleri** gelen **hızlı bağlantılar** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ffd07-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![portal hızlı bağlantılar bölümü](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="ffd07-119">Görünüm listesinden __Hive görünümü__.</span><span class="sxs-lookup"><span data-stu-id="ffd07-119">From the list of views, select the __Hive View__.</span></span>

![Seçilen Hive görünümü](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="ffd07-121">Ambari erişirken siteye kimlik doğrulaması yapmak istenir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-121">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="ffd07-122">Yönetici girin (varsayılan `admin`) hesap adı ve küme oluştururken kullanılan parola.</span><span class="sxs-lookup"><span data-stu-id="ffd07-122">Enter the admin (default `admin`) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="ffd07-123">Aşağıdaki görüntüye benzer bir sayfa görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ffd07-123">You should see a page similar to the following image:</span></span>

![Hive görünümü için sorgu çalışma sayfası görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="ffd07-125"><a name="hivequery"></a>Sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ffd07-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="ffd07-126">Bir hive sorgusu çalıştırmak için Hive görünümünden aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ffd07-126">To run a hive query, use the following steps from the Hive view.</span></span>

1. <span data-ttu-id="ffd07-127">Gelen __sorgu__ sekmesinde, aşağıdaki HiveQL ifadelerini çalışma sayfasına yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="ffd07-127">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="ffd07-128">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ffd07-128">These statements perform the following actions:</span></span>

   * <span data-ttu-id="ffd07-129">`DROP TABLE`-Tablonun ve veri dosyası siler durumda tablo zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="ffd07-129">`DROP TABLE` - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="ffd07-130">`CREATE EXTERNAL TABLE`-Kovanında yeni bir "dış" tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ffd07-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="ffd07-131">Dış tablolara yalnızca tablo tanımı kovanında depolar.</span><span class="sxs-lookup"><span data-stu-id="ffd07-131">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="ffd07-132">Veriler özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-132">The data is left in the original location.</span></span>

   * <span data-ttu-id="ffd07-133">`ROW FORMAT`-Nasıl veri biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-133">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="ffd07-134">Bu durumda, her günlüğün içinde alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-134">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="ffd07-135">`STORED AS TEXTFILE LOCATION`-Verilerin depolandığı ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-135">`STORED AS TEXTFILE LOCATION` - Where the data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="ffd07-136">`SELECT`-Sütun t4 [Hata] değeri, içerdiği tüm satırların sayımını seçer.</span><span class="sxs-lookup"><span data-stu-id="ffd07-136">`SELECT` - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="ffd07-137">Dış kaynak tarafından güncelleştirilecek temel alınan veri beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-137">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="ffd07-138">Örneğin, bir otomatik veri karşıya yükleme işlem, veya başka bir MapReduce işlemi tarafından.</span><span class="sxs-lookup"><span data-stu-id="ffd07-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="ffd07-139">Bir dış tablo bırakma mu *değil* verileri, yalnızca tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="ffd07-139">Dropping an external table does *not* delete the data, only the table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ffd07-140">Bırakın __veritabanı__ seçimi daha __varsayılan__.</span><span class="sxs-lookup"><span data-stu-id="ffd07-140">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="ffd07-141">Bu belgedeki örneklerde, Hdınsight ile dahil varsayılan veritabanı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ffd07-141">The examples in this document use the default database included with HDInsight.</span></span>

2. <span data-ttu-id="ffd07-142">Sorguyu başlatmak için kullanmak **yürütme** çalışma aşağıdaki düğmesine.</span><span class="sxs-lookup"><span data-stu-id="ffd07-142">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="ffd07-143">Turuncu kapatır ve metin değişir **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="ffd07-143">It turns orange and the text changes to **Stop**.</span></span>

3. <span data-ttu-id="ffd07-144">Sorgu tamamladığında **sonuçları** sekmesi işlemin sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ffd07-144">Once the query has finished, The **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="ffd07-145">Sorgunun sonucu metindir:</span><span class="sxs-lookup"><span data-stu-id="ffd07-145">The following text is the result of the query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="ffd07-146">**Günlükleri** sekmesi, işlem tarafından oluşturulan günlük bilgilerini görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-146">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="ffd07-147">**Sonuçları Kaydet** açılan iletişim kutusunda üst sol üst **sorgu işleminin sonuçları** bölümü indirin veya sonuçları kaydetmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ffd07-147">The **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="ffd07-148">Bu sorgunun ilk dört satırları seçin ve ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="ffd07-148">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="ffd07-149">İş tamamlandığında, hiçbir sonuç olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ffd07-149">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="ffd07-150">Kullanarak **yürütme** sorgu parçası seçildiğinde düğmesi yalnızca seçilen ifadeleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="ffd07-150">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="ffd07-151">Bu durumda, seçim tablosundan satır alır son deyim eklemediniz.</span><span class="sxs-lookup"><span data-stu-id="ffd07-151">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="ffd07-152">Yalnızca bu satırı seçin ve kullanırsanız **yürütme**, beklenen sonuçları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-152">If you select just that line and use **Execute**, you should see the expected results.</span></span>

5. <span data-ttu-id="ffd07-153">Bir çalışma sayfası eklemek için kullanın **yeni çalışma sayfası** alt kısmındaki düğmesi **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="ffd07-153">To add a worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="ffd07-154">Yeni çalışma sayfasında, aşağıdaki HiveQL ifadelerini girin:</span><span class="sxs-lookup"><span data-stu-id="ffd07-154">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="ffd07-155">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ffd07-155">These statements perform the following actions:</span></span>

   * <span data-ttu-id="ffd07-156">**Tablo IF değil var oluşturmak** -zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ffd07-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="ffd07-157">Bu yana **dış** anahtar sözcüğü kullanılmaz, bir iç tablosu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ffd07-157">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="ffd07-158">Bir iç tablosu Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-158">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="ffd07-159">Dış tablolara, bir iç tablosu bırakarak temel alınan veri de siler.</span><span class="sxs-lookup"><span data-stu-id="ffd07-159">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="ffd07-160">**AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="ffd07-160">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ffd07-161">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="ffd07-162">**INSERT ÜZERİNE... SEÇİN** -satırları seçer **log4jLogs** içeren tablo `[ERROR]`ve ardından verileri ekler **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="ffd07-162">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain `[ERROR]`, and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="ffd07-163">Kullanım **yürütme** bu sorguyu çalıştırmak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ffd07-163">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="ffd07-164">**Sonuçları** sekmesinde sorgu sıfır satır geri döndüğünde herhangi bir bilgi içermiyor.</span><span class="sxs-lookup"><span data-stu-id="ffd07-164">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="ffd07-165">Durum olarak göstermelidir **başarılı** sorgu işlemi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="ffd07-165">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="ffd07-166">Visual açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="ffd07-166">Visual explain</span></span>

<span data-ttu-id="ffd07-167">Görsel sorgu planı olarak görüntülenecek seçin **Visual açıklayan** sekmenin çalışma altında.</span><span class="sxs-lookup"><span data-stu-id="ffd07-167">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="ffd07-168">**Visual açıklayan** sorgu görünümünü karmaşık sorgular akışını anlamak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-168">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="ffd07-169">Bu görünüm metinsel denk kullanarak görüntüleyebileceğiniz **açıklama** düğmesi sorgu Düzenleyicisi'nde.</span><span class="sxs-lookup"><span data-stu-id="ffd07-169">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="ffd07-170">Tez kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="ffd07-170">Tez UI</span></span>

<span data-ttu-id="ffd07-171">Sorgu için Tez UI görüntülemek için seçin **Tez** sekmenin çalışma altında.</span><span class="sxs-lookup"><span data-stu-id="ffd07-171">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffd07-172">Tez tüm sorguları çözümlemek için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ffd07-172">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="ffd07-173">Çok sayıda sorgu, Tez kullanmadan çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="ffd07-174">Tez sorgusunu çözümlemek için kullanıldıysa, yönlendirilmiş Çevrimsiz grafik (DAG) görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-174">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="ffd07-175">Olduğunuz çalıştırdı geçmişte ya da Tez işlemde hata ayıklamak sorguları kullanmak için DAG görüntülemek istiyorsanız [Tez Görünüm](hdinsight-debug-ambari-tez-view.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="ffd07-175">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="ffd07-176">İş geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ffd07-176">View job history</span></span>

<span data-ttu-id="ffd07-177">__İşleri__ sekmesi Hive sorguları geçmişini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ffd07-177">The __Jobs__ tab displays a history of Hive queries.</span></span>

![İş Geçmişi görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="ffd07-179">Veritabanı tabloları</span><span class="sxs-lookup"><span data-stu-id="ffd07-179">Database tables</span></span>

<span data-ttu-id="ffd07-180">Kullanabileceğiniz __tabloları__ tabloları Hive veritabanı içinde çalışmak üzere sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ffd07-180">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![Tablolar sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="ffd07-182">Kaydedilmiş sorguları</span><span class="sxs-lookup"><span data-stu-id="ffd07-182">Saved queries</span></span>

<span data-ttu-id="ffd07-183">Sorgu sekmesinden sorguları isteğe bağlı olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffd07-183">From the Query tab, you can optionally save queries.</span></span> <span data-ttu-id="ffd07-184">Kaydedildikten sonra sorgudan yeniden __kaydedilen sorguları__ sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ffd07-184">Once saved, you can reuse the query from the __Saved Queries__ tab.</span></span>

![Kaydedilen sorgular sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="ffd07-186">Kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="ffd07-186">User-defined functions</span></span>

<span data-ttu-id="ffd07-187">Hive, kullanıcı tanımlı işlevler (UDF) da genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="ffd07-188">Bir UDF işlev veya kolayca modellenir değil mantığı içinde HiveQL uygulamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ffd07-188">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="ffd07-189">Hive görünümü üstündeki UDF sekme bildirme ve bir dizi UDF'ler kaydetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ffd07-189">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs.</span></span> <span data-ttu-id="ffd07-190">Bu UDF'ler kullanılabilir **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="ffd07-190">These UDFs can be used with the **Query Editor**.</span></span>

![UDF sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="ffd07-192">Hive görünümü için bir UDF ekledikten sonra bir **Ekle UDF'ler** düğmesinin alt kısmındaki **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="ffd07-192">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="ffd07-193">Bu girişi seçerseniz Hive görünümünde tanımlanan UDF'ler açılan listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ffd07-193">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="ffd07-194">Bir UDF seçerek HiveQL ifadelerini UDF etkinleştirmek için sorgunuza ekler.</span><span class="sxs-lookup"><span data-stu-id="ffd07-194">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="ffd07-195">Örneğin, aşağıdaki özelliklere sahip bir UDF tanımlanmışsa:</span><span class="sxs-lookup"><span data-stu-id="ffd07-195">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="ffd07-196">Kaynak adı: myudfs</span><span class="sxs-lookup"><span data-stu-id="ffd07-196">Resource name: myudfs</span></span>

* <span data-ttu-id="ffd07-197">Kaynak yol: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="ffd07-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="ffd07-198">UDF ad: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="ffd07-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="ffd07-199">UDF sınıf adı: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="ffd07-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="ffd07-200">Kullanarak **Ekle UDF'ler** düğmesi görüntüler adlı bir girdi **myudfs**, başka bir açılan her UDF bu kaynak için tanımlanan için.</span><span class="sxs-lookup"><span data-stu-id="ffd07-200">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="ffd07-201">Bu durumda, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="ffd07-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="ffd07-202">Bu girdi seçerek aşağıdaki sorguyu başlangıcına ekler:</span><span class="sxs-lookup"><span data-stu-id="ffd07-202">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="ffd07-203">Ardından sorgunuza UDF kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffd07-203">You can then use the UDF in your query.</span></span> <span data-ttu-id="ffd07-204">Örneğin, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="ffd07-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="ffd07-205">UDF'ler hdınsight'ta Hive kullanma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="ffd07-205">For more information on using UDFs with Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ffd07-206">Hive veya Pig hdınsight'ta Python kullanarak</span><span class="sxs-lookup"><span data-stu-id="ffd07-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="ffd07-207">Hdınsight için özel bir Hive UDF ekleme</span><span class="sxs-lookup"><span data-stu-id="ffd07-207">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="ffd07-208">Hive ayarları</span><span class="sxs-lookup"><span data-stu-id="ffd07-208">Hive settings</span></span>

<span data-ttu-id="ffd07-209">Ayarlar, çeşitli Hive ayarlarını değiştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ffd07-209">Settings can be used to change various Hive settings.</span></span> <span data-ttu-id="ffd07-210">Örneğin, yürütme altyapısı Tez (varsayılan) kovana MapReduce değiştirme.</span><span class="sxs-lookup"><span data-stu-id="ffd07-210">For example, changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <span data-ttu-id="ffd07-211"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ffd07-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ffd07-212">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="ffd07-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="ffd07-213">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ffd07-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ffd07-214">Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ffd07-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ffd07-215">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="ffd07-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ffd07-216">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="ffd07-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
