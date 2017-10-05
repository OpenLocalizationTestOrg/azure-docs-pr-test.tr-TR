---
title: "Hdınsight'ta Hadoop Oozie Düzenleyicisi zamana dayalı kullanın | Microsoft Docs"
description: "Hdınsight, büyük veri hizmeti zamana dayalı Hadoop Oozie düzenleyicisi kullanın. Oozie iş akışları ve düzenleyiciler tanımlayın ve işleri gönderme hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="340dc-104">İş akışları tanımlamak ve işleri koordine etmek için hdınsight'ta Hadoop ile zamana dayalı Oozie düzenleyicisi kullanın</span><span class="sxs-lookup"><span data-stu-id="340dc-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="340dc-105">Bu makalede, iş akışları ve düzenleyiciler nasıl tanımlanacağı ve zamana dayalı Düzenleyicisi işleri tetiklemek nasıl öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="340dc-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="340dc-106">Geçtikleri faydalıdır [Hdınsight ile kullanım Oozie] [ hdinsight-use-oozie] önce bu makaleyi okuyun.</span><span class="sxs-lookup"><span data-stu-id="340dc-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="340dc-107">Oozie ek olarak, Azure Data Factory kullanarak işleri de zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="340dc-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="340dc-108">Azure Data Factory öğrenmek için bkz: [kullanım Pig ve Hive Data Factory ile](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="340dc-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="340dc-109">Bu makalede Windows tabanlı Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="340dc-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="340dc-110">Oozie, Linux tabanlı bir kümede zaman tabanlı işleri de dahil olmak üzere kullanma hakkında bilgi için bkz: [tanımlamak ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırmak için Hadoop ile kullanım Oozie](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="340dc-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="340dc-111">Oozie nedir</span><span class="sxs-lookup"><span data-stu-id="340dc-111">What is Oozie</span></span>
<span data-ttu-id="340dc-112">Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir.</span><span class="sxs-lookup"><span data-stu-id="340dc-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="340dc-113">Bu Hadoop yığını ile tümleşiktir ve Apache MapReduce, Apache Pig, Apache Hive ve Apache Sqoop için Hadoop işlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="340dc-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="340dc-114">Ayrıca, Java programları veya kabuk betikleri gibi sisteme özel işleri planlamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="340dc-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="340dc-115">Aşağıdaki resimde, gerçekleştireceksiniz iş akışı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="340dc-115">The following image shows the workflow you will implement:</span></span>

![İş akışı diyagramı][img-workflow-diagram]

