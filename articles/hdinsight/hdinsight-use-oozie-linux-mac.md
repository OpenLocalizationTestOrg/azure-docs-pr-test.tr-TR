---
title: "Linux tabanlı Hdınsight'ta Hadoop Oozie iş akışlarını kullanın | Microsoft Docs"
description: "Linux tabanlı Hdınsight'ta Hadoop Oozie kullanın. Oozie iş akışı tanımlamak ve Oozie işi göndermek öğrenin."
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="7199a-104">Oozie Hadoop ile tanımlamak ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="7199a-105">Hdınsight'ta Hadoop ile Apache Oozie kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7199a-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="7199a-106">Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir.</span><span class="sxs-lookup"><span data-stu-id="7199a-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="7199a-107">Oozie Hadoop yığını ile tümleştirilir ve aşağıdaki işleri destekler:</span><span class="sxs-lookup"><span data-stu-id="7199a-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="7199a-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="7199a-108">Apache MapReduce</span></span>
* <span data-ttu-id="7199a-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="7199a-109">Apache Pig</span></span>
* <span data-ttu-id="7199a-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="7199a-110">Apache Hive</span></span>
* <span data-ttu-id="7199a-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="7199a-111">Apache Sqoop</span></span>

<span data-ttu-id="7199a-112">Oozie, Java programları veya kabuk betikleri gibi sisteme özel işleri planlamak için de kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="7199a-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="7199a-113">Hdınsight iş akışlarıyla tanımlamak için başka bir Azure Data Factory seçenektir.</span><span class="sxs-lookup"><span data-stu-id="7199a-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="7199a-114">Azure Data Factory hakkında daha fazla bilgi için bkz: [kullanım Pig ve Hive Data Factory ile][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="7199a-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7199a-115">Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.</span><span class="sxs-lookup"><span data-stu-id="7199a-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7199a-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7199a-116">Prerequisites</span></span>

* <span data-ttu-id="7199a-117">**Hdınsight kümesi**: bkz [Linux'ta Hdınsight ile çalışmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7199a-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7199a-118">Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7199a-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7199a-119">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="7199a-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7199a-120">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7199a-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="7199a-121">Örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="7199a-121">Example workflow</span></span>

<span data-ttu-id="7199a-122">Bu belgede kullanılan iş akışı iki eylemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7199a-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="7199a-123">Hive, Sqoop, MapReduce veya başka bir işlemin çalıştırma gibi görevler için tanımları eylemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7199a-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![İş akışı diyagramı][img-workflow-diagram]

1. <span data-ttu-id="7199a-125">Hive eylem kayıtları ayıklamak için HiveQL betiğini çalıştırır **hivesampletable** Hdınsight ile dahil.</span><span class="sxs-lookup"><span data-stu-id="7199a-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="7199a-126">Her veri satırının belirli bir mobil CİHAZDAN ziyaret açıklar.</span><span class="sxs-lookup"><span data-stu-id="7199a-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="7199a-127">Kayıt biçimi aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="7199a-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="7199a-128">Bu belgede kullanılan Hive betiğini (örneğin, Android veya iPhone) her platform için toplam ziyaret sayar ve yeni bir Hive tablosu için sayıları depolar.</span><span class="sxs-lookup"><span data-stu-id="7199a-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="7199a-129">Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="7199a-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="7199a-130">Sqoop eylem yeni Hive tablosu içeriğini bir Azure SQL veritabanındaki bir tablo dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="7199a-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="7199a-131">Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hadoop Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="7199a-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="7199a-132">Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="7199a-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="7199a-133">Çalışma dizini oluşturma</span><span class="sxs-lookup"><span data-stu-id="7199a-133">Create the working directory</span></span>

<span data-ttu-id="7199a-134">Oozie aynı dizinde depolanması bir iş için gereken kaynakları bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7199a-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="7199a-135">Bu örnekte **wasb: / / / öğreticileri/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="7199a-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="7199a-136">Bu dizin ve bu iş akışı tarafından oluşturulan yeni Hive tablosu tutan veri dizini oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="7199a-137">`-p` Parametresi oluşturulacak yolunda tüm dizinleri neden olur.</span><span class="sxs-lookup"><span data-stu-id="7199a-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="7199a-138">**Veri** dizini tarafından kullanılan verileri depolamak için kullanılan **useooziewf.hql** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="7199a-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="7199a-139">Ayrıca Oozie, kullanıcı hesabınızın Hive ve Sqoop işleri çalıştırırken bürünebileceğini sağlar aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7199a-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="7199a-140">Değiştir **kullanıcıadı** oturum açma adınız ile:</span><span class="sxs-lookup"><span data-stu-id="7199a-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="7199a-141">Kullanıcı zaten bir üyesidir hataları yoksayabilirsiniz `users` grubu.</span><span class="sxs-lookup"><span data-stu-id="7199a-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="7199a-142">Bir veritabanı sürücüsü Ekle</span><span class="sxs-lookup"><span data-stu-id="7199a-142">Add a database driver</span></span>

<span data-ttu-id="7199a-143">Bu iş akışı SQL veritabanına veri vermek için Sqoop kullandığından, SQL veritabanı ile iletişim için kullanılan JDBC sürücüsü kopyasını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7199a-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="7199a-144">Çalışma dizini kopyalamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="7199a-145">İş akışınızı bir MapReduce uygulaması içeren jar gibi diğer kaynaklar kullandıysanız, bu kaynakları de eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7199a-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="7199a-146">Hive sorgusunu tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7199a-146">Define the Hive query</span></span>

<span data-ttu-id="7199a-147">Bu belgenin sonraki bölümlerinde bir Oozie akışında kullanılan bir sorguyu tanımlayan bir HiveQL betiği oluşturmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="7199a-148">SSH kullanarak kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="7199a-149">Aşağıdaki komutu kullanarak, bir örnek verilmiştir `ssh` komutu.</span><span class="sxs-lookup"><span data-stu-id="7199a-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="7199a-150">Değiştir __kullanıcıadı__ SSH kullanıcı kümesi için.</span><span class="sxs-lookup"><span data-stu-id="7199a-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="7199a-151">Değiştir __CLUSTERNAME__ Hdınsight kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="7199a-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7199a-152">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7199a-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="7199a-153">SSH bağlantısı, bir dosya oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="7199a-154">Nano Düzenleyici açar sonra dosyanın içeriğini aşağıdaki sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="7199a-155">Komut dosyasında kullanılan iki değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7199a-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="7199a-156">**${hiveTableName}**: Oluşturulacak tablonun adını içerir</span><span class="sxs-lookup"><span data-stu-id="7199a-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="7199a-157">**${hiveDataFolder}**: Tablo için veri dosyalarının depolanacağı konumu içerir</span><span class="sxs-lookup"><span data-stu-id="7199a-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="7199a-158">İş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu HiveQL betiğini bu değerleri, çalışma zamanında geçirir.</span><span class="sxs-lookup"><span data-stu-id="7199a-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="7199a-159">Düzenleyiciden çıkmak için Ctrl-X tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7199a-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="7199a-160">İstendiğinde, seçin **Y** dosyayı kaydetmek için daha sonra kullanmak **Enter** kullanmak için **useooziewf.hql** dosya adı.</span><span class="sxs-lookup"><span data-stu-id="7199a-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="7199a-161">Kopyalamak için aşağıdaki komutları kullanın **useooziewf.hql** için **wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="7199a-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="7199a-162">Bu komutlar depolamak **useooziewf.hql** HDFS uyumlu depolama biriminde bir dosya kümesi için.</span><span class="sxs-lookup"><span data-stu-id="7199a-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="7199a-163">İş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="7199a-163">Define the workflow</span></span>

<span data-ttu-id="7199a-164">Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır.</span><span class="sxs-lookup"><span data-stu-id="7199a-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="7199a-165">İş akışını tanımlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="7199a-166">Oluşturun ve yeni bir dosya düzenlemek için şu deyimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="7199a-167">Nano Düzenleyici açar sonra aşağıdaki XML dosya içeriklerini girin:</span><span class="sxs-lookup"><span data-stu-id="7199a-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    <span data-ttu-id="7199a-168">İş akışında tanımlanan iki eylem vardır:</span><span class="sxs-lookup"><span data-stu-id="7199a-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="7199a-169">**RunHiveScript**: Bu eylem başlangıç eylemdir ve çalışan **useooziewf.hql** Hive betiği</span><span class="sxs-lookup"><span data-stu-id="7199a-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="7199a-170">**RunSqoopExport**: Bu eylem Sqoop kullanarak SQL veritabanına Hive komut dosyasından oluşturulan veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="7199a-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="7199a-171">Bu eylem yalnızca çalıştırır **RunHiveScript** eylem başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="7199a-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="7199a-172">İş akışı gibi birden çok girişi sahip `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="7199a-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="7199a-173">Bu girişler iş tanımında kullandığınız değerler değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="7199a-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="7199a-174">İş tanımı, bu belgenin sonraki bölümlerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7199a-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="7199a-175">Ayrıca unutmayın `<archive>sqljdbc4.jar</arcive>` Sqoop bölümünde girişi.</span><span class="sxs-lookup"><span data-stu-id="7199a-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="7199a-176">Bu giriş, bu eylem çalıştırıldığında bu arşiv Sqoop için kullanılabilmesi için Oozie bildirir.</span><span class="sxs-lookup"><span data-stu-id="7199a-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="7199a-177">CTRL-X, daha sonra kullanmak **Y** ve **Enter** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7199a-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="7199a-178">Kopyalamak için aşağıdaki komutu kullanın **workflow.xml** dosya **/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="7199a-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="7199a-179">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7199a-179">Create the database</span></span>

<span data-ttu-id="7199a-180">Bir Azure SQL veritabanı oluşturmak için adımları [bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7199a-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="7199a-181">Veritabanı oluştururken `oozietest` veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="7199a-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="7199a-182">Ayrıca veritabanı sunucusunun adını not edin.</span><span class="sxs-lookup"><span data-stu-id="7199a-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="7199a-183">Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="7199a-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="7199a-184">Bir tablo oluşturmak için SQL veritabanına bağlanmak için birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7199a-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="7199a-185">Aşağıdaki adımları kullanın [ücretsiz](http://www.freetds.org/) Hdınsight kümesine ait.</span><span class="sxs-lookup"><span data-stu-id="7199a-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="7199a-186">Ücretsiz Hdınsight kümesine yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="7199a-187">Ücretsiz bir kez yüklenir, önceden oluşturduğunuz bir SQL veritabanı sunucusuna bağlanmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="7199a-188">Aşağıdakine benzer bir çıktı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="7199a-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="7199a-189">Konumundaki `1>` isteminde, aşağıdaki satırları girin:</span><span class="sxs-lookup"><span data-stu-id="7199a-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="7199a-190">Zaman `GO` deyimi girilir, önceki deyimleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="7199a-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="7199a-191">Bu ifadeler adlı bir tablo oluşturmak **mobiledata** iş akışı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7199a-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="7199a-192">Tablo oluşturulduğunu doğrulamak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="7199a-193">Aşağıdakine benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="7199a-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="7199a-194">Girin `exit` adresindeki `1>` tsql yardımcı programı'ndan çıkmak komut istemi.</span><span class="sxs-lookup"><span data-stu-id="7199a-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="7199a-195">İş tanımı oluştur</span><span class="sxs-lookup"><span data-stu-id="7199a-195">Create the job definition</span></span>

<span data-ttu-id="7199a-196">İş tanımı workflow.xml nerede bulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="7199a-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="7199a-197">Ayrıca (örneğin, useooziewf.hql.) iş akışı tarafından kullanılan diğer dosyaları nerede bulacağını açıklanır Özellikler iş akışı içinde kullanılan ve dosyalar ilişkili değerleri de tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7199a-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="7199a-198">Varsayılan depolama tam adresini almak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="7199a-199">Bu adres yapılandırma dosyasında birazdan kullanılır:</span><span class="sxs-lookup"><span data-stu-id="7199a-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="7199a-200">Bu komut, bilgileri aşağıdaki XML benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="7199a-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="7199a-201">Hdınsight küme varsayılan depolama alanı olarak Azure Storage kullanıyorsa `<value>` öğenin içeriği ile başlar `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="7199a-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="7199a-202">Azure Data Lake Store yerine kullanılırsa, ile başlayan `adl://`.</span><span class="sxs-lookup"><span data-stu-id="7199a-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="7199a-203">İçeriğini kaydetme `<value>` şekliyle öğe, sonraki adımlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7199a-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="7199a-204">Küme headnode FQDN'sini almak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="7199a-205">Bu bilgiler, küme için Jobtracker'a adresi için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="7199a-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="7199a-206">Bu bilgiler aşağıdaki metni benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="7199a-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="7199a-207">Jobtracker'a için kullanılacak tam adresi 8050, Jobtracker'a için kullanılan bağlantı noktası olduğundan `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="7199a-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="7199a-208">Oozie iş tanımı yapılandırması oluşturmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="7199a-209">Nano düzenleyici açılır olduktan sonra aşağıdaki XML dosyasının içeriği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

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

   * <span data-ttu-id="7199a-210">Tüm örneklerinin yerine  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  aldığınız önceki sürümleri için varsayılan depolama değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="7199a-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="7199a-211">Yol ise bir `wasb` yolu, tam yolunu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7199a-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="7199a-212">Yalnızca kendisine kısaltın değil `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="7199a-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="7199a-213">Değiştir **JOBTRACKERADDRESS** daha önce aldığınız Jobtracker'a/ResourceManager adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="7199a-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="7199a-214">Değiştir **adınız** Hdınsight kümesi için oturum açma adınızı ile.</span><span class="sxs-lookup"><span data-stu-id="7199a-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="7199a-215">Değiştir **serverName**, **adminLogin**, ve **Admınpassword** Azure SQL veritabanınıza ilişkin bilgiler.</span><span class="sxs-lookup"><span data-stu-id="7199a-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="7199a-216">Bu dosyadaki bilgiler çoğunu (örneğin, ${iş}.) workflow.xml veya ooziewf.hql dosyalarında kullanılan değerleri doldurmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="7199a-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="7199a-217">**Oozie.wf.application.path** girdi tanımlar workflow.xml dosya nerede bulacağını bu iş tarafından çalıştırılan iş akışını içerir.</span><span class="sxs-lookup"><span data-stu-id="7199a-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="7199a-218">CTRL-X, daha sonra kullanmak **Y** ve **Enter** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7199a-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="7199a-219">Gönderme ve iş yönetimi</span><span class="sxs-lookup"><span data-stu-id="7199a-219">Submit and manage the job</span></span>

<span data-ttu-id="7199a-220">Aşağıdaki adımlar Oozie komutunu göndermek ve küme Oozie iş akışlarında yönetmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="7199a-221">Oozie kullanıcı dostu bir arabirim üzerinden komuttur [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="7199a-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7199a-222">Oozie komutunu kullanırken, FQDN için Hdınsight headnode kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7199a-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="7199a-223">Bu FQDN yalnızca kümeden erişilebilir veya küme aynı ağdaki diğer makinelerden bir Azure sanal ağda ise.</span><span class="sxs-lookup"><span data-stu-id="7199a-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="7199a-224">Oozie hizmeti URL'sini almak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="7199a-225">Bu bilgiler aşağıdaki XML benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="7199a-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="7199a-226">`http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` Bölümüdür Oozie komutu ile kullanılacak URL.</span><span class="sxs-lookup"><span data-stu-id="7199a-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="7199a-227">Her komut için yazmak zorunda kalmamak için URL için bir ortam değişkeni oluşturmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="7199a-228">URL, daha önce aldığınız adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7199a-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="7199a-229">İşi göndermek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="7199a-230">Bu komut iş bilgilerini yükler **job.xml** ve Oozie için gönderir, ancak değil çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7199a-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="7199a-231">Komut tamamlandığında, iş kimliği döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="7199a-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="7199a-232">Örneğin, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="7199a-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="7199a-233">Bu kimliği iş yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7199a-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="7199a-234">Aşağıdaki komutu kullanarak iş durumunu görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="7199a-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="7199a-235">Değiştir `<JOBID>` önceki adımda döndürülen Kimliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="7199a-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="7199a-236">Bu bilgiler aşağıdaki metni benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="7199a-236">This returns information similar to the following text:</span></span>

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

    <span data-ttu-id="7199a-237">Bu iş durumuna sahip `PREP`.</span><span class="sxs-lookup"><span data-stu-id="7199a-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="7199a-238">Bu durum, iş oluşturuldu, ancak başlatılmamış olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7199a-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="7199a-239">İşlemi başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="7199a-240">Değiştir `<JOBID>` döndürülen Kimliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="7199a-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="7199a-241">Bu komutun sonraki durumunu denetlemek, çalışır durumda olduğundan ve iş içindeki eylemler için bilgi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="7199a-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="7199a-242">Görev başarıyla tamamlandıktan sonra veri oluşturulur ve aşağıdaki komutları kullanarak SQL veritabanı tablosuna dışa aktarılan olduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7199a-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="7199a-243">Konumundaki `1>` isteminde, aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="7199a-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="7199a-244">Döndürülen bilgi aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="7199a-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="7199a-245">Oozie komutu hakkında daha fazla bilgi için bkz: [Oozie komut satırı aracı](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="7199a-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="7199a-246">Oozie REST API'si</span><span class="sxs-lookup"><span data-stu-id="7199a-246">Oozie REST API</span></span>

<span data-ttu-id="7199a-247">Oozie REST API ile Oozie iş kendi araçları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7199a-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="7199a-248">Hdınsight Oozie REST API kullanımı hakkında belirli bilgiler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7199a-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="7199a-249">**URI**: REST API erişilebilir gelen küme dışındaki`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="7199a-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="7199a-250">**Kimlik doğrulama**: küme HTTP hesabı (Yönetici) ve parolayı kullanarak API kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="7199a-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="7199a-251">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7199a-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="7199a-252">Oozie REST API kullanarak daha fazla bilgi için bkz: [Oozie Web Hizmetleri API'si](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="7199a-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="7199a-253">Oozie Web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="7199a-253">Oozie Web UI</span></span>

<span data-ttu-id="7199a-254">Oozie Web kullanıcı arabirimini Oozie işlerin durumunu web tabanlı bir görünüme kümede sağlar.</span><span class="sxs-lookup"><span data-stu-id="7199a-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="7199a-255">Web kullanıcı Arabirimi, aşağıdaki bilgileri görüntülemenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="7199a-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="7199a-256">İş durumu</span><span class="sxs-lookup"><span data-stu-id="7199a-256">Job status</span></span>
* <span data-ttu-id="7199a-257">İş tanımı</span><span class="sxs-lookup"><span data-stu-id="7199a-257">Job definition</span></span>
* <span data-ttu-id="7199a-258">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7199a-258">Configuration</span></span>
* <span data-ttu-id="7199a-259">İşte eylemlerin bir grafik</span><span class="sxs-lookup"><span data-stu-id="7199a-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="7199a-260">İşi için kayıtlar</span><span class="sxs-lookup"><span data-stu-id="7199a-260">Logs for the job</span></span>

<span data-ttu-id="7199a-261">Ayrıca bir işi içinde eylemler ayrıntılarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7199a-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="7199a-262">Oozie Web kullanıcı arabirimini erişmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="7199a-263">Bir Hdınsight kümesine SSH tüneli oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7199a-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="7199a-264">Bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7199a-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="7199a-265">Bir tünel oluşturulduktan sonra Ambari web kullanıcı Arabirimi, web tarayıcınızda açın.</span><span class="sxs-lookup"><span data-stu-id="7199a-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="7199a-266">Ambari site için bir URI **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="7199a-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="7199a-267">Değiştir **CLUSTERNAME** Linux tabanlı Hdınsight kümenizin adıyla.</span><span class="sxs-lookup"><span data-stu-id="7199a-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="7199a-268">Sayfanın sol taraftan seçin **Oozie**, ardından **hızlı bağlantılar**ve son olarak **Oozie Web kullanıcı arabirimini**.</span><span class="sxs-lookup"><span data-stu-id="7199a-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![görüntüsü menüler](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="7199a-270">Oozie Web kullanıcı Arabirimi iş akışı işleri çalıştırma görüntüleme için varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7199a-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="7199a-271">Tüm iş akışı işleri görmek için seçin **tüm işleri**.</span><span class="sxs-lookup"><span data-stu-id="7199a-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![Görüntülenen tüm işleri](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="7199a-273">İş hakkında daha fazla bilgi görüntülemek için bir iş seçin.</span><span class="sxs-lookup"><span data-stu-id="7199a-273">Select a job to view more information about the job.</span></span>

    ![İş bilgileri](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="7199a-275">İş bilgileri sekmesinden temel iş bilgileri ve iş içindeki ayrı Eylemler görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7199a-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="7199a-276">En üstte sekmeleri kullanarak iş tanımı, iş yapılandırması, erişim iş günlüğü görüntülemek veya yönlendirilmiş Çevrimsiz grafik (DAG) işin görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7199a-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="7199a-277">**İş günlüğü**: seçin **GetLogs** iş için tüm günlükleri almak için düğmesini veya kullanmak **girin arama filtresi** günlükleri filtrelemek için alan</span><span class="sxs-lookup"><span data-stu-id="7199a-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![İş günlüğü](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="7199a-279">**JobDAG**: DAG olan akışı gerçekleştirilecek veri yolları grafik bir genel bakış</span><span class="sxs-lookup"><span data-stu-id="7199a-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![İş DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="7199a-281">Eylemlerden birini seçerek **iş bilgileri** sekme eylemi için bilgileri getirir.</span><span class="sxs-lookup"><span data-stu-id="7199a-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="7199a-282">Örneğin, seçin **RunHiveScript** eylem.</span><span class="sxs-lookup"><span data-stu-id="7199a-282">For example, select the **RunHiveScript** action.</span></span>

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="7199a-284">Bir bağlantı gibi eylemin ayrıntılarını görebilirsiniz **Konsolu URL'si**.</span><span class="sxs-lookup"><span data-stu-id="7199a-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="7199a-285">Bu bağlantı, iş Jobtracker'a bilgilerini görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7199a-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="7199a-286">İşlerini zamanlama</span><span class="sxs-lookup"><span data-stu-id="7199a-286">Scheduling jobs</span></span>

<span data-ttu-id="7199a-287">Düzenleyici, başlangıç, bitiş ve işleri için oluşum sıklığını belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7199a-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="7199a-288">İş akışı için bir zamanlama tanımlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="7199a-289">Adlı bir dosya oluşturmak için aşağıdakileri kullanın **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="7199a-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="7199a-290">Aşağıdaki XML dosyasının içeriği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-290">Use the following XML as the contents of the file:</span></span>

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
    > <span data-ttu-id="7199a-291">`${...}` Değişkenleri, çalışma zamanında iş tanımında değerlere göre değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="7199a-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="7199a-292">Değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7199a-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="7199a-293">`${coordFrequency}`: Çalışan iş örneklerini arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="7199a-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="7199a-294">** `${coordStart}`: İş başlangıç zamanı.</span><span class="sxs-lookup"><span data-stu-id="7199a-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="7199a-295">`${coordEnd}`: İş bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="7199a-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="7199a-296">`${coordTimezone}`: Sabit bir saat diliminde (genellikle UTC ile gösterilir) hiçbir gün ışığından yararlanma saatine sahip olan düzenleyici işleri.</span><span class="sxs-lookup"><span data-stu-id="7199a-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="7199a-297">Bu saat dilimi "Oozie işleme saat dilimi." olarak adlandırılır</span><span class="sxs-lookup"><span data-stu-id="7199a-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="7199a-298">`${wfPath}`: Workflow.xml yolu.</span><span class="sxs-lookup"><span data-stu-id="7199a-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="7199a-299">Dosyayı kaydetmek için Ctrl-X, kullanmak **Y**, ve **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7199a-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="7199a-300">Bu proje için çalışma dizini dosyasını kopyalamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="7199a-301">Değiştirmek için aşağıdakileri kullanın **job.xml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="7199a-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="7199a-302">Aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="7199a-302">Make the following changes:</span></span>

   * <span data-ttu-id="7199a-303">İş akışı yerine Düzenleyicisi dosyasını çalıştırmak için oozie istemek üzere değiştirme `<name>oozie.wf.application.path</name>` için `<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="7199a-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="7199a-304">Ayarlamak için `workflowPath` aşağıdaki XML ekleme Düzenleyicisi tarafından kullanılan değişkeni:</span><span class="sxs-lookup"><span data-stu-id="7199a-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="7199a-305">Değiştir `wasb://mycontainer@mystorageaccount.blob.core.windows` diğer giriş job.xml dosyası kullanılan değeri olan metin.</span><span class="sxs-lookup"><span data-stu-id="7199a-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="7199a-306">Başlangıç tanımlamak için aşağıdaki XML bitiş ve düzenleyici sıklığı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7199a-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

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

       <span data-ttu-id="7199a-307">Bu değerleri 10 May 2017'den itibaren 12 Mayıs 2017 için bitiş zamanı üzerinde 12:00 PM için başlangıç saatini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7199a-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="7199a-308">Bu işi her gün aralığı.</span><span class="sxs-lookup"><span data-stu-id="7199a-308">The interval for running this job daily.</span></span> <span data-ttu-id="7199a-309">Dakika cinsinden sıklığıdır 1440 dakika 24 saat x 60 dakika kadar =.</span><span class="sxs-lookup"><span data-stu-id="7199a-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="7199a-310">Son olarak, saat dilimi UTC için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7199a-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="7199a-311">CTRL-X, daha sonra kullanmak **Y** ve **Enter** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7199a-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="7199a-312">İşi çalıştırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="7199a-313">Bu komut gönderir ve işini başlatır.</span><span class="sxs-lookup"><span data-stu-id="7199a-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="7199a-314">Oozie Web kullanıcı arabirimini ziyaret edin ve seçin, **Düzenleyicisi işleri** sekmesinde, aşağıdaki görüntüye benzer bilgileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7199a-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![Düzenleyici işler sekmesi](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="7199a-316">**Sonraki Materialization** girişi, işin bir sonraki çalıştırmasında içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7199a-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="7199a-317">Önceki iş akışının benzeyen, web kullanıcı Arabirimi iş girişine seçme bilgileri işinde görüntüler:</span><span class="sxs-lookup"><span data-stu-id="7199a-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![Düzenleyici iş bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="7199a-319">Bu görüntü yalnızca başarılı çalıştırır zamanlanmış iş akışı içinde bireysel Eylemler işinin gösterir.</span><span class="sxs-lookup"><span data-stu-id="7199a-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="7199a-320">İçin bkz, aşağıdakilerden birini seçin **eylem** girişleri.</span><span class="sxs-lookup"><span data-stu-id="7199a-320">To see that, select one of the **Action** entries.</span></span>

    ![Eylem bilgileri](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="7199a-322">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7199a-322">Troubleshooting</span></span>

<span data-ttu-id="7199a-323">Oozie UI Oozie günlükleri görüntülemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="7199a-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="7199a-324">Ayrıca, iş akışı tarafından başlatılan MapReduce görevler için Jobtracker'a günlüklerini bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="7199a-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="7199a-325">Sorun giderme için desen olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="7199a-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="7199a-326">İşi Oozie Web Arabiriminde görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7199a-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="7199a-327">Bir hata veya belirli bir eylemi için hatası ise, olmadığını görmek için bir eylem seçin **hata iletisi** alan hatada daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7199a-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="7199a-328">Varsa, eyleminden URL eylemi için (örneğin, Jobtracker'a günlükleri) daha fazla ayrıntı görüntülemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7199a-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="7199a-329">Karşılaşabileceğiniz belirli hataları ve bunların nasıl çözüleceği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7199a-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="7199a-330">JA009: küme başlatılamıyor</span><span class="sxs-lookup"><span data-stu-id="7199a-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="7199a-331">**Belirtiler**: İş durumu değişikliklerini **ASKIYA**.</span><span class="sxs-lookup"><span data-stu-id="7199a-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="7199a-332">İşe yönelik ayrıntıları göster olarak RunHiveScript durumu **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="7199a-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="7199a-333">Eylem seçildikten aşağıdaki hata iletisini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="7199a-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="7199a-334">**Neden**: kullanılan WASB adresleri **job.xml** dosya depolama kapsayıcısı veya depolama hesabı adı içermiyor.</span><span class="sxs-lookup"><span data-stu-id="7199a-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="7199a-335">WASB adres biçimini olmalıdır `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7199a-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="7199a-336">**Çözümleme**: İş tarafından kullanılan WASB adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7199a-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="7199a-337">JA002: Oozie almasına izin verilmiyor &lt;kullanıcı ></span><span class="sxs-lookup"><span data-stu-id="7199a-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="7199a-338">**Belirtiler**: İş durumu değişikliklerini **ASKIYA**.</span><span class="sxs-lookup"><span data-stu-id="7199a-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="7199a-339">İşe yönelik ayrıntıları göster olarak RunHiveScript durumu **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="7199a-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="7199a-340">Eylem seçmek aşağıdaki hata iletisini gösterir:</span><span class="sxs-lookup"><span data-stu-id="7199a-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="7199a-341">**Neden**: Geçerli izin ayarlarını Oozie belirtilen kullanıcı hesabı almasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="7199a-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="7199a-342">**Çözümleme**: Oozie izin verilir, kullanıcının kimliğine bürünmek için **kullanıcılar** grubu.</span><span class="sxs-lookup"><span data-stu-id="7199a-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="7199a-343">Kullanım `groups USERNAME` kullanıcı hesabının bir üyesi olduğu grupların görmek için.</span><span class="sxs-lookup"><span data-stu-id="7199a-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="7199a-344">Kullanıcı bir üyesi değilse **kullanıcılar** grup, kullanıcı grubuna eklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7199a-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="7199a-345">Kullanıcı grubuna eklenmiş olan Hdınsight algılamasından önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="7199a-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="7199a-346">Başlatıcı hata (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="7199a-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="7199a-347">**Belirtiler**: İş durumu değişikliklerini **KILLED**.</span><span class="sxs-lookup"><span data-stu-id="7199a-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="7199a-348">İşe yönelik ayrıntıları göster olarak RunSqoopExport durumu **hata**.</span><span class="sxs-lookup"><span data-stu-id="7199a-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="7199a-349">Eylem seçmek aşağıdaki hata iletisini gösterir:</span><span class="sxs-lookup"><span data-stu-id="7199a-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="7199a-350">**Neden**: Sqoop veritabanına erişmek için gerekli veritabanı sürücüsünü yükleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="7199a-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="7199a-351">**Çözümleme**: Sqoop, Oozie işten kullanırken, iş tarafından kullanılan veritabanı sürücüsünü diğer kaynaklarla (örneğin, workflow.xml) içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7199a-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="7199a-352">Ayrıca veritabanı sürücüyü içeren arşiv başvuru `<sqoop>...</sqoop>` workflow.xml bölümü.</span><span class="sxs-lookup"><span data-stu-id="7199a-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="7199a-353">Örneğin, bu belgede proje için aşağıdaki adımları kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="7199a-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="7199a-354">Sqljdbc4.1.jar dosyasını /tutorials/useoozie dizinine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="7199a-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="7199a-355">Yeni bir satıra yukarıdaki aşağıdaki XML eklemek için workflow.xml değiştirmek `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="7199a-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="7199a-356">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7199a-356">Next steps</span></span>

<span data-ttu-id="7199a-357">Bu öğreticide, Oozie iş akışı tanımlama ve Oozie işini çalıştır öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="7199a-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="7199a-358">Hdınsight ile çalışma hakkında daha fazla bilgi edinmek için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="7199a-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="7199a-359">[Hdınsight ile zamana dayalı Oozie düzenleyicisi kullanın][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="7199a-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="7199a-360">[Hdınsight'ta Hadoop işleri için verileri karşıya yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="7199a-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="7199a-361">[Hdınsight'ta Hadoop ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="7199a-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="7199a-362">[Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="7199a-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="7199a-363">[Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="7199a-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="7199a-364">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="7199a-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
