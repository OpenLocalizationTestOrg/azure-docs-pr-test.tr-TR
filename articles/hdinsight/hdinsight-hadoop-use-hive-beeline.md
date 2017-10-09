---
title: "Apache Hive - Azure Hdınsight ile Beeline aaaUse | Microsoft Docs"
description: "Hdınsight'ta Hadoop ile nasıl toouse hello Beeline istemci toorun Hive sorguları hakkında bilgi edinin. Beeline JDBC HiveServer2 ile çalışmaya yönelik bir yardımcı programdır."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="0932a-105">Apache Hive ile Merhaba Beeline İstemcisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="0932a-106">Bilgi nasıl toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive Hdınsight'ta sorgular.</span><span class="sxs-lookup"><span data-stu-id="0932a-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="0932a-107">Beeline hello baş Hdınsight küme düğümlerinde bulunan bir Hive istemcidir.</span><span class="sxs-lookup"><span data-stu-id="0932a-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="0932a-108">Beeline JDBC tooconnect tooHiveServer2, Hdınsight kümenize üzerinde barındırılan bir hizmete kullanır.</span><span class="sxs-lookup"><span data-stu-id="0932a-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="0932a-109">Ayrıca Beeline tooaccess Hive Hdınsight'ta uzaktan üzerinde kullanabileceğiniz Internet hello.</span><span class="sxs-lookup"><span data-stu-id="0932a-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="0932a-110">Aşağıdaki tablonun hello Beeline ile kullanım için bağlantı dizelerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="0932a-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="0932a-111">Gelen Beeline çalıştırdığı</span><span class="sxs-lookup"><span data-stu-id="0932a-111">Where you run Beeline from</span></span> | <span data-ttu-id="0932a-112">Parametreler</span><span class="sxs-lookup"><span data-stu-id="0932a-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0932a-113">Bir SSH bağlantı tooa headnode veya kenar düğümü</span><span class="sxs-lookup"><span data-stu-id="0932a-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="0932a-114">Dış hello küme</span><span class="sxs-lookup"><span data-stu-id="0932a-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="0932a-115">Değiştir `admin` hello küme oturum açma hesabıyla kümeniz için.</span><span class="sxs-lookup"><span data-stu-id="0932a-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="0932a-116">Değiştir `password` hello küme oturum açma hesabının hello parolayla.</span><span class="sxs-lookup"><span data-stu-id="0932a-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="0932a-117">Değiştir `clustername` Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="0932a-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="0932a-118"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0932a-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="0932a-119">Linux tabanlı Hadoop Hdınsight kümesi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0932a-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0932a-120">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="0932a-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0932a-121">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0932a-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0932a-122">Bir SSH istemcisi veya yerel bir Beeline istemci.</span><span class="sxs-lookup"><span data-stu-id="0932a-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="0932a-123">Çoğu hello adımları bu belgede, bir SSH oturumu toohello kümeden Beeline kullandığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="0932a-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="0932a-124">Merhaba Beeline dış hello kümeden çalıştırma hakkında daha fazla bilgi için bkz [Beeline uzaktan kullanmak](#remote) bölümü.</span><span class="sxs-lookup"><span data-stu-id="0932a-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="0932a-125">SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0932a-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="0932a-126"><a id="beeline"></a>Beeline kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="0932a-127">Beeline başlatırken Hdınsight kümenize HiveServer2 için bir bağlantı dizesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0932a-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="0932a-128">toorun hello komutu dış hello kümeden hello küme oturum açma hesabı adı de sağlamanız gerekir (varsayılan `admin`) ve parola.</span><span class="sxs-lookup"><span data-stu-id="0932a-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="0932a-129">Biçim ve parametreleri Tablo toofind hello bağlantı dizesi toouse aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0932a-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="0932a-130">Gelen Beeline çalıştırdığı</span><span class="sxs-lookup"><span data-stu-id="0932a-130">Where you run Beeline from</span></span> | <span data-ttu-id="0932a-131">Parametreler</span><span class="sxs-lookup"><span data-stu-id="0932a-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="0932a-132">Bir SSH bağlantı tooa headnode veya kenar düğümü</span><span class="sxs-lookup"><span data-stu-id="0932a-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="0932a-133">Dış hello küme</span><span class="sxs-lookup"><span data-stu-id="0932a-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="0932a-134">Örneğin, komutu aşağıdaki hello kullanılan toostart Beeline bir SSH oturumu toohello kümeden olabilir:</span><span class="sxs-lookup"><span data-stu-id="0932a-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="0932a-135">Bu komut hello Beeline istemci başlar ve tooHiveServer2 hello küme baş düğümünde bağlanır.</span><span class="sxs-lookup"><span data-stu-id="0932a-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="0932a-136">Konumundaki gelmesini Hello komutu işlemi tamamlandıktan sonra bir `jdbc:hive2://headnodehost:10001/>` istemi.</span><span class="sxs-lookup"><span data-stu-id="0932a-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="0932a-137">Beeline komutları ile başlar bir `!` karakter, örneğin `!help` Yardım gösterir.</span><span class="sxs-lookup"><span data-stu-id="0932a-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="0932a-138">Ancak hello `!` bazı komutlar için atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0932a-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="0932a-139">Örneğin, `help` de çalışır.</span><span class="sxs-lookup"><span data-stu-id="0932a-139">For example, `help` also works.</span></span>

    <span data-ttu-id="0932a-140">Var olan bir `!sql`, hangi HiveQL ifadelerini kullanılan tooexecute değil.</span><span class="sxs-lookup"><span data-stu-id="0932a-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="0932a-141">Ancak, önceki hello atlayabilirsiniz kadar sık HiveQL kullanılır `!sql`.</span><span class="sxs-lookup"><span data-stu-id="0932a-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="0932a-142">Aşağıdaki iki deyimleri hello eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="0932a-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="0932a-143">Yeni kümede, yalnızca bir tablo listelenir: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="0932a-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="0932a-144">Komut toodisplay hello şema hello hivesampletable için aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0932a-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="0932a-145">Bu komut, aşağıdaki bilgilerle hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="0932a-145">This command returns hello following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="0932a-146">Bu bilgiler hello tablodaki hello sütun açıklar.</span><span class="sxs-lookup"><span data-stu-id="0932a-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="0932a-147">Biz bu verileri bazı sorgular gerçekleştirebilir olsa da, bunun yerine yeni bir tablo toodemonstrate nasıl oluşturalım Hive tooload veri ve şema uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0932a-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="0932a-148">Aşağıdaki deyimleri toocreate adlı bir tablo hello girin **log4jLogs** hello Hdınsight kümesi ile sağlanan örnek verileri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0932a-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="0932a-149">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0932a-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="0932a-150">`DROP TABLE`-Hello tablo zaten varsa, bu silinir.</span><span class="sxs-lookup"><span data-stu-id="0932a-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="0932a-151">`CREATE EXTERNAL TABLE`-Oluşturur bir **dış** Hive tablo.</span><span class="sxs-lookup"><span data-stu-id="0932a-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="0932a-152">Dış tablolara hello tablo tanımı kovanında yalnızca depolar.</span><span class="sxs-lookup"><span data-stu-id="0932a-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="0932a-153">Merhaba veri hello özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="0932a-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="0932a-154">`ROW FORMAT`-Nasıl hello veri biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="0932a-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="0932a-155">Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="0932a-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="0932a-156">`STORED AS TEXTFILE LOCATION`-Burada Hello veriler depolanır ve hangi dosya biçiminde.</span><span class="sxs-lookup"><span data-stu-id="0932a-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="0932a-157">`SELECT`-Tüm satırların sayımını seçer Burada sütun **t4** hello değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="0932a-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="0932a-158">Bu sorgunun döndürdüğü değeri **3** bu değeri içeren üç satır olarak.</span><span class="sxs-lookup"><span data-stu-id="0932a-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="0932a-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive tooapply hello şema tooall dosyaları hello dizininde çalışır.</span><span class="sxs-lookup"><span data-stu-id="0932a-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="0932a-160">Bu durumda, başlangıç dizini hello şema eşleşmiyor dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0932a-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="0932a-161">tooprevent çöp veriler hello sonuçlarında, bu bildirimi bildirir Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini. günlük.</span><span class="sxs-lookup"><span data-stu-id="0932a-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0932a-162">Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0932a-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="0932a-163">Örneğin, bir otomatik veri karşıya yükleme işlemi veya bir MapReduce işlemi.</span><span class="sxs-lookup"><span data-stu-id="0932a-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="0932a-164">Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="0932a-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="0932a-165">Merhaba, bu komutun metin benzer toohello aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="0932a-165">hello output of this command is similar toohello following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="0932a-166">tooexit Beeline, kullanmak `!exit`.</span><span class="sxs-lookup"><span data-stu-id="0932a-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="0932a-167"><a id="file"></a>Beeline toorun HiveQL dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="0932a-168">Adımları toocreate bir dosya çalıştırın Beeline kullanarak aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0932a-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="0932a-169">Kullanım hello şu komutu toocreate adlı bir dosya **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="0932a-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="0932a-170">Metin hello hello dosyasının içeriğini aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0932a-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="0932a-171">Bu sorgu adlı yeni bir 'iç' tablo oluşturur **günlüklerini**:</span><span class="sxs-lookup"><span data-stu-id="0932a-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="0932a-172">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0932a-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="0932a-173">**Tablo IF değil var oluşturmak** -hello tablo zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0932a-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="0932a-174">Merhaba itibaren **dış** anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0932a-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="0932a-175">İç tablolar hello Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="0932a-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="0932a-176">**AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="0932a-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="0932a-177">ORC biçimi Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="0932a-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="0932a-178">**INSERT ÜZERİNE... SEÇİN** -hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, eklemeleri veri hello hello sonra **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="0932a-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0932a-179">Dış tablolara, bir iç tablosu bırakarak hello temel alınan veri de siler.</span><span class="sxs-lookup"><span data-stu-id="0932a-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="0932a-180">toosave hello dosya, kullanım **Ctrl**+**_X**, enter **Y**ve son olarak **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0932a-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="0932a-181">Aşağıdaki Beeline kullanarak toorun hello dosyasına hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0932a-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="0932a-182">Merhaba `-i` parametresi Beeline başlatır ve çalıştırmalarını hello hello query.hql dosyasındaki ifadelerini.</span><span class="sxs-lookup"><span data-stu-id="0932a-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="0932a-183">Merhaba sorgu işlemi tamamlandıktan sonra hello gelmesini `jdbc:hive2://headnodehost:10001/>` istemi.</span><span class="sxs-lookup"><span data-stu-id="0932a-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="0932a-184">Hello kullanarak bir dosyaya da çalıştırabilirsiniz `-f` hello sorgu tamamlandıktan sonra Beeline çıkar parametresi.</span><span class="sxs-lookup"><span data-stu-id="0932a-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="0932a-185">Merhaba tooverify **günlüklerini** tablosu oluşturuldu, tüm satırları hello deyimi tooreturn aşağıdaki hello kullan **günlüklerini**:</span><span class="sxs-lookup"><span data-stu-id="0932a-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="0932a-186">Üç veri satırı döndürülmesi, tüm içeren **[Hata]** sütun t4 içinde:</span><span class="sxs-lookup"><span data-stu-id="0932a-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="0932a-187"><a id="remote"></a>Beeline uzaktan kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="0932a-188">Beeline yerel olarak yüklenmiş olması veya Docker resmin arkasını gibi kullanıyorsanız [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), şu parametreler hello kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0932a-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="0932a-189">__Bağlantı dizesi__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="0932a-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="0932a-190">__Küme oturum açma adı__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="0932a-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="0932a-191">__Küme oturum açma parolasını__`-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="0932a-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="0932a-192">Hello yerine `clustername` hello bağlantı dizesinde Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="0932a-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="0932a-193">Değiştir `admin` küme oturum açma ve değiştirme hello adıyla `password` , küme oturum açma için hello parolayla.</span><span class="sxs-lookup"><span data-stu-id="0932a-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="0932a-194"><a id="sparksql"></a>Spark ile Beeline kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="0932a-195">Spark refered tooas hello Spark Thrift sunucusunun görülür HiveServer2 kendi uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0932a-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="0932a-196">Bu hizmet, Hive yerine Spark SQL tooresolve sorgularını kullanır ve sorgunuzu bağlı olarak daha iyi performans sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0932a-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="0932a-197">Spark Hdınsight kümesinde, bağlantı noktası tooconnect toohello Spark Thrift sunucusunun `10002` yerine `10001`.</span><span class="sxs-lookup"><span data-stu-id="0932a-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="0932a-198">Örneğin, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="0932a-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0932a-199">değil erişilebilir üzerinden hello doğrudan internet hello Spark Thrift sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="0932a-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="0932a-200">Yalnızca bir SSH oturumunda tooit bağlanın veya içinde aynı Azure sanal ağ Hdınsight kümesi hello gibi hello.</span><span class="sxs-lookup"><span data-stu-id="0932a-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="0932a-201"><a id="summary"></a><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0932a-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="0932a-202">Hdınsight'ta Hive hakkında daha fazla genel bilgi için belge aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0932a-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="0932a-203">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="0932a-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0932a-204">Hdınsight'ta Hadoop ile çalışabilirsiniz diğer yollar hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0932a-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="0932a-205">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="0932a-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0932a-206">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="0932a-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="0932a-207">Tez Hive ile kullanıyorsanız, belgeleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0932a-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="0932a-208">Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="0932a-209">Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın</span><span class="sxs-lookup"><span data-stu-id="0932a-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
