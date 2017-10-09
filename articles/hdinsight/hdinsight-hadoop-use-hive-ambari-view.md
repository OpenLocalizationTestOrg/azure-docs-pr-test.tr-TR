---
title: "hdınsight'ta (Hadoop) - Azure Hive ile aaaUse Ambari görünümleri toowork | Microsoft Docs"
description: "Nasıl toouse hello Hive görünümü, web tarayıcısı toosubmit Hive sorgularının öğrenin. Merhaba Hive görünümü Ambari Web kullanıcı Arabirimi ile Linux tabanlı Hdınsight kümenizi sağlanan hello bir parçasıdır."
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
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="2c92f-104">Hdınsight'ta Hadoop ile Hive görünümü Hello kullanın</span><span class="sxs-lookup"><span data-stu-id="2c92f-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2c92f-105">Ambari Hive görünümünü kullanarak nasıl toorun Hive sorguları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2c92f-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="2c92f-106">Ambari, yönetim ve izleme yardımcı programı Linux tabanlı Hdınsight kümeleri ile sağlanan ' dir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2c92f-107">Ambari sağlanan hello özellikleri kullanılan toorun Hive sorguları olabilecek UI biridir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="2c92f-108">Ambari, bu belgede ele alınan değil birçok özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2c92f-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="2c92f-109">Daha fazla bilgi için bkz: [Hdınsight kümelerini yönetme hello Ambari Web kullanıcı arabirimini kullanarak](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="2c92f-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c92f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2c92f-110">Prerequisites</span></span>

* <span data-ttu-id="2c92f-111">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="2c92f-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2c92f-112">Küme oluşturma hakkında daha fazla bilgi için bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2c92f-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c92f-113">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2c92f-114">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2c92f-115">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2c92f-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="2c92f-116">Merhaba Hive görünümü Aç</span><span class="sxs-lookup"><span data-stu-id="2c92f-116">Open hello Hive view</span></span>

<span data-ttu-id="2c92f-117">Ambari görünümleri hello Azure portal ' olabilir; Hdınsight kümenize seçin ve ardından **Ambari görünümleri** hello gelen **hızlı bağlantılar** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2c92f-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![Merhaba portalı hızlı bağlantılar bölümü](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="2c92f-119">Merhaba görünümlerinin hello listesinden __Hive görünümü__.</span><span class="sxs-lookup"><span data-stu-id="2c92f-119">From hello list of views, select hello __Hive View__.</span></span>

