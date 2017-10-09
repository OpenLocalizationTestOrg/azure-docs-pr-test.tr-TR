---
title: "Linux tabanlı Hdınsight Hadoop Oozie akışlarında aaaUse | Microsoft Docs"
description: "Linux tabanlı Hdınsight'ta Hadoop Oozie kullanın. Bilgi nasıl toodefine bir Oozie iş akışı ve Oozie işi gönderin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="b4bf9-104">Oozie Hadoop toodefine ile kullanın ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b4bf9-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="b4bf9-105">Bilgi nasıl toouse hdınsight'ta Hadoop ile Apache Oozie.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="b4bf9-106">Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="b4bf9-107">Oozie hello Hadoop yığını ile tümleştirilir ve işleri aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="b4bf9-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="b4bf9-108">Apache MapReduce</span></span>
* <span data-ttu-id="b4bf9-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="b4bf9-109">Apache Pig</span></span>
* <span data-ttu-id="b4bf9-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="b4bf9-110">Apache Hive</span></span>
* <span data-ttu-id="b4bf9-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="b4bf9-111">Apache Sqoop</span></span>

<span data-ttu-id="b4bf9-112">Oozie de Java programları veya kabuk betikleri gibi belirli tooa sistem kullanılan tooschedule işler olabilir</span><span class="sxs-lookup"><span data-stu-id="b4bf9-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="b4bf9-113">Hdınsight iş akışlarıyla tanımlamak için başka bir Azure Data Factory seçenektir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="b4bf9-114">Azure Data Factory hakkında daha fazla toolearn bkz [kullanım Pig ve Hive Data Factory ile][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="b4bf9-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4bf9-115">Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4bf9-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b4bf9-116">Prerequisites</span></span>

