---
title: "Hdınsight'ta Hadoop Oozie kullanın | Microsoft Docs"
description: "Hadoop Oozie Hdınsight, büyük veri hizmeti kullanın. Oozie iş akışı tanımlamak ve Oozie işi göndermek öğrenin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 36fe3e4220ec92699b6d52cba47cd6b83f361d66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="0f2cf-104">Oozie Hadoop ile tanımlamak ve Hdınsight'ta bir iş akışını çalıştırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-104">Use Oozie with Hadoop to define and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="0f2cf-105">Apache Oozie bir iş akışı tanımlayın ve üzerinde Hdınsight iş akışını çalıştırmak için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-105">Learn how to use Apache Oozie to define a workflow and run the workflow on HDInsight.</span></span> <span data-ttu-id="0f2cf-106">Oozie Düzenleyicisi hakkında bilgi edinmek için [Hdınsight ile zamana dayalı Oozie Düzenleyicisi Hadoop kullanma][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="0f2cf-106">To learn about the Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="0f2cf-107">Azure Data Factory öğrenmek için bkz: [kullanım Pig ve Hive Data Factory ile][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="0f2cf-107">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="0f2cf-108">Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="0f2cf-109">Bu Hadoop yığını ile tümleşiktir ve Apache MapReduce, Apache Pig, Apache Hive ve Apache Sqoop için Hadoop işlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-109">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="0f2cf-110">Ayrıca, Java programları veya kabuk betikleri gibi sisteme özel işleri planlamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-110">It can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="0f2cf-111">Bu öğreticide yönergeleri izleyerek uygulama iş akışı iki eylemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-111">The workflow you implement by following the instructions in this tutorial contains two actions:</span></span>

![İş akışı diyagramı][img-workflow-diagram]

1. <span data-ttu-id="0f2cf-113">Hive eylem log4j dosyasını her günlük düzeyi türünün oluşumları saymak için HiveQL betiğini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-113">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="0f2cf-114">Her log4j dosyasını türünün ve önem örneğin gösterir [günlük düzeyi] alan içeren bir dizi alanlarının oluşur:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows the type and the severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="0f2cf-115">Hive betiği çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-115">The Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="0f2cf-116">Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="0f2cf-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="0f2cf-117">Sqoop eylem HiveQL çıktı Azure SQL veritabanındaki bir tablo dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-117">A Sqoop action exports the HiveQL output to a table in an Azure SQL database.</span></span> <span data-ttu-id="0f2cf-118">Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hadoop Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="0f2cf-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="0f2cf-119">Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler nelerdir?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="0f2cf-119">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="0f2cf-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0f2cf-120">Prerequisites</span></span>
<span data-ttu-id="0f2cf-121">Bu öğreticiye başlamadan önce aşağıdaki öğesi olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-121">Before you begin this tutorial, you must have the following item:</span></span>

* <span data-ttu-id="0f2cf-122">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="0f2cf-123">Oozie iş akışı ve ilgili HiveQL betiğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="0f2cf-123">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="0f2cf-124">Oozie iş akışı tanımları hPDL (XML işlem tanım dili) yazılır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="0f2cf-125">Varsayılan iş akışı dosya adı *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-125">The default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="0f2cf-126">Bu öğreticide kullandığınız iş akışı dosyası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-126">The following is the workflow file you use in this tutorial.</span></span>

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>