![Merhaba seçilen Hive görünümü](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="2c92f-121">Ambari erişmek için istendiğinde tooauthenticate toohello site olur.</span><span class="sxs-lookup"><span data-stu-id="2c92f-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="2c92f-122">Hello Yöneticisi girin (varsayılan `admin`) hesap adı ve parola oluştururken kullandığınız küme hello.</span><span class="sxs-lookup"><span data-stu-id="2c92f-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="2c92f-123">Aşağıdaki görüntü bir sayfa benzer toohello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="2c92f-123">You should see a page similar toohello following image:</span></span>

![Merhaba Hive görünümü için hello sorgu çalışma sayfası görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="2c92f-125"><a name="hivequery"></a>Sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2c92f-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="2c92f-126">toorun bir hive sorgusu hello hello Hive görünümünü aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c92f-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="2c92f-127">Merhaba gelen __sorgu__ sekmesinde, HiveQL ifadelerini hello çalışma sayfasına aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="2c92f-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="2c92f-128">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2c92f-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="2c92f-129">`DROP TABLE`-Hello tablo ve hello veri dosyası siler hello tablo zaten mevcut durumda.</span><span class="sxs-lookup"><span data-stu-id="2c92f-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="2c92f-130">`CREATE EXTERNAL TABLE`-Kovanında yeni bir "dış" tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c92f-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="2c92f-131">Dış tablolara yalnızca hello tablo tanımı kovanında depolar.</span><span class="sxs-lookup"><span data-stu-id="2c92f-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="2c92f-132">Merhaba veri hello özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="2c92f-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="2c92f-133">`ROW FORMAT`-Nasıl hello veri biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="2c92f-134">Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="2c92f-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="2c92f-135">`STORED AS TEXTFILE LOCATION`-Hello verilerin depolandığı ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="2c92f-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="2c92f-136">`SELECT`-Hello değer [Hata], sütun t4 içerdiği tüm satırların sayımını seçer.</span><span class="sxs-lookup"><span data-stu-id="2c92f-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="2c92f-137">Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2c92f-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="2c92f-138">Örneğin, bir otomatik veri karşıya yükleme işlem, veya başka bir MapReduce işlemi tarafından.</span><span class="sxs-lookup"><span data-stu-id="2c92f-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="2c92f-139">Bir dış tablo bırakma mu *değil* hello verileri, yalnızca hello tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="2c92f-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2c92f-140">Merhaba bırakın __veritabanı__ seçimi daha __varsayılan__.</span><span class="sxs-lookup"><span data-stu-id="2c92f-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="2c92f-141">Bu belgedeki örneklerde Hello Hdınsight ile dahil hello varsayılan veritabanı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c92f-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="2c92f-142">toostart hello sorgu, kullanım hello **yürütme** hello çalışma aşağıdaki düğmesine.</span><span class="sxs-lookup"><span data-stu-id="2c92f-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="2c92f-143">Turuncu ve hello metin değişiklikleri çok renge**durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="2c92f-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="2c92f-144">Merhaba sorgu tamamladığında hello **sonuçları** sekmesi hello işlemi hello sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2c92f-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="2c92f-145">metin aşağıdaki hello hello hello sorgu sonucudur:</span><span class="sxs-lookup"><span data-stu-id="2c92f-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="2c92f-146">Merhaba **günlükleri** sekmesini hello işlem tarafından oluşturulan kullanılan tooview hello günlük bilgileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="2c92f-147">Merhaba **sonuçları kaydetmek** açılan iletişim kutusunda hello üst sol Merhaba **sorgu işleminin sonuçları** bölüm sonuçları kaydetmek veya toodownload sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c92f-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="2c92f-148">Select hello ilk dört satırı bu sorgu ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="2c92f-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="2c92f-149">Merhaba işi tamamlandığında sonuç olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c92f-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="2c92f-150">Hello kullanarak **yürütme** düğmesinin hello sorgu parçası olduğunda çalışır seçili deyimleri hello yalnızca seçili.</span><span class="sxs-lookup"><span data-stu-id="2c92f-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="2c92f-151">Bu durumda, hello seçimi hello tablosundan satır alır hello son deyimini eklemediniz.</span><span class="sxs-lookup"><span data-stu-id="2c92f-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="2c92f-152">Yalnızca bu satırı seçin ve kullanırsanız **yürütme**, beklenen hello sonuçları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="2c92f-153">tooadd bir çalışma kullanmak hello **yeni çalışma sayfası** düğmesi hello hello sonundaki **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="2c92f-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="2c92f-154">Merhaba yeni çalışma sayfasında, aşağıdaki HiveQL ifadelerini hello girin:</span><span class="sxs-lookup"><span data-stu-id="2c92f-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="2c92f-155">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2c92f-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="2c92f-156">**Tablo IF değil var oluşturmak** -zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c92f-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="2c92f-157">Merhaba itibaren **dış** anahtar sözcüğü kullanılmaz, bir iç tablosu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2c92f-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="2c92f-158">Bir iç tablosu hello Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="2c92f-159">Dış tablolara, bir iç tablosu bırakarak hello temel alınan veri de siler.</span><span class="sxs-lookup"><span data-stu-id="2c92f-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="2c92f-160">**AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="2c92f-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="2c92f-161">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="2c92f-162">**INSERT ÜZERİNE... SEÇİN** -hello satırları seçer **log4jLogs** içeren tablo `[ERROR]`, ve ardından ekler veri hello hello **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="2c92f-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="2c92f-163">Kullanım hello **yürütme** toorun bu sorguyu düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c92f-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="2c92f-164">Merhaba **sonuçları** sekmesini hello sorgu sıfır satır geri döndüğünde herhangi bir bilgi içermiyor.</span><span class="sxs-lookup"><span data-stu-id="2c92f-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="2c92f-165">Hello durumunu göster olarak **başarılı** hello sorgu işlemi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="2c92f-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="2c92f-166">Visual açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="2c92f-166">Visual explain</span></span>

<span data-ttu-id="2c92f-167">toodisplay hello sorgu planı, select hello görselleştirmesini **Visual açıklayan** sekmenin hello çalışma altında.</span><span class="sxs-lookup"><span data-stu-id="2c92f-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="2c92f-168">Merhaba **Visual açıklayan** hello sorgu görünümünü karmaşık sorgular hello akışını anlamak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="2c92f-169">Bu görünüm metinsel denk hello kullanarak görüntüleyebileceğiniz **açıklama** hello sorgu Düzenleyicisi'ni düğmesini.</span><span class="sxs-lookup"><span data-stu-id="2c92f-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="2c92f-170">Tez kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="2c92f-170">Tez UI</span></span>

<span data-ttu-id="2c92f-171">toodisplay hello Tez UI hello sorgu select hello **Tez** sekmenin hello çalışma altında.</span><span class="sxs-lookup"><span data-stu-id="2c92f-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c92f-172">Tez kullanılmaz tooresolve tüm sorgudur.</span><span class="sxs-lookup"><span data-stu-id="2c92f-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="2c92f-173">Çok sayıda sorgu, Tez kullanmadan çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="2c92f-174">Tez kullanılan tooresolve hello sorgu olduysa, hello yönlendirilmiş Çevrimsiz grafik (DAG) görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="2c92f-175">Tez işlem olduğunuz çalıştırdı hello geçmiş ya da hata ayıklama sorguları hello için tooview hello DAG istiyorsanız, hello kullanın [Tez Görünüm](hdinsight-debug-ambari-tez-view.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="2c92f-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="2c92f-176">İş geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2c92f-176">View job history</span></span>

<span data-ttu-id="2c92f-177">Merhaba __işleri__ sekmesi Hive sorguları geçmişini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2c92f-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Merhaba iş geçmişi görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="2c92f-179">Veritabanı tabloları</span><span class="sxs-lookup"><span data-stu-id="2c92f-179">Database tables</span></span>

<span data-ttu-id="2c92f-180">Merhaba kullanabilirsiniz __tabloları__ toowork Hive veritabanındaki tablolarla sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="2c92f-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Merhaba tablolar sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="2c92f-182">Kaydedilmiş sorguları</span><span class="sxs-lookup"><span data-stu-id="2c92f-182">Saved queries</span></span>

<span data-ttu-id="2c92f-183">Merhaba sorgu sekmesinden sorguları isteğe bağlı olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c92f-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="2c92f-184">Kaydedildikten sonra hello hello sorgudan yeniden __kaydedilen sorguları__ sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2c92f-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Kaydedilen sorgular sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="2c92f-186">Kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="2c92f-186">User-defined functions</span></span>

<span data-ttu-id="2c92f-187">Hive, kullanıcı tanımlı işlevler (UDF) da genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="2c92f-188">Bir UDF tooimplement işlev veya HiveQL içinde kolayca modellenir değil mantığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c92f-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="2c92f-189">Merhaba UDF sekmesini hello Hive görünümü hello üstündeki toodeclare sağlar ve UDF'ler kümesi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2c92f-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="2c92f-190">Bu UDF'ler ile Merhaba kullanılabilir **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="2c92f-190">These UDFs can be used with hello **Query Editor**.</span></span>

![UDF sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="2c92f-192">UDF toohello Hive görünümü ekledikten sonra bir **Ekle UDF'ler** düğmesi görünür hello hello altındaki **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="2c92f-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="2c92f-193">Bu girdi seçerek hello hello Hive görünümü tanımlı UDF'ler açılan listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2c92f-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="2c92f-194">Bir UDF seçerek HiveQL ifadelerini tooyour sorgu tooenable hello UDF ekler.</span><span class="sxs-lookup"><span data-stu-id="2c92f-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="2c92f-195">Örneğin, aşağıdaki özelliklere hello ile bir UDF tanımladıysanız:</span><span class="sxs-lookup"><span data-stu-id="2c92f-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="2c92f-196">Kaynak adı: myudfs</span><span class="sxs-lookup"><span data-stu-id="2c92f-196">Resource name: myudfs</span></span>

* <span data-ttu-id="2c92f-197">Kaynak yol: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="2c92f-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="2c92f-198">UDF ad: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="2c92f-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="2c92f-199">UDF sınıf adı: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="2c92f-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="2c92f-200">Hello kullanarak **Ekle UDF'ler** düğmesi görüntüler adlı bir girdi **myudfs**, başka bir açılan her UDF bu kaynak için tanımlanan için.</span><span class="sxs-lookup"><span data-stu-id="2c92f-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="2c92f-201">Bu durumda, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="2c92f-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="2c92f-202">Bu girdi seçerek hello sorgu toohello başlangıcını izleyen hello ekler:</span><span class="sxs-lookup"><span data-stu-id="2c92f-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="2c92f-203">Daha sonra sorgunuzu hello UDF kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c92f-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="2c92f-204">Örneğin, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="2c92f-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="2c92f-205">UDF'ler hdınsight'ta Hive kullanma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2c92f-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="2c92f-206">Hive veya Pig hdınsight'ta Python kullanarak</span><span class="sxs-lookup"><span data-stu-id="2c92f-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="2c92f-207">Nasıl tooadd özel bir Hive UDF tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="2c92f-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="2c92f-208">Hive ayarları</span><span class="sxs-lookup"><span data-stu-id="2c92f-208">Hive settings</span></span>

<span data-ttu-id="2c92f-209">Ayarları can kullanılan toochange çeşitli Hive ayarları olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c92f-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="2c92f-210">Örneğin, hello yürütme alt yapısı için Hive Tez (Merhaba varsayılan) tooMapReduce değiştirme.</span><span class="sxs-lookup"><span data-stu-id="2c92f-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="2c92f-211"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c92f-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2c92f-212">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="2c92f-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="2c92f-213">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="2c92f-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2c92f-214">Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c92f-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2c92f-215">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="2c92f-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2c92f-216">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="2c92f-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