<span data-ttu-id="340dc-117">İş akışı iki eylemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="340dc-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="340dc-118">Hive eylem her günlük düzeyi türü log4j günlük dosyasında oluşumları saymak için HiveQL betiğini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="340dc-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="340dc-119">Her log4j günlük türünün ve önem örneğin göstermek için [günlük düzeyi] alan içeren bir dizi alanlarının oluşur:</span><span class="sxs-lookup"><span data-stu-id="340dc-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="340dc-120">Hive betiği çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="340dc-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="340dc-121">Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="340dc-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="340dc-122">Sqoop eylem HiveQL eylem çıkışı bir Azure SQL veritabanındaki bir tablo dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="340dc-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="340dc-123">Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="340dc-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="340dc-124">Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [Hdınsight tarafından sağlanan küme sürümlerindeki yenilikler nelerdir?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="340dc-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="340dc-125">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="340dc-125">Prerequisites</span></span>
<span data-ttu-id="340dc-126">Bu öğreticiye başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="340dc-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="340dc-127">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="340dc-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="340dc-128">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışıdır** ve 1 Ocak 2017 tarihine kadar kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="340dc-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="340dc-129">Bu belgede yer alan adımlar, Azure Resource Manager ile çalışan yeni HDInsight cmdlet'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="340dc-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="340dc-130">Azure PowerShell’in en son sürümünü yüklemek için lütfen [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs)’daki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="340dc-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="340dc-131">Azure Resource Manager’la çalışan yeni cmdlet’lerle kullanmak için değiştirilmesi gereken komut dosyalarınız varsa, daha fazla bilgi için bkz. [HDInsight kümeleri için Azure Resource Manager tabanlı geliştirme araçlarına geçme](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="340dc-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="340dc-132">**Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="340dc-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="340dc-133">Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight kümeleri oluşturma][hdinsight-provision], veya [Hdınsight kullanmaya başlama][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="340dc-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="340dc-134">Öğreticiyi incelemek için aşağıdaki veriler gerekir:</span><span class="sxs-lookup"><span data-stu-id="340dc-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="340dc-135">Küme özelliği</span><span class="sxs-lookup"><span data-stu-id="340dc-135">Cluster property</span></span></th><th><span data-ttu-id="340dc-136">Windows PowerShell değişken adı</span><span class="sxs-lookup"><span data-stu-id="340dc-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="340dc-137">Değer</span><span class="sxs-lookup"><span data-stu-id="340dc-137">Value</span></span></th><th><span data-ttu-id="340dc-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="340dc-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="340dc-139">Hdınsight küme adı</span><span class="sxs-lookup"><span data-stu-id="340dc-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="340dc-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="340dc-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="340dc-141">Bu öğretici çalışacağı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="340dc-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-142">Hdınsight küme kullanıcı</span><span class="sxs-lookup"><span data-stu-id="340dc-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="340dc-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="340dc-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="340dc-144">Hdınsight küme kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="340dc-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="340dc-145">Hdınsight küme kullanıcı parolası</span><span class="sxs-lookup"><span data-stu-id="340dc-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="340dc-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="340dc-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="340dc-147">Hdınsight küme kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="340dc-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-148">Azure depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="340dc-148">Azure storage account name</span></span></td><td><span data-ttu-id="340dc-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="340dc-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="340dc-150">Bir Azure depolama hesabı Hdınsight küme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="340dc-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="340dc-151">Bu öğretici için küme sağlama işlemi sırasında belirtilen varsayılan depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="340dc-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-152">Azure Blob kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="340dc-152">Azure Blob container name</span></span></td><td><span data-ttu-id="340dc-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="340dc-153">$containerName</span></span></td><td></td><td><span data-ttu-id="340dc-154">Bu örnekte, varsayılan Hdınsight küme dosya sistemi için kullanılan Azure Blob Depolama kapsayıcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="340dc-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="340dc-155">Varsayılan olarak, Hdınsight kümesi ile aynı ada sahip.</span><span class="sxs-lookup"><span data-stu-id="340dc-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="340dc-156">
* **Bir Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="340dc-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="340dc-157">İş istasyonunuzu erişime izin verecek şekilde SQL veritabanı sunucusu için bir güvenlik duvarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="340dc-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="340dc-158">Bir Azure SQL veritabanı oluşturma ve Güvenlik Duvarı'nı yapılandırma hakkında yönergeler için bkz. [Azure SQL veritabanı ile çalışmaya başlamak] [sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="340dc-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="340dc-159">Bu makalede, Bu öğretici için gereksinim duyduğunuz Azure SQL veritabanı tablosu oluşturmak için bir Windows PowerShell komut dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="340dc-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="340dc-160">SQL veritabanı özelliği</span><span class="sxs-lookup"><span data-stu-id="340dc-160">SQL database property</span></span></th><th><span data-ttu-id="340dc-161">Windows PowerShell değişken adı</span><span class="sxs-lookup"><span data-stu-id="340dc-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="340dc-162">Değer</span><span class="sxs-lookup"><span data-stu-id="340dc-162">Value</span></span></th><th><span data-ttu-id="340dc-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="340dc-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="340dc-164">SQL veritabanı sunucusu adı</span><span class="sxs-lookup"><span data-stu-id="340dc-164">SQL database server name</span></span></td><td><span data-ttu-id="340dc-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="340dc-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="340dc-166">SQL veritabanı sunucusuna Sqoop verileri dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="340dc-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="340dc-167">SQL veritabanı oturum açma adı</span><span class="sxs-lookup"><span data-stu-id="340dc-167">SQL database login name</span></span></td><td><span data-ttu-id="340dc-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="340dc-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="340dc-169">SQL veritabanı oturum açma adı.</span><span class="sxs-lookup"><span data-stu-id="340dc-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-170">SQL veritabanı oturum açma parolası</span><span class="sxs-lookup"><span data-stu-id="340dc-170">SQL database login password</span></span></td><td><span data-ttu-id="340dc-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="340dc-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="340dc-172">SQL veritabanı oturum açma parolası.</span><span class="sxs-lookup"><span data-stu-id="340dc-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-173">SQL veritabanı adı</span><span class="sxs-lookup"><span data-stu-id="340dc-173">SQL database name</span></span></td><td><span data-ttu-id="340dc-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="340dc-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="340dc-175">Azure SQL veritabanı Sqoop verileri dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="340dc-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="340dc-176">Varsayılan olarak, Azure Hdınsight gibi Azure hizmetlerinden bağlantıları bir Azure SQL veritabanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="340dc-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="340dc-177">Bu güvenlik duvarı ayarı devre dışıysa, Azure Portalı'ndan etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="340dc-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="340dc-178">Bir SQL veritabanı oluşturma ve güvenlik duvarı kuralları yapılandırma hakkında daha fazla yönerge için bkz: [oluşturma ve yapılandırma SQL veritabanı][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="340dc-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="340dc-179">Doldurma tablolardaki değerleri.</span><span class="sxs-lookup"><span data-stu-id="340dc-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="340dc-180">Bu öğreticide olmaya yardımcı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="340dc-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="340dc-181">Oozie iş akışı ve ilgili HiveQL betiğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="340dc-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="340dc-182">Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır.</span><span class="sxs-lookup"><span data-stu-id="340dc-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="340dc-183">Varsayılan iş akışı dosya adı *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="340dc-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="340dc-184">İş akışı dosyasını yerel olarak kaydedin ve ardından daha sonra Bu öğreticide Azure PowerShell kullanarak Hdınsight kümesine dağıtın.</span><span class="sxs-lookup"><span data-stu-id="340dc-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="340dc-185">İş akışı Hive eylemde HiveQL komut dosyasını çağırır.</span><span class="sxs-lookup"><span data-stu-id="340dc-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="340dc-186">Bu komut dosyasını üç HiveQL ifadelerini içerir:</span><span class="sxs-lookup"><span data-stu-id="340dc-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="340dc-187">**DROP TABLE deyimi** varsa log4j Hive tablosu siler.</span><span class="sxs-lookup"><span data-stu-id="340dc-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="340dc-188">**CREATE TABLE deyimi** log4j günlük dosyasının; konumuna işaret eden bir log4j Hive dış tablosu oluşturur</span><span class="sxs-lookup"><span data-stu-id="340dc-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="340dc-189">**Log4j günlük dosyasının konumunu**.</span><span class="sxs-lookup"><span data-stu-id="340dc-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="340dc-190">Alan sınırlayıcı ",".</span><span class="sxs-lookup"><span data-stu-id="340dc-190">The field delimiter is ",".</span></span> <span data-ttu-id="340dc-191">Varsayılan satır ayırıcı "\n" dir.</span><span class="sxs-lookup"><span data-stu-id="340dc-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="340dc-192">Hive dış tablo durumunda, birden çok kez Oozie iş akışını çalıştırmak istediğiniz veri dosyasındaki özgün konumundan kaldırılmasını önlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="340dc-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="340dc-193">**INSERT üzerine deyimi** sayıları her günlük düzeyi türü log4j Hive tablosu ve oluşumlarını kaydeder çıkışı bir Azure Blob depolama konumuna.</span><span class="sxs-lookup"><span data-stu-id="340dc-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="340dc-194">Bilinen bir Hive yolu sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="340dc-194">There is a known Hive path issue.</span></span> <span data-ttu-id="340dc-195">Bu sorunla Oozie iş gönderirken çalışır.</span><span class="sxs-lookup"><span data-stu-id="340dc-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="340dc-196">Sorunu düzeltmek için yönergeleri TechNet Wiki'de bulunabilir: [Hdınsight Hive hata: yeniden adlandırılamıyor][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="340dc-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="340dc-197">**İş akışı tarafından çağrılacak HiveQL komut dosyasını tanımlamak için**</span><span class="sxs-lookup"><span data-stu-id="340dc-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="340dc-198">Aşağıdaki içerik ile bir metin dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="340dc-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="340dc-199">Komut dosyasında kullanılan üç değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="340dc-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="340dc-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="340dc-200">${hiveTableName}</span></span>
   * <span data-ttu-id="340dc-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="340dc-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="340dc-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="340dc-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="340dc-203">İş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu değerleri bu HiveQL betiğini çalışma zamanında geçer.</span><span class="sxs-lookup"><span data-stu-id="340dc-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="340dc-204">Dosyayı Farklı Kaydet **C:\Tutorials\UseOozie\useooziewf.hql** ANSI (ASCII) kodlama kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="340dc-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="340dc-205">(Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.) Bu komut dosyası Hdınsight kümesine daha sonra öğreticide dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="340dc-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="340dc-206">**Bir iş akışı tanımlamak için**</span><span class="sxs-lookup"><span data-stu-id="340dc-206">**To define a workflow**</span></span>