<span data-ttu-id="0f2cf-127">İş akışında tanımlanan iki eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-127">There are two actions defined in the workflow.</span></span> <span data-ttu-id="0f2cf-128">Başlangıç için eylem *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-128">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="0f2cf-129">Eylem başarıyla çalışırsa, bir sonraki eylem olan *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-129">If the action runs successfully, the next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="0f2cf-130">RunHiveScript birkaç değişkeni yok.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-130">The RunHiveScript has several variables.</span></span> <span data-ttu-id="0f2cf-131">Azure PowerShell kullanarak Oozie iş istasyonunuzdan gönderdiğinizde değerlerini geçirin.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-131">You pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="0f2cf-132">İş akışı değişkenleri</span><span class="sxs-lookup"><span data-stu-id="0f2cf-132">Workflow variables</span></span></th><th><span data-ttu-id="0f2cf-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f2cf-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="0f2cf-134">${Jobtracker'a}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-134">${jobTracker}</span></span></td><td><span data-ttu-id="0f2cf-135">Hadoop işi İzleyicisi URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-135">Specifies the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="0f2cf-136">Kullanım <strong>jobtrackerhost:9010</strong> Hdınsight sürüm 3.0 ve 2.1 içinde.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="0f2cf-137">${İş}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-137">${nameNode}</span></span></td><td><span data-ttu-id="0f2cf-138">Hadoop adı düğümü URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-138">Specifies the URL of the Hadoop name node.</span></span> <span data-ttu-id="0f2cf-139">Örneğin, varsayılan dosya sistemi adresi kullanın <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-139">Use the default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="0f2cf-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-140">${queueName}</span></span></td><td><span data-ttu-id="0f2cf-141">İş için gönderildiğinde sıra adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-141">Specifies the queue name that the job is submitted to.</span></span> <span data-ttu-id="0f2cf-142">Kullanım <strong>varsayılan</strong>.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-142">Use the <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="0f2cf-143">Eylem değişkeni yığını</span><span class="sxs-lookup"><span data-stu-id="0f2cf-143">Hive action variable</span></span></th><th><span data-ttu-id="0f2cf-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f2cf-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="0f2cf-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="0f2cf-146">Create Table Hive komutu için kaynak dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-146">Specifies the source directory for the Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="0f2cf-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="0f2cf-148">INSERT üzerine deyimi için çıkış klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-148">Specifies the output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="0f2cf-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-149">${hiveTableName}</span></span></td><td><span data-ttu-id="0f2cf-150">Log4j veri dosyalarına başvuran Hive tablosu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-150">Specifies the name of the Hive table that references the log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="0f2cf-151">Sqoop eylem değişkeni</span><span class="sxs-lookup"><span data-stu-id="0f2cf-151">Sqoop action variable</span></span></th><th><span data-ttu-id="0f2cf-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f2cf-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="0f2cf-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="0f2cf-154">Azure SQL veritabanı bağlantı dizesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-154">Specifies the Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="0f2cf-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="0f2cf-156">Veriler için dışa Azure SQL veritabanı tablosu belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-156">Specifies the Azure SQL database table where the data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="0f2cf-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="0f2cf-158">Hive Ekle üzerine deyimi için çıkış klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-158">Specifies the output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="0f2cf-159">Bu Sqoop verme (verme-dir) için aynı klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-159">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="0f2cf-160">Oozie iş akışı ve iş akışı eylemlerinin kullanma hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (Hdınsight sürüm 3.0 için) veya [Apache Oozie 3.3.2 belgelerine] [ apache-oozie-332] (Hdınsight sürüm 2.1 için).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="0f2cf-161">İş akışı Hive eylemde HiveQL komut dosyasını çağırır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-161">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="0f2cf-162">Bu komut dosyasını üç HiveQL ifadelerini içerir:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="0f2cf-163">**DROP TABLE deyimi** varsa log4j Hive tablosu siler.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-163">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="0f2cf-164">**CREATE TABLE deyimi** log4j günlük dosyası konumuna işaret log4j Hive dış tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-164">**The CREATE TABLE statement** creates a log4j Hive external table that points to the location of the log4j log file.</span></span> <span data-ttu-id="0f2cf-165">Alan sınırlayıcı ",".</span><span class="sxs-lookup"><span data-stu-id="0f2cf-165">The field delimiter is ",".</span></span> <span data-ttu-id="0f2cf-166">Varsayılan satır ayırıcı "\n" dir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-166">The default line delimiter is "\n".</span></span> <span data-ttu-id="0f2cf-167">Hive dış tablo birden çok kez Oozie iş akışını çalıştırmak istiyorsanız, özgün konumundan kaldırılmakta olan veri dosyası önlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-167">A Hive external table is used to avoid the data file being removed from the original location if you want to run the Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="0f2cf-168">**INSERT üzerine deyimi** log4j Hive tablosu her günlük düzeyi türünden oluşumlarını sayar ve çıktı Azure storage'da bir blob kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-168">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and saves the output to a blob in Azure Storage.</span></span>

<span data-ttu-id="0f2cf-169">Komut dosyasında kullanılan üç değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-169">There are three variables used in the script:</span></span>

* <span data-ttu-id="0f2cf-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-170">${hiveTableName}</span></span>
* <span data-ttu-id="0f2cf-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="0f2cf-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="0f2cf-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="0f2cf-173">İş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu değerleri bu HiveQL betiğini çalışma zamanında geçirir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-173">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time.</span></span>

<span data-ttu-id="0f2cf-174">İş akışı dosyası ve HiveQL dosya bir blob kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-174">Both the workflow file and the HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="0f2cf-175">Daha sonra Bu öğreticide kullandığınız PowerShell Betiği hem dosyaları için varsayılan depolama hesabı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-175">The PowerShell script you use later in this tutorial copies both files to the default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="0f2cf-176">PowerShell kullanarak Oozie işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="0f2cf-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="0f2cf-177">Azure PowerShell cmdlet'lerin Oozie işleri tanımlamak için şu anda sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="0f2cf-178">Kullanabileceğiniz **Invoke-RestMethod** cmdlet'ini Oozie web hizmetlerini çağırır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-178">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="0f2cf-179">Oozie web hizmetleri API'si bir HTTP REST JSON API'dir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-179">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="0f2cf-180">Oozie web hizmetleri API'si hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (Hdınsight sürüm 3.0 için) veya [Apache Oozie 3.3.2 belgelerine] [ apache-oozie-332] (Hdınsight sürüm 2.1 için).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-180">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="0f2cf-181">Bu bölümdeki PowerShell Betiği aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-181">The PowerShell script in this section performs the following steps:</span></span>

1. <span data-ttu-id="0f2cf-182">Azure'a bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-182">Connect to Azure.</span></span>
2. <span data-ttu-id="0f2cf-183">Bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-183">Create an Azure resource group.</span></span> <span data-ttu-id="0f2cf-184">Daha fazla bilgi için bkz: [kullanım Azure PowerShell'i Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="0f2cf-185">Bir Azure SQL veritabanı sunucusu, Azure SQL veritabanına ve iki tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="0f2cf-186">Bunlar, Sqoop eylem iş akışı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-186">These are used by the Sqoop action in the workflow.</span></span>
   
    <span data-ttu-id="0f2cf-187">Tablo adı *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-187">The table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="0f2cf-188">Oozie işlerini çalıştırmak için kullanılan Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-188">Create an HDInsight cluster used to run Oozie jobs.</span></span>
   
    <span data-ttu-id="0f2cf-189">Küme incelemek için Azure portalında veya Azure PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-189">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="0f2cf-190">Oozie iş akışı dosyası ve HiveQL komut dosyası için varsayılan dosya sistemi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-190">Copy the oozie workflow file and the HiveQL script file to the default file system.</span></span>
   
    <span data-ttu-id="0f2cf-191">Her iki dosyaları bir ortak Blob kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="0f2cf-192">HiveQL betiğini (useoozie.hql) (wasb:///tutorials/useoozie/useoozie.hql) Azure depolama alanına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-192">Copy the HiveQL script (useoozie.hql) to Azure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="0f2cf-193">Workflow.XML için wasb:///tutorials/useoozie/workflow.xml kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-193">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="0f2cf-194">Veri dosyasını kopyalayın (/ example/data/sample.log) wasb:///tutorials/useoozie/data/sample.log için.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-194">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="0f2cf-195">Oozie işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="0f2cf-196">OOzie iş sonuçları incelemek için Azure SQL veritabanına bağlanmak için Visual Studio veya diğer Araçlar'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-196">To examine the OOzie job results, use Visual Studio or other tools to connect to the Azure SQL Database.</span></span>

<span data-ttu-id="0f2cf-197">Komut dosyası aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-197">Here is the script.</span></span>  <span data-ttu-id="0f2cf-198">Windows PowerShell ISE komut dosyasını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-198">You can run the script from Windows PowerShell ISE.</span></span> <span data-ttu-id="0f2cf-199">Yalnızca ilk 7 değişkenleri yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-199">You only need to configure the first 7 variables.</span></span>

    #region - provide the following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # The default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating the log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate the copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy the sample.log file

    Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate the copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

    <property>
        <name>nameNode</name>
        <value>$storageUrI</value>
    </property>

    <property>
        <name>jobTracker</name>
        <value>jobtrackerhost:9010</value>
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
        <value>$hiveScript</value>
    </property>

    <property>
        <name>hiveTableName</name>
        <value>$hiveTableName</value>
    </property>

    <property>
        <name>hiveDataFolder</name>
        <value>$hiveDataFolder</value>
    </property>

    <property>
        <name>hiveOutputFolder</name>
        <value>$hiveOutputFolder</value>
    </property>

    <property>
        <name>sqlDatabaseConnectionString</name>
        <value>&quot;$sqlDatabaseConnectionString&quot;</value>
    </property>

    <property>
        <name>sqlDatabaseTableName</name>
        <value>$SQLDatabaseTableName</value>
    </property>

    <property>
        <name>user.name</name>
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting the Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="0f2cf-200">**Öğreticiyi yeniden çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-200">**To re-run the tutorial**</span></span>

<span data-ttu-id="0f2cf-201">İş akışını yeniden çalıştırmak için aşağıdaki öğeleri silmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-201">To re-run the workflow, you must delete the following items:</span></span>

* <span data-ttu-id="0f2cf-202">Hive betiği çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="0f2cf-202">The Hive script output file</span></span>
* <span data-ttu-id="0f2cf-203">Log4jLogsCount tablosundaki verileri</span><span class="sxs-lookup"><span data-stu-id="0f2cf-203">The data in the log4jLogsCount table</span></span>

<span data-ttu-id="0f2cf-204">Kullanabileceğiniz bir örnek PowerShell komut dosyasını şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete the Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="0f2cf-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f2cf-205">Next steps</span></span>
<span data-ttu-id="0f2cf-206">Bu öğreticide, Oozie iş akışı tanımlama ve PowerShell kullanarak bir Oozie işi çalıştırmak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-206">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job by using PowerShell.</span></span> <span data-ttu-id="0f2cf-207">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="0f2cf-207">To learn more, see the following articles:</span></span>

* <span data-ttu-id="0f2cf-208">[Hdınsight ile zamana dayalı Oozie düzenleyicisi kullanın][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="0f2cf-209">[Hadoop ile hdınsight'ta Hive mobil ahize kullanımını çözümleme için kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-209">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="0f2cf-210">[Hdınsight ile Azure Blob storage kullanma][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="0f2cf-211">[PowerShell kullanarak Hdınsight yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="0f2cf-212">[Hdınsight'ta Hadoop işleri için verileri karşıya yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="0f2cf-213">[Hdınsight'ta Hadoop ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="0f2cf-214">[Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="0f2cf-215">[Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="0f2cf-216">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="0f2cf-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
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