* <span data-ttu-id="b4bf9-117">**Hdınsight kümesi**: bkz [Linux'ta Hdınsight ile çalışmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b4bf9-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b4bf9-118">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="b4bf9-119">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b4bf9-120">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b4bf9-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="b4bf9-121">Örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="b4bf9-121">Example workflow</span></span>

<span data-ttu-id="b4bf9-122">Bu belgede kullanılan hello iş akışı iki eylemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="b4bf9-123">Hive, Sqoop, MapReduce veya başka bir işlemin çalıştırma gibi görevler için tanımları eylemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![İş akışı diyagramı][img-workflow-diagram]

1. <span data-ttu-id="b4bf9-125">Bir Hive eylem HiveQL betiğini tooextract kayıtları hello çalıştırır **hivesampletable** Hdınsight ile dahil.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="b4bf9-126">Her veri satırının belirli bir mobil CİHAZDAN ziyaret açıklar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="b4bf9-127">Merhaba kayıt biçimi metin aşağıdaki benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="b4bf9-128">Bu belgede kullanılan Hive betiğini Hello hello toplam ziyaretleriniz (örneğin, Android veya iPhone) her platform için sayar ve hello sayıları tooa yeni Hive tablosu depolar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="b4bf9-129">Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="b4bf9-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="b4bf9-130">Sqoop eylemin hello yeni Hive tablosu tooa tabloda bir Azure SQL veritabanı Merhaba içeriğine dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="b4bf9-131">Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hadoop Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="b4bf9-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="b4bf9-132">Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [hello Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="b4bf9-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="b4bf9-133">Merhaba çalışma dizini oluşturulamadı</span><span class="sxs-lookup"><span data-stu-id="b4bf9-133">Create hello working directory</span></span>

<span data-ttu-id="b4bf9-134">Oozie iş toobe hello aynı depolanan için gereken kaynakları bekliyor dizin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="b4bf9-135">Bu örnekte **wasb: / / / öğreticileri/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="b4bf9-136">Komut toocreate aşağıdaki hello bu dizini ve bu iş akışı tarafından oluşturulan hello yeni Hive tablosu tutan hello veri dizini kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="b4bf9-137">Merhaba `-p` parametresi hello yolu toobe oluşturulan tüm dizinleri neden olur.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="b4bf9-138">Merhaba **veri** dizindir hello tarafından kullanılan kullanılan toohold verileri **useooziewf.hql** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="b4bf9-139">Ayrıca Oozie, kullanıcı hesabınızın Hive ve Sqoop işleri çalıştırırken bürünebileceğini sağlar komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="b4bf9-140">Değiştir **kullanıcıadı** oturum açma adınız ile:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="b4bf9-141">Hataları yoksayma hello kullanıcı zaten hello üyesi olan `users` grubu.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="b4bf9-142">Bir veritabanı sürücüsü Ekle</span><span class="sxs-lookup"><span data-stu-id="b4bf9-142">Add a database driver</span></span>

<span data-ttu-id="b4bf9-143">Bu iş akışı Sqoop tooexport veri tooSQL veritabanı kullandığından, tootalk tooSQL veritabanının bir kopyasını hello JDBC sürücüsü kullanılan sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="b4bf9-144">Kullanım hello komut toocopy, toohello çalışma dizini:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="b4bf9-145">İş akışınızı bir MapReduce uygulaması içeren jar gibi diğer kaynaklar kullandıysanız, bu kaynakları da tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="b4bf9-146">Merhaba Hive sorgusunu tanımlama</span><span class="sxs-lookup"><span data-stu-id="b4bf9-146">Define hello Hive query</span></span>

<span data-ttu-id="b4bf9-147">Aşağıdaki adımları toocreate bir Oozie iş akışında bu belgenin sonraki bölümlerinde kullanılan bir sorguyu tanımlayan bir HiveQL betiğini hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="b4bf9-148">SSH kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="b4bf9-149">Merhaba aşağıdaki komutu hello kullanarak bir örnektir `ssh` komutu.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="b4bf9-150">Değiştir __kullanıcıadı__ hello SSH kullanıcıyla hello küme.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="b4bf9-151">Değiştir __CLUSTERNAME__ hello Hdınsight kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="b4bf9-152">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b4bf9-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b4bf9-153">SSH bağlantısı Hello komutu toocreate bir dosya aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="b4bf9-154">Merhaba nano düzenleyici açılır olduktan sonra sorgu hello dosyasının Merhaba içeriğine aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="b4bf9-155">Merhaba komut dosyasında kullanılan iki değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="b4bf9-156">**${hiveTableName}**: hello tablo toobe oluşturulan hello adını içerir</span><span class="sxs-lookup"><span data-stu-id="b4bf9-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="b4bf9-157">**${hiveDataFolder}**: hello tablo için hello konumu toostore hello veri dosyalarını içerir</span><span class="sxs-lookup"><span data-stu-id="b4bf9-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="b4bf9-158">Merhaba iş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu değerleri toothis HiveQL betiğini çalışma zamanında geçirir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="b4bf9-159">tooexit hello Düzenleyici, Ctrl-X tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="b4bf9-160">İstendiğinde, seçin **Y** toosave hello dosyasını yeniden kullanın **Enter** toouse hello **useooziewf.hql** dosya adı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="b4bf9-161">Kullanım hello aşağıdaki komutları toocopy **useooziewf.hql** çok**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="b4bf9-162">Bu komutlar hello depolamak **useooziewf.hql** hello küme için hello HDFS uyumlu depolama dosyası.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="b4bf9-163">Merhaba iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="b4bf9-163">Define hello workflow</span></span>

<span data-ttu-id="b4bf9-164">Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="b4bf9-165">Aşağıdaki adımları toodefine hello iş akışı hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="b4bf9-166">Deyimi toocreate aşağıdaki hello kullanın ve yeni dosyasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="b4bf9-167">Bir kez hello nano Düzenleyici açıldığında, XML hello dosya içeriğini aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="b4bf9-168">Merhaba iş akışında tanımlanan iki eylem vardır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="b4bf9-169">**RunHiveScript**: Bu eylem hello başlangıç eylemdir ve çalışan hello **useooziewf.hql** Hive betiği</span><span class="sxs-lookup"><span data-stu-id="b4bf9-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="b4bf9-170">**RunSqoopExport**: Bu eylem hello Hive betiği tooSQL oluşturulmuş hello veri aktarır Sqoop kullanarak veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="b4bf9-171">Bu eylem yalnızca hello çalıştırır **RunHiveScript** eylem başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="b4bf9-172">Merhaba iş akışı sahip birden çok girişi gibi `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="b4bf9-173">Bu girişler hello iş tanımında kullandığınız değerler değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="b4bf9-174">Merhaba iş tanımı, bu belgenin sonraki bölümlerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="b4bf9-175">Ayrıca Not hello `<archive>sqljdbc4.jar</arcive>` hello Sqoop bölüm girişi.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="b4bf9-176">Bu eylem çalıştırıldığında bu girişi Oozie toomake Sqoop için kullanılabilir bu arşiv bildirir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="b4bf9-177">CTRL-X, daha sonra kullanmak **Y** ve **Enter** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="b4bf9-178">Kullanım hello şu komutu toocopy hello **workflow.xml** çok dosya**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="b4bf9-179">Merhaba veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4bf9-179">Create hello database</span></span>

<span data-ttu-id="b4bf9-180">toocreate bir Azure SQL veritabanı izleyin hello hello adımlarda [bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="b4bf9-181">Merhaba veritabanı oluştururken `oozietest` hello veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="b4bf9-182">Ayrıca hello hello veritabanı sunucusunun adını not edin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="b4bf9-183">Merhaba tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4bf9-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="b4bf9-184">Birçok yolu tooconnect tooSQL veritabanı toocreate bir tablo yok.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="b4bf9-185">Aşağıdaki adımları kullan hello [ücretsiz](http://www.freetds.org/) hello Hdınsight kümesine ait.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="b4bf9-186">Komut tooinstall ücretsiz hello Hdınsight kümesinde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="b4bf9-187">Ücretsiz yüklendikten sonra daha önce oluşturulan komutu tooconnect toohello SQL veritabanı sunucusu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="b4bf9-188">Metin aşağıdaki çıktı benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="b4bf9-189">Merhaba, `1>` isteminde, aşağıdaki satırları hello girin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="b4bf9-190">Ne zaman hello `GO` deyimi girilir, hello önceki deyimleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="b4bf9-191">Bu ifadeler adlı bir tablo oluşturmak **mobiledata** hello iş akışı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="b4bf9-192">Tablo hello tooverify aşağıdaki kullanım hello oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="b4bf9-193">Metin aşağıdaki çıktı benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="b4bf9-194">Girin `exit` hello adresindeki `1>` sor tooexit hello tsql yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="b4bf9-195">Merhaba iş tanımı oluştur</span><span class="sxs-lookup"><span data-stu-id="b4bf9-195">Create hello job definition</span></span>

<span data-ttu-id="b4bf9-196">Merhaba iş tanımı burada toofind hello workflow.xml açıklar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="b4bf9-197">Ayrıca nerede tanımlar toofind (örneğin, useooziewf.hql.) hello iş akışı tarafından kullanılan diğer dosyaları Özellikler hello iş akışı içinde kullanılan ve dosyalar ilişkili ayrıca hello değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="b4bf9-198">Kullanım hello aşağıdaki tooget hello tam adresini hello varsayılan depolama komutu.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="b4bf9-199">Bu adres hello yapılandırma dosyasında birazdan kullanılır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="b4bf9-200">Bu komut, XML aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="b4bf9-201">Merhaba Hdınsight küme hello varsayılan depolama alanı olarak Azure Storage kullanıyorsa, hello `<value>` öğenin içeriği ile başlar `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="b4bf9-202">Azure Data Lake Store yerine kullanılırsa, ile başlayan `adl://`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="b4bf9-203">Merhaba Hello içeriğini kaydetme `<value>` şekliyle öğe hello sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="b4bf9-204">Komut tooget hello küme headnode FQDN'si aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="b4bf9-205">Bu bilgiler hello hello küme için Jobtracker'a adresi için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="b4bf9-206">Bu metin aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="b4bf9-207">Merhaba tam adresi toouse hello Jobtracker'a için olacak şekilde hello Jobtracker'a hello için kullanılan bağlantı noktası 8050, olan `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="b4bf9-208">Toocreate hello Oozie iş tanımı yapılandırması aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="b4bf9-209">Merhaba nano düzenleyici açılır sonra XML hello hello dosyasının içeriğini aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="b4bf9-210">Tüm örneklerinin yerine  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  aldığınız önceki sürümleri için varsayılan depolama hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="b4bf9-211">Merhaba yol ise bir `wasb` yolu hello tam yolunu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="b4bf9-212">Toojust kısaltın değil `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="b4bf9-213">Değiştir **JOBTRACKERADDRESS** hello daha önce aldığınız Jobtracker'a/ResourceManager adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="b4bf9-214">Değiştir **adınız** hello Hdınsight kümesi için oturum açma adınızı ile.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="b4bf9-215">Değiştir **serverName**, **adminLogin**, ve **Admınpassword** Azure SQL veritabanınıza ilişkin hello bilgiler.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="b4bf9-216">Bu dosyadaki hello bilgilerin çoğunu olduğu (örneğin, ${iş}.) hello workflow.xml veya ooziewf.hql dosyalarında kullanılan kullanılan toopopulate hello değerleri</span><span class="sxs-lookup"><span data-stu-id="b4bf9-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="b4bf9-217">Hello **oozie.wf.application.path** girdi tanımlar where hello iş akışı içeren toofind hello workflow.xml dosyasını bu iş tarafından çalıştı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="b4bf9-218">CTRL-X, daha sonra kullanmak **Y** ve **Enter** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="b4bf9-219">Gönderme ve hello işi yönetme</span><span class="sxs-lookup"><span data-stu-id="b4bf9-219">Submit and manage hello job</span></span>

<span data-ttu-id="b4bf9-220">Merhaba aşağıdaki adımları hello Oozie komutu toosubmit kullanın ve Oozie iş akışları hello kümede yönetin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="b4bf9-221">Merhaba Oozie komutu olan kullanıcı dostu bir arabirim hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="b4bf9-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4bf9-222">Merhaba Oozie komutunu kullanırken, hello Hdınsight headnode hello FQDN kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="b4bf9-223">Bu FQDN yalnızca hello kümeden erişilebilir olduğunu veya hello küme hello üzerindeki diğer makinelerden bir Azure sanal ağda ise aynı ağ.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="b4bf9-224">Tooobtain hello URL toohello Oozie hizmeti aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="b4bf9-225">Bu bilgi benzer toohello XML aşağıdaki döndürür:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="b4bf9-226">Merhaba `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` hello URL toouse hello Oozie komutu sahip bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="b4bf9-227">Tootype aktarıp toocreate bir ortam değişkeni hello URL'sini aşağıdaki kullanım hello her komut için:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="b4bf9-228">Merhaba URL hello biri daha önce aldığınız değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="b4bf9-229">Toosubmit hello işi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="b4bf9-230">Bu komut hello iş bilgilerini yükler **job.xml** ve tooOozie, ancak bunu çalışmıyor mu gönderir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="b4bf9-231">Merhaba komutu tamamlandığında hello işin hello kimliği döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="b4bf9-232">Örneğin, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="b4bf9-233">Kullanılan toomanage hello iş kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="b4bf9-234">Komutu aşağıdaki hello kullanarak hello işi Hello durumunu görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="b4bf9-235">Değiştir `<JOBID>` ile Merhaba hello önceki adımda döndürülen kimliği.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="b4bf9-236">Bu metin aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-236">This returns information similar toohello following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="b4bf9-237">Bu iş durumuna sahip `PREP`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="b4bf9-238">Bu durum, bu hello iş oluşturuldu, ancak henüz başlatılmamış gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="b4bf9-239">Komut toostart hello işi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="b4bf9-240">Değiştir `<JOBID>` hello ile döndürülen kimliği daha önce.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="b4bf9-241">Bu komutun ardından hello durumunu denetlemek, çalışır durumda olduğundan ve bilgi hello işindeki hello eylemler için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="b4bf9-242">Merhaba görev başarıyla tamamlandıktan sonra hello veri oluşturuldu ve toohello SQL veritabanı tablosu hello aşağıdaki komutları kullanarak dışa aktarılan doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="b4bf9-243">Merhaba, `1>` isteminde, sorgu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="b4bf9-244">döndürülen hello bilgi metnini izleyen benzer toohello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="b4bf9-245">Merhaba Oozie komut hakkında daha fazla bilgi için bkz: [Oozie komut satırı aracı](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="b4bf9-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="b4bf9-246">Oozie REST API'si</span><span class="sxs-lookup"><span data-stu-id="b4bf9-246">Oozie REST API</span></span>

<span data-ttu-id="b4bf9-247">Merhaba Oozie REST API toobuild verir Oozie ile iş kendi araçları.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="b4bf9-248">Merhaba, Hdınsight hello Oozie REST API kullanımı hakkında belirli bilgiler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="b4bf9-249">**URI**: REST API erişilebilir dış hello kümeden hello`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="b4bf9-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="b4bf9-250">**Kimlik doğrulama**: toohello API hello küme HTTP hesabı (Yönetici) ve parola kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="b4bf9-251">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="b4bf9-252">Merhaba Oozie REST API kullanma hakkında daha fazla bilgi için bkz: [Oozie Web Hizmetleri API'si](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="b4bf9-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="b4bf9-253">Oozie Web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="b4bf9-253">Oozie Web UI</span></span>

<span data-ttu-id="b4bf9-254">Merhaba Oozie Web kullanıcı arabirimini hello Oozie işlerin durumunu web tabanlı bir görünüme hello kümede sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="b4bf9-255">Merhaba web kullanıcı Arabirimi aşağıdaki bilgilerle tooview hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="b4bf9-256">İş durumu</span><span class="sxs-lookup"><span data-stu-id="b4bf9-256">Job status</span></span>
* <span data-ttu-id="b4bf9-257">İş tanımı</span><span class="sxs-lookup"><span data-stu-id="b4bf9-257">Job definition</span></span>
* <span data-ttu-id="b4bf9-258">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b4bf9-258">Configuration</span></span>
* <span data-ttu-id="b4bf9-259">Merhaba işteki hello eylemlerin bir grafik</span><span class="sxs-lookup"><span data-stu-id="b4bf9-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="b4bf9-260">Merhaba işi için kayıtlar</span><span class="sxs-lookup"><span data-stu-id="b4bf9-260">Logs for hello job</span></span>

<span data-ttu-id="b4bf9-261">Ayrıca bir işi içinde eylemler ayrıntılarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="b4bf9-262">tooaccess Oozie Web kullanıcı arabirimini Merhaba, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="b4bf9-263">SSH tüneli toohello Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="b4bf9-264">Bilgi için bkz: Merhaba [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="b4bf9-265">Bir tünel oluşturulduktan sonra hello Ambari web kullanıcı Arabirimi, web tarayıcınızda açın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="b4bf9-266">Merhaba URI hello Ambari site için olan **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="b4bf9-267">Değiştir **CLUSTERNAME** Linux tabanlı Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="b4bf9-268">Yan hello sayfasının sol hello seçin **Oozie**, ardından **hızlı bağlantılar**ve son olarak **Oozie Web kullanıcı arabirimini**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![Merhaba menü görüntüsü](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="b4bf9-270">Merhaba Oozie Web kullanıcı arabirimini Varsayılanları toodisplaying iş akışı işleri çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="b4bf9-271">tüm iş akışı işleri toosee seçin **tüm işleri**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Görüntülenen tüm işleri](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="b4bf9-273">Bir iş tooview hello işi hakkında daha fazla bilgi seçin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-273">Select a job tooview more information about hello job.</span></span>

    ![İş bilgileri](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="b4bf9-275">Merhaba iş bilgileri sekmesinden temel iş bilgilerini ve hello ayrı Eylemler hello işindeki görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="b4bf9-276">Merhaba sekmelerini kullanarak görüntüleyebileceğiniz hello üstünde iş tanımı, iş yapılandırması, erişim hello iş günlüğü hello veya yönlendirilmiş Çevrimsiz grafik (DAG) hello işin görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="b4bf9-277">**İş günlüğü**: Select hello **GetLogs** tooget hello işi için tüm günlükleri düğmesine veya hello kullan **girin arama filtresi** alan toofilter günlükleri</span><span class="sxs-lookup"><span data-stu-id="b4bf9-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![İş günlüğü](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="b4bf9-279">**JobDAG**: Merhaba DAG olan hello akışı gerçekleştirilecek hello veri yolları grafik bir genel bakış</span><span class="sxs-lookup"><span data-stu-id="b4bf9-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![İş DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="b4bf9-281">Hello hello eylemlerden birini seçerek **iş bilgileri** sekmesini hello eylemi için bilgileri getirir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="b4bf9-282">Örneğin, hello seçin **RunHiveScript** eylem.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="b4bf9-284">Bir bağlantı toohello gibi hello eylem ayrıntılarını görebilirsiniz **Konsolu URL'si**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="b4bf9-285">Bu bağlantıyı hello işi için kullanılan tooview Jobtracker'a bilgileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="b4bf9-286">İşlerini zamanlama</span><span class="sxs-lookup"><span data-stu-id="b4bf9-286">Scheduling jobs</span></span>

<span data-ttu-id="b4bf9-287">Merhaba Düzenleyicisi toospecify işleri için bir başlangıç, bitiş ve geçişi sıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="b4bf9-288">Merhaba iş akışı, aşağıdaki adımları kullanın hello için bir zamanlama toodefine:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="b4bf9-289">Toocreate adlı bir dosya aşağıdaki kullanım hello **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="b4bf9-290">XML hello hello dosyasının içeriğini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-290">Use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="b4bf9-291">Merhaba `${...}` değişkenleri, çalışma zamanında hello iş tanımında değerlere göre değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="b4bf9-292">Merhaba değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="b4bf9-293">`${coordFrequency}`: Çalışan hello iş örneklerini arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="b4bf9-294">** `${coordStart}`: hello iş başlangıç zamanı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="b4bf9-295">`${coordEnd}`: hello iş bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="b4bf9-296">`${coordTimezone}`: Sabit bir saat diliminde (genellikle UTC ile gösterilir) hiçbir gün ışığından yararlanma saatine sahip olan düzenleyici işleri.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="b4bf9-297">Bu saat dilimi hello "Oozie işleme saat dilimi." olarak adlandırılır</span><span class="sxs-lookup"><span data-stu-id="b4bf9-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="b4bf9-298">`${wfPath}`: yolu toohello workflow.xml hello.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="b4bf9-299">toosave hello dosya, Ctrl-X, kullanmak **Y**, ve **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="b4bf9-300">Bu iş için komut toocopy hello dosya toohello çalışma dizini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="b4bf9-301">Kullanım hello toomodify hello aşağıdaki **job.xml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="b4bf9-302">Aşağıdaki değişiklikler hello olun:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-302">Make hello following changes:</span></span>

   * <span data-ttu-id="b4bf9-303">Merhaba iş akışı, değişiklik yerine tooinstruct oozie toorun hello Düzenleyici dosyasında `<name>oozie.wf.application.path</name>` çok`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="b4bf9-304">tooset hello `workflowPath` hello Düzenleyicisi tarafından kullanılan değişken XML aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="b4bf9-305">Hello yerine `wasb://mycontainer@mystorageaccount.blob.core.windows` diğer giriş hello job.xml dosyası kullanılan hello değeri olan metin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="b4bf9-306">toodefine hello başlangıç, bitiş ve sıklığı hello Düzenleyicisi için XML aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="b4bf9-307">Merhaba başlangıç saati too12 bu değerleri ayarlayın: 00 PM 10 May 2017 üzerinde hello bitiş saati tooMay 12, 2017.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="b4bf9-308">Bu işi her gün için başlangıç aralığı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-308">hello interval for running this job daily.</span></span> <span data-ttu-id="b4bf9-309">Merhaba sıklığıdır dakika içinde bu nedenle 1440 dakika 24 saat x 60 dakika =.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="b4bf9-310">Son olarak, hello saat dilimi tooUTC ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="b4bf9-311">CTRL-X, daha sonra kullanmak **Y** ve **Enter** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="b4bf9-312">toorun hello iş, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="b4bf9-313">Bu komut gönderir ve hello işini başlatır.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="b4bf9-314">Merhaba Oozie Web kullanıcı arabirimini ziyaret ederek seçin hello **Düzenleyicisi işleri** sekmesine, görüntü aşağıdaki bilgileri benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![Düzenleyici işler sekmesi](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="b4bf9-316">Merhaba **sonraki Materialization** giriş İş çalıştırmaları hello bir sonraki başlatılışında hello içerir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="b4bf9-317">Benzer toohello hello proje girişi hello web kullanıcı arabirimini seçerek önceki iş akışı işini hello işinde bilgileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![Düzenleyici iş bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="b4bf9-319">Bu görüntü yalnızca başarılı çalıştırır hello zamanlanmış iş akışı içinde bireysel Eylemler hello işin gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="b4bf9-320">Merhaba birini seçin, toosee **eylem** girişleri.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="b4bf9-322">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b4bf9-322">Troubleshooting</span></span>

<span data-ttu-id="b4bf9-323">Merhaba Oozie UI tooview Oozie günlükleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="b4bf9-324">Ayrıca, MapReduce görevlerin hello iş akışı tarafından başlatılan bağlantıları tooJobTracker günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="b4bf9-325">sorun giderme için hello düzeni olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="b4bf9-326">Oozie Web kullanıcı arabirimini hello işi görüntüle.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="b4bf9-327">Bir hata veya belirli bir eylemi için hatası ise, select hello varsa, eylem toosee hello **hata iletisi** alan hello hatada daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="b4bf9-328">Varsa, hello eylem tooview hello URL'den hello eylem için daha fazla ayrıntı (örneğin, Jobtracker'a günlükleri) kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="b4bf9-329">Merhaba karşılaşabileceğiniz, belirli hataları verilmiştir ve nasıl tooresolve bunları.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="b4bf9-330">JA009: küme başlatılamıyor</span><span class="sxs-lookup"><span data-stu-id="b4bf9-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="b4bf9-331">**Belirtiler**: İş durumu değiştiğinde çok hello**ASKIYA**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="b4bf9-332">Merhaba işe yönelik ayrıntıları göster hello RunHiveScript durumu olarak **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="b4bf9-333">Merhaba eylem seçildikten hello aşağıdaki hata iletisini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="b4bf9-334">**Neden**: Merhaba hello kullanılan WASB adresleri **job.xml** dosya hello depolama kapsayıcısı veya depolama hesabı adı içermiyor.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="b4bf9-335">Merhaba WASB adres biçimini olmalıdır `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="b4bf9-336">**Çözümleme**: hello iş tarafından kullanılan hello WASB adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="b4bf9-337">JA002: Tooimpersonate Oozie izin verilmiyor &lt;kullanıcı ></span><span class="sxs-lookup"><span data-stu-id="b4bf9-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="b4bf9-338">**Belirtiler**: İş durumu değiştiğinde çok hello**ASKIYA**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="b4bf9-339">Merhaba işe yönelik ayrıntıları göster hello RunHiveScript durumu olarak **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="b4bf9-340">Merhaba eylem seçmek aşağıdaki hata iletisini hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="b4bf9-341">**Neden**: Geçerli izin ayarlarını Oozie izin vermez tooimpersonate hello belirtilen kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="b4bf9-342">**Çözümleme**: Oozie hello tooimpersonate kullanıcılar izin **kullanıcılar** grubu.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="b4bf9-343">Kullanım hello `groups USERNAME` kullanıcı hesabı hello toosee hello gruplarının bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="b4bf9-344">Merhaba kullanıcı hello üyesi değilse **kullanıcılar** grup, komut tooadd hello kullanıcı toohello grubu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="b4bf9-345">Merhaba kullanıcı toohello Grup eklenen Hdınsight algılamasından önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="b4bf9-346">Başlatıcı hata (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="b4bf9-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="b4bf9-347">**Belirtiler**: İş durumu değiştiğinde çok hello**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="b4bf9-348">Merhaba işe yönelik ayrıntıları göster hello RunSqoopExport durumu olarak **hata**.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="b4bf9-349">Merhaba eylem seçmek aşağıdaki hata iletisini hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="b4bf9-350">**Neden**: Sqoop veritabanıdır oluşturulamıyor tooload hello veritabanı sürücüsü gerekli tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="b4bf9-351">**Çözümleme**: Sqoop, Oozie işten kullanırken, hello veritabanı sürücüsünü hello ile Merhaba iş tarafından kullanılan diğer kaynakları (örneğin, hello workflow.xml) içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="b4bf9-352">Ayrıca hello hello veritabanı sürücüsünü içeren hello arşiv başvuru `<sqoop>...</sqoop>` hello workflow.xml bölümü.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="b4bf9-353">Örneğin, bu belgedeki hello işi için aşağıdaki adımları hello kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="b4bf9-354">Merhaba sqljdbc4.1.jar dosyası toohello /tutorials/useoozie dizinine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="b4bf9-355">Yeni bir satıra yukarıdaki XML aşağıdaki hello workflow.xml tooadd hello değiştirme `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="b4bf9-356">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4bf9-356">Next steps</span></span>

<span data-ttu-id="b4bf9-357">Bu öğreticide, nasıl öğrenilen toodefine Oozie iş akışı ve nasıl toorun Oozie işi.</span><span class="sxs-lookup"><span data-stu-id="b4bf9-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="b4bf9-358">Hdınsight ile çalışma hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b4bf9-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="b4bf9-359">[Hdınsight ile zamana dayalı Oozie düzenleyicisi kullanın][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="b4bf9-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="b4bf9-360">[Hdınsight'ta Hadoop işleri için verileri karşıya yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b4bf9-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b4bf9-361">[Hdınsight'ta Hadoop ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="b4bf9-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="b4bf9-362">[Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b4bf9-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b4bf9-363">[Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b4bf9-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="b4bf9-364">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="b4bf9-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