1. <span data-ttu-id="340dc-207">Aşağıdaki içerik ile bir metin dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="340dc-207">Create a text file with the following content:</span></span>

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
    ```

    <span data-ttu-id="340dc-208">İş akışında tanımlanan iki eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="340dc-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="340dc-209">Başlangıç için eylem *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="340dc-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="340dc-210">Eylem çalıştırıyorsa *Tamam*, bir sonraki eylem *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="340dc-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="340dc-211">RunHiveScript birkaç değişkeni yok.</span><span class="sxs-lookup"><span data-stu-id="340dc-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="340dc-212">Azure PowerShell kullanarak Oozie iş istasyonunuzdan gönderdiğinizde değerler geçer.</span><span class="sxs-lookup"><span data-stu-id="340dc-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="340dc-213">İş akışı değişkenleri</span><span class="sxs-lookup"><span data-stu-id="340dc-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="340dc-214">İş akışı değişkenleri</span><span class="sxs-lookup"><span data-stu-id="340dc-214">Workflow variables</span></span></th><th><span data-ttu-id="340dc-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="340dc-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="340dc-216">${Jobtracker'a}</span><span class="sxs-lookup"><span data-stu-id="340dc-216">${jobTracker}</span></span></td><td><span data-ttu-id="340dc-217">Hadoop işi İzleyicisi URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="340dc-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="340dc-218">Kullanım <strong>jobtrackerhost:9010</strong> Hdınsight sürüm 3.0 ve 2.0 küme.</span><span class="sxs-lookup"><span data-stu-id="340dc-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-219">${İş}</span><span class="sxs-lookup"><span data-stu-id="340dc-219">${nameNode}</span></span></td><td><span data-ttu-id="340dc-220">Hadoop adı düğümü URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="340dc-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="340dc-221">Varsayılan dosya sistemi wasb kullanın: / / adres, örneğin, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="340dc-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="340dc-222">${queueName}</span></span></td><td><span data-ttu-id="340dc-223">İş için gönderilen sıra adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="340dc-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="340dc-224">Kullanım <strong>varsayılan</strong>.</span><span class="sxs-lookup"><span data-stu-id="340dc-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="340dc-225">Hive eylem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="340dc-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="340dc-226">Eylem değişkeni yığını</span><span class="sxs-lookup"><span data-stu-id="340dc-226">Hive action variable</span></span></th><th><span data-ttu-id="340dc-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="340dc-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="340dc-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="340dc-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="340dc-229">Create Table Hive komutu için kaynak dizini.</span><span class="sxs-lookup"><span data-stu-id="340dc-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="340dc-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="340dc-231">Çıkış klasörüne eklemek üzerine deyimi için.</span><span class="sxs-lookup"><span data-stu-id="340dc-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="340dc-232">${hiveTableName}</span></span></td><td><span data-ttu-id="340dc-233">Log4j veri dosyalarına başvuran Hive tablosu adı.</span><span class="sxs-lookup"><span data-stu-id="340dc-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="340dc-234">Sqoop eylem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="340dc-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="340dc-235">Sqoop eylem değişkeni</span><span class="sxs-lookup"><span data-stu-id="340dc-235">Sqoop action variable</span></span></th><th><span data-ttu-id="340dc-236">Açıklama</span><span class="sxs-lookup"><span data-stu-id="340dc-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="340dc-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="340dc-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="340dc-238">SQL veritabanı bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="340dc-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="340dc-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="340dc-240">Verileri dışarı burada için Azure SQL veritabanı tablosu.</span><span class="sxs-lookup"><span data-stu-id="340dc-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="340dc-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="340dc-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="340dc-242">Çıkış klasörüne Hive Ekle üzerine deyimi için.</span><span class="sxs-lookup"><span data-stu-id="340dc-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="340dc-243">Bu Sqoop verme (verme-dir) için aynı klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="340dc-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="340dc-244">Oozie iş akışı ve iş akışı eylemlerinin kullanma hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (için Hdınsight kümesi sürüm 3.0) veya [Apache Oozie 3.3.2 belgeleri ] [ apache-oozie-332] (için Hdınsight kümesi sürüm 2.1).</span><span class="sxs-lookup"><span data-stu-id="340dc-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="340dc-245">Dosyayı Farklı Kaydet **C:\Tutorials\UseOozie\workflow.xml** ANSI (ASCII) kodlama kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="340dc-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="340dc-246">(Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.)</span><span class="sxs-lookup"><span data-stu-id="340dc-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="340dc-247">**Düzenleyici tanımlamak için**</span><span class="sxs-lookup"><span data-stu-id="340dc-247">**To define coordinator**</span></span>

1. <span data-ttu-id="340dc-248">Aşağıdaki içerik ile bir metin dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="340dc-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="340dc-249">Tanım dosyasında kullanılan beş değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="340dc-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="340dc-250">Değişken</span><span class="sxs-lookup"><span data-stu-id="340dc-250">Variable</span></span> | <span data-ttu-id="340dc-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="340dc-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="340dc-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="340dc-252">${coordFrequency}</span></span> |<span data-ttu-id="340dc-253">İş duraklatma süresi.</span><span class="sxs-lookup"><span data-stu-id="340dc-253">Job pause time.</span></span> <span data-ttu-id="340dc-254">Sıklık, her zaman dakika cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="340dc-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="340dc-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="340dc-255">${coordStart}</span></span> |<span data-ttu-id="340dc-256">İş başlangıç zamanı.</span><span class="sxs-lookup"><span data-stu-id="340dc-256">Job start time.</span></span> |
   | <span data-ttu-id="340dc-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="340dc-257">${coordEnd}</span></span> |<span data-ttu-id="340dc-258">İş bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="340dc-258">Job end time.</span></span> |
   | <span data-ttu-id="340dc-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="340dc-259">${coordTimezone}</span></span> |<span data-ttu-id="340dc-260">Oozie Düzenleyicisi işleri sabit bir saat diliminde hiçbir gün ışığından yararlanma saati (UTC kullanarak tipik olarak gösterilir) ile işler.</span><span class="sxs-lookup"><span data-stu-id="340dc-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="340dc-261">Bu saat dilimi "Oozie işleme saat dilimi." olarak adlandırılır</span><span class="sxs-lookup"><span data-stu-id="340dc-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="340dc-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="340dc-262">${wfPath}</span></span> |<span data-ttu-id="340dc-263">Workflow.xml yolu.</span><span class="sxs-lookup"><span data-stu-id="340dc-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="340dc-264">İş akışı dosyası adı varsayılan dosya adı (workflow.xml) değilse, belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="340dc-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="340dc-265">Dosyayı Farklı Kaydet **C:\Tutorials\UseOozie\coordinator.xml** ANSI (ASCII) kodlama kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="340dc-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="340dc-266">(Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.)</span><span class="sxs-lookup"><span data-stu-id="340dc-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="340dc-267">Oozie projeyi dağıtın ve öğretici hazırlama</span><span class="sxs-lookup"><span data-stu-id="340dc-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="340dc-268">Aşağıdakileri gerçekleştirmek üzere bir Azure PowerShell komut dosyası çalışır:</span><span class="sxs-lookup"><span data-stu-id="340dc-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="340dc-269">Azure Blob depolama alanına HiveQL betiğini (useoozie.hql) kopyalama wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="340dc-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="340dc-270">Workflow.XML için wasb:///tutorials/useoozie/workflow.xml kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="340dc-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="340dc-271">Coordinator.XML için wasb:///tutorials/useoozie/coordinator.xml kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="340dc-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="340dc-272">Veri dosyasını kopyalayın (/ example/data/sample.log) wasb:///tutorials/useoozie/data/sample.log için.</span><span class="sxs-lookup"><span data-stu-id="340dc-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="340dc-273">Sqoop verme verileri depolamak için bir Azure SQL veritabanı tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="340dc-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="340dc-274">Tablo adı *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="340dc-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="340dc-275">**Hdınsight depolama anlama**</span><span class="sxs-lookup"><span data-stu-id="340dc-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="340dc-276">Hdınsight Azure Blob Depolama, veri depolaması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="340dc-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="340dc-277">wasb: / / Azure Blob depolamada Hadoop dağıtılmış dosya sistemi (HDFS) Microsoft uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="340dc-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="340dc-278">Daha fazla bilgi için bkz: [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="340dc-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="340dc-279">Hdınsight kümesi sağladığınızda, Azure Blob Depolama hesabı ve bu hesaptan belirli bir kapsayıcıya tasarlanmış varsayılan dosya sistemi olarak gibi HDFS'de.</span><span class="sxs-lookup"><span data-stu-id="340dc-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="340dc-280">Bu depolama hesabına ek olarak, ek depolama hesapları aynı Azure aboneliğinden veya farklı Azure aboneliklerinden sağlama işlemi sırasında ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="340dc-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="340dc-281">Ek depolama hesapları ekleme hakkında yönergeler için bkz: [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="340dc-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="340dc-282">Bu öğreticide kullanılan Azure PowerShell Betiği basitleştirmek için tüm dosyaları konumunda bulunan varsayılan dosya sistemi kapsayıcısında depolanır */öğreticileri/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="340dc-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="340dc-283">Varsayılan olarak, bu kapsayıcı Hdınsight küme adı ile aynı ada sahiptir.</span><span class="sxs-lookup"><span data-stu-id="340dc-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="340dc-284">Söz dizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="340dc-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="340dc-285">Yalnızca *wasb: / /* söz dizimi Hdınsight kümesi sürüm 3.0 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="340dc-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="340dc-286">Eski *asv: / /* söz dizimi Hdınsight 2.1 ve 1.6 kümeleri desteklenir, ancak Hdınsight 3.0 kümelerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="340dc-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="340dc-287">Wasb: / / yolu olan bir sanal yol.</span><span class="sxs-lookup"><span data-stu-id="340dc-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="340dc-288">Daha fazla bilgi için bkz: [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="340dc-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="340dc-289">Varsayılan dosya sistemi kapsayıcısında depolanır bir dosya (workflow.xml örnek olarak kullanıyorum) aşağıdaki URI'ler birini kullanarak Hdınsight'ta erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="340dc-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="340dc-290">Dosyayı doğrudan depolama hesabından erişmek isterseniz, blob dosya adıdır:</span><span class="sxs-lookup"><span data-stu-id="340dc-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="340dc-291">**Hive iç ve dış tablolar anlama**</span><span class="sxs-lookup"><span data-stu-id="340dc-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="340dc-292">Hive iç ve dış tablolar hakkında bilmeniz gereken birkaç şey vardır:</span><span class="sxs-lookup"><span data-stu-id="340dc-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="340dc-293">CREATE TABLE komutu bir iç tablosu olarak da bilinen yönetilen bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="340dc-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="340dc-294">Veri dosyası varsayılan kapsayıcısında bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="340dc-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="340dc-295">CREATE TABLE komutu veri dosyası /hive/ambarı/için taşır<TableName> varsayılan kapsayıcı klasöründe.</span><span class="sxs-lookup"><span data-stu-id="340dc-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="340dc-296">Dış tablo oluşturma komut bir dış tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="340dc-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="340dc-297">Veri dosyasındaki varsayılan kapsayıcı bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="340dc-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="340dc-298">Dış Tablo Oluştur komutu veri dosyasını taşımaz.</span><span class="sxs-lookup"><span data-stu-id="340dc-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="340dc-299">Dış tablo oluşturma komut konumu yan tümcesinde belirtilen klasör altındaki tüm alt izin vermez.</span><span class="sxs-lookup"><span data-stu-id="340dc-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="340dc-300">Bu öğretici sample.log dosyasının bir kopyasını neden yapar nedenidir.</span><span class="sxs-lookup"><span data-stu-id="340dc-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="340dc-301">Daha fazla bilgi için bkz: [Hdınsight: Hive iç ve dış tablolar giriş][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="340dc-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="340dc-302">**Öğretici hazırlamak için**</span><span class="sxs-lookup"><span data-stu-id="340dc-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="340dc-303">Windows PowerShell ISE açın (Windows 8 Başlat ekranında, yazın **PowerShell_ISE**ve ardından **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="340dc-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="340dc-304">Daha fazla bilgi için bkz: [Başlat Windows PowerShell Windows 8 ve Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="340dc-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="340dc-305">Alt bölmede Azure aboneliğinize bağlanmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="340dc-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="340dc-306">Azure hesabı kimlik bilgilerinizi girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="340dc-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="340dc-307">Bu yöntem bir abonelik bağlantısı ekleme zaman aşımına uğrayıp 12 saat sonra cmdlet'ini yeniden çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="340dc-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="340dc-308">Birden çok Azure aboneliğiniz varsa ve varsayılan abonelik kullanmak için kullanmak istediğiniz değil <strong>Select-AzureSubscription</strong> cmdlet'ini bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="340dc-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="340dc-309">Betik bölmesine aşağıdaki betiği kopyalayın ve ilk altı değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="340dc-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="340dc-310">Değişkenleri daha fazla açıklamaları için bkz: [Önkoşullar](#prerequisites) Bu öğretici bölümünde.</span><span class="sxs-lookup"><span data-stu-id="340dc-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="340dc-311">Aşağıdaki betik bölmesine komut dosyası Ekle:</span><span class="sxs-lookup"><span data-stu-id="340dc-311">Append the following to the script in the script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create the log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="340dc-312">Tıklatın **komut dosyasını Çalıştır** veya basın **F5** komut dosyasını çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="340dc-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="340dc-313">Çıktı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="340dc-313">The output will be similar to:</span></span>

    ![Eğitmen hazırlık çıktı][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="340dc-315">Oozie projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="340dc-315">Run the Oozie project</span></span>
<span data-ttu-id="340dc-316">Azure PowerShell cmdlet'lerin Oozie işleri tanımlamak için şu anda sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="340dc-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="340dc-317">Kullanabileceğiniz **Invoke-RestMethod** cmdlet'ini Oozie web hizmetlerini çağırır.</span><span class="sxs-lookup"><span data-stu-id="340dc-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="340dc-318">Oozie web hizmetleri API'si bir HTTP REST JSON API'dir.</span><span class="sxs-lookup"><span data-stu-id="340dc-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="340dc-319">Oozie web hizmetleri API'si hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (için Hdınsight kümesi sürüm 3.0) veya [Apache Oozie 3.3.2 belgelerine] [ apache-oozie-332] (için Hdınsight kümesi sürüm 2.1).</span><span class="sxs-lookup"><span data-stu-id="340dc-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="340dc-320">**Oozie işi göndermek için**</span><span class="sxs-lookup"><span data-stu-id="340dc-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="340dc-321">Windows PowerShell ISE açın (Windows 8 Başlat ekranında, yazın **PowerShell_ISE**ve ardından **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="340dc-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="340dc-322">Daha fazla bilgi için bkz: [Başlat Windows PowerShell Windows 8 ve Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="340dc-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="340dc-323">Betik bölmesine aşağıdaki betiği kopyalayın ve bu ilk on dört değişkenleri ayarlayın (ancak, atla **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="340dc-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="340dc-324">Değişkenleri daha fazla açıklamaları için bkz: [Önkoşullar](#prerequisites) Bu öğretici bölümünde.</span><span class="sxs-lookup"><span data-stu-id="340dc-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="340dc-325">$coordstart ve $coordend başlangıç ve bitiş saati iş akışı ' dir.</span><span class="sxs-lookup"><span data-stu-id="340dc-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="340dc-326">UTC/GMT zaman aşımına uğrar bulmak için "utc saati" aratıp arayın. $CoordFrequency, iş akışını çalıştırmak istediğiniz sıklıkta dakikadır.</span><span class="sxs-lookup"><span data-stu-id="340dc-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="340dc-327">Aşağıdaki komut dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="340dc-327">Append the following to the script.</span></span> <span data-ttu-id="340dc-328">Bu bölümü Oozie yükünü tanımlar:</span><span class="sxs-lookup"><span data-stu-id="340dc-328">This part defines the Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
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
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
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
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="340dc-329">İş akışı gönderme yükü dosyasına göre en önemli fark değişkenidir **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="340dc-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="340dc-330">İş akışının gönderdiğinizde, kullandığınız **oozie.wf.application.path** yerine.</span><span class="sxs-lookup"><span data-stu-id="340dc-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="340dc-331">Aşağıdaki komut dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="340dc-331">Append the following to the script.</span></span> <span data-ttu-id="340dc-332">Bu bölümü Oozie web hizmetinin durumunu denetler:</span><span class="sxs-lookup"><span data-stu-id="340dc-332">This part checks the Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="340dc-333">Aşağıdaki komut dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="340dc-333">Append the following to the script.</span></span> <span data-ttu-id="340dc-334">Bu bölümü Oozie işi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="340dc-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="340dc-335">İş akışının gönderdiğinizde, işi oluşturulduktan sonra işini başlatmak için çağrısı başka bir web hizmeti olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="340dc-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="340dc-336">Bu durumda, düzenleyici işi zaman tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="340dc-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="340dc-337">İş otomatik olarak başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="340dc-337">The job will start automatically.</span></span>

6. <span data-ttu-id="340dc-338">Aşağıdaki komut dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="340dc-338">Append the following to the script.</span></span> <span data-ttu-id="340dc-339">Bu bölümü Oozie iş durumunu denetler:</span><span class="sxs-lookup"><span data-stu-id="340dc-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="340dc-340">(İsteğe bağlı) Aşağıdaki komut dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="340dc-340">(Optional) Append the following to the script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="340dc-341">Aşağıdaki komut dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="340dc-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="340dc-342">Ek işlevler çalıştırmak istiyorsanız # işareti kaldırın.</span><span class="sxs-lookup"><span data-stu-id="340dc-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="340dc-343">Hdınsight kümesi sürüm 2.1 ise "https://$clusterName.azurehdinsight.net:443/oozie/v2/" "https://$clusterName.azurehdinsight.net:443/oozie/v1/" ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="340dc-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="340dc-344">Hdınsight kümesi sürüm 2.1 değil destekler 2 web hizmetlerini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="340dc-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="340dc-345">Tıklatın **komut dosyasını Çalıştır** veya basın **F5** komut dosyasını çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="340dc-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="340dc-346">Çıktı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="340dc-346">The output will be similar to:</span></span>

     ![İş akışı çıkış öğreticisini çalıştırma][img-runworkflow-output]
11. <span data-ttu-id="340dc-348">Dışarı aktarılan verileri görmek için SQL veritabanına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="340dc-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="340dc-349">**İş hata günlüğü denetlemek için**</span><span class="sxs-lookup"><span data-stu-id="340dc-349">**To check the job error log**</span></span>

<span data-ttu-id="340dc-350">Bir iş akışı gidermek için Oozie günlük dosyası C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log küme headnode bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="340dc-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="340dc-351">RDP hakkında daha fazla bilgi için bkz: [Azure Portalı'nı kullanarak yönetme Hdınsight kümelerini][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="340dc-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="340dc-352">**Öğreticiyi yeniden çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="340dc-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="340dc-353">İş akışını yeniden çalıştırmak için aşağıdaki görevleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="340dc-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="340dc-354">Hive betiği çıktı dosyasını silin.</span><span class="sxs-lookup"><span data-stu-id="340dc-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="340dc-355">Log4jLogsCount tablodaki verileri silin.</span><span class="sxs-lookup"><span data-stu-id="340dc-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="340dc-356">Kullanabileceğiniz örnek Windows PowerShell betiğini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="340dc-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="340dc-357">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="340dc-357">Next steps</span></span>
<span data-ttu-id="340dc-358">Bu öğreticide, Oozie iş akışı ve Oozie Düzenleyicisi nasıl tanımlanacağı ve Azure PowerShell kullanarak bir Oozie Düzenleyicisi işi çalıştırmak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="340dc-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="340dc-359">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="340dc-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="340dc-360">[Hdınsight kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="340dc-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="340dc-361">[Hdınsight ile Azure Blob storage kullanma][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="340dc-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="340dc-362">[Hdınsight Azure PowerShell kullanarak yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="340dc-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="340dc-363">[HDInsight'a veri yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="340dc-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="340dc-364">[Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="340dc-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="340dc-365">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="340dc-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="340dc-366">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="340dc-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="340dc-367">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="340dc-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
