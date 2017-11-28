---
title: "aaaUse hdınsight'ta Hadoop Oozie Düzenleyicisi zamana dayalı | Microsoft Docs"
description: "Hdınsight, büyük veri hizmeti zamana dayalı Hadoop Oozie düzenleyicisi kullanın. Bilgi nasıl toodefine Oozie iş akışları ve düzenleyicileri ve işleri göndermek."
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
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="c080b-104">Hdınsight toodefine akışlarında Hadoop ile zamana dayalı Oozie düzenleyicisi kullanın ve işleri koordine</span><span class="sxs-lookup"><span data-stu-id="c080b-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="c080b-105">Bu makalede, nasıl toodefine iş akışları ve düzenleyiciler ve nasıl tootrigger hello Düzenleyicisi işleri, zamana dayalı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c080b-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="c080b-106">Aracılığıyla yararlı toogo olan [Hdınsight ile kullanım Oozie] [ hdinsight-use-oozie] önce bu makaleyi okuyun.</span><span class="sxs-lookup"><span data-stu-id="c080b-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="c080b-107">Ayrıca tooOozie, Azure Data Factory kullanarak işleri de zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c080b-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="c080b-108">Azure Data Factory toolearn bkz [kullanım Pig ve Hive Data Factory ile](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c080b-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c080b-109">Bu makalede Windows tabanlı Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c080b-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="c080b-110">Oozie, Linux tabanlı bir kümede zaman tabanlı işleri de dahil olmak üzere kullanma hakkında bilgi için bkz: [kullanım Oozie Hadoop toodefine ve Linux tabanlı Hdınsight üzerinde bir iş akışını çalıştırma](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="c080b-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="c080b-111">Oozie nedir</span><span class="sxs-lookup"><span data-stu-id="c080b-111">What is Oozie</span></span>
<span data-ttu-id="c080b-112">Apache Oozie, Hadoop işlerini yöneten bir iş akışı/koordinasyon sistemidir.</span><span class="sxs-lookup"><span data-stu-id="c080b-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="c080b-113">Merhaba Hadoop yığını ile tümleştirilir ve Apache MapReduce, Apache Pig, Apache Hive ve Apache Sqoop için Hadoop işlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="c080b-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="c080b-114">Ayrıca, Java programları veya kabuk betikleri gibi belirli tooa sistem kullanılan tooschedule işler de olabilir.</span><span class="sxs-lookup"><span data-stu-id="c080b-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="c080b-115">Merhaba aşağıdaki resimde, gerçekleştireceksiniz hello iş akışı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c080b-115">hello following image shows hello workflow you will implement:</span></span>

![İş akışı diyagramı][img-workflow-diagram]

<span data-ttu-id="c080b-117">Merhaba iş akışı iki eylemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c080b-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="c080b-118">Bir Hive eylem HiveQL betiğini toocount hello log4j günlük dosyasına günlük düzeyi türlerinin oluşumları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="c080b-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="c080b-119">Her log4j günlük bir [günlük düzeyi] alan tooshow hello türü ve hello önem derecesi, örneğin içeren bir dizi alanlarının oluşur:</span><span class="sxs-lookup"><span data-stu-id="c080b-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="c080b-120">Merhaba Hive betik çıktısı benzer:</span><span class="sxs-lookup"><span data-stu-id="c080b-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="c080b-121">Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="c080b-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="c080b-122">Sqoop eylemin hello HiveQL eylem çıktı tooa tablosu bir Azure SQL veritabanında dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="c080b-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="c080b-123">Sqoop hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="c080b-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="c080b-124">Hdınsight kümelerinde desteklenen Oozie sürümleri için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler nelerdir?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="c080b-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="c080b-125">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c080b-125">Prerequisites</span></span>
<span data-ttu-id="c080b-126">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c080b-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c080b-127">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="c080b-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c080b-128">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışıdır** ve 1 Ocak 2017 tarihine kadar kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="c080b-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="c080b-129">Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="c080b-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="c080b-130">Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="c080b-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="c080b-131">Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c080b-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="c080b-132">**Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="c080b-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="c080b-133">Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight kümeleri oluşturma][hdinsight-provision], veya [Hdınsight kullanmaya başlama][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="c080b-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="c080b-134">Başlangıç Öğreticisi aracılığıyla veri toogo aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c080b-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c080b-135">Küme özelliği</span><span class="sxs-lookup"><span data-stu-id="c080b-135">Cluster property</span></span></th><th><span data-ttu-id="c080b-136">Windows PowerShell değişken adı</span><span class="sxs-lookup"><span data-stu-id="c080b-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="c080b-137">Değer</span><span class="sxs-lookup"><span data-stu-id="c080b-137">Value</span></span></th><th><span data-ttu-id="c080b-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c080b-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c080b-139">Hdınsight küme adı</span><span class="sxs-lookup"><span data-stu-id="c080b-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="c080b-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="c080b-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="c080b-141">Bu öğretici çalışacağı hello Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="c080b-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-142">Hdınsight küme kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c080b-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="c080b-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="c080b-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="c080b-144">Merhaba Hdınsight küme kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="c080b-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="c080b-145">Hdınsight küme kullanıcı parolası</span><span class="sxs-lookup"><span data-stu-id="c080b-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="c080b-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="c080b-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="c080b-147">Merhaba Hdınsight küme kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="c080b-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-148">Azure depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="c080b-148">Azure storage account name</span></span></td><td><span data-ttu-id="c080b-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="c080b-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="c080b-150">Azure depolama hesabı kullanılabilir toohello Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="c080b-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="c080b-151">Bu öğretici için hello küme sağlama işlemi sırasında belirtilen hello varsayılan depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c080b-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-152">Azure Blob kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="c080b-152">Azure Blob container name</span></span></td><td><span data-ttu-id="c080b-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="c080b-153">$containerName</span></span></td><td></td><td><span data-ttu-id="c080b-154">Bu örnekte, hello varsayılan Hdınsight küme dosya sistemi için kullanılan hello Azure Blob Depolama kapsayıcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c080b-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="c080b-155">Varsayılan olarak, aynı hello Hdınsight kümesi olarak ad hello içeriyor.</span><span class="sxs-lookup"><span data-stu-id="c080b-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="c080b-156">
* **Bir Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="c080b-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="c080b-157">Merhaba SQL veritabanı sunucusu tooallow erişimi için bir güvenlik duvarı kuralı istasyonunuzdan yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c080b-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="c080b-158">Bir Azure SQL veritabanı oluşturma ve hello güvenlik duvarını yapılandırma hakkında yönergeler için bkz. [Azure SQL veritabanı ile çalışmaya başlamak] [sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="c080b-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="c080b-159">Bu makalede, Bu öğretici için gereksinim duyduğunuz hello Azure SQL veritabanı tablosu oluşturmak için bir Windows PowerShell komut dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="c080b-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c080b-160">SQL veritabanı özelliği</span><span class="sxs-lookup"><span data-stu-id="c080b-160">SQL database property</span></span></th><th><span data-ttu-id="c080b-161">Windows PowerShell değişken adı</span><span class="sxs-lookup"><span data-stu-id="c080b-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="c080b-162">Değer</span><span class="sxs-lookup"><span data-stu-id="c080b-162">Value</span></span></th><th><span data-ttu-id="c080b-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c080b-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c080b-164">SQL veritabanı sunucusu adı</span><span class="sxs-lookup"><span data-stu-id="c080b-164">SQL database server name</span></span></td><td><span data-ttu-id="c080b-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="c080b-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="c080b-166">Merhaba SQL veritabanı sunucusu toowhich Sqoop veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="c080b-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="c080b-167">SQL veritabanı oturum açma adı</span><span class="sxs-lookup"><span data-stu-id="c080b-167">SQL database login name</span></span></td><td><span data-ttu-id="c080b-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="c080b-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="c080b-169">SQL veritabanı oturum açma adı.</span><span class="sxs-lookup"><span data-stu-id="c080b-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-170">SQL veritabanı oturum açma parolası</span><span class="sxs-lookup"><span data-stu-id="c080b-170">SQL database login password</span></span></td><td><span data-ttu-id="c080b-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="c080b-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="c080b-172">SQL veritabanı oturum açma parolası.</span><span class="sxs-lookup"><span data-stu-id="c080b-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-173">SQL veritabanı adı</span><span class="sxs-lookup"><span data-stu-id="c080b-173">SQL database name</span></span></td><td><span data-ttu-id="c080b-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="c080b-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="c080b-175">Hello Azure SQL veritabanı toowhich Sqoop veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="c080b-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="c080b-176">Varsayılan olarak, Azure Hdınsight gibi Azure hizmetlerinden bağlantıları bir Azure SQL veritabanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c080b-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="c080b-177">Bu güvenlik duvarı ayarı devre dışıysa, hello Azure Portalı ' etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c080b-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="c080b-178">Bir SQL veritabanı oluşturma ve güvenlik duvarı kuralları yapılandırma hakkında daha fazla yönerge için bkz: [oluşturma ve yapılandırma SQL veritabanı][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="c080b-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="c080b-179">Merhaba tablolardaki doldurma hello değerleri.</span><span class="sxs-lookup"><span data-stu-id="c080b-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="c080b-180">Bu öğreticide olmaya yardımcı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c080b-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="c080b-181">Merhaba HiveQL betiğini ilgili ve Oozie iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="c080b-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="c080b-182">Oozie iş akışı tanımları hPDL (bir XML işlem tanım dili) yazılır.</span><span class="sxs-lookup"><span data-stu-id="c080b-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="c080b-183">Merhaba varsayılan iş akışı dosya adı *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="c080b-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="c080b-184">Merhaba iş akışı dosyasını yerel olarak kaydedin ve ardından daha sonra Bu öğreticide Azure PowerShell kullanarak toohello Hdınsight kümesi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c080b-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="c080b-185">Merhaba Hive eylemin hello iş akışında bir HiveQL komut dosyasını çağırır.</span><span class="sxs-lookup"><span data-stu-id="c080b-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="c080b-186">Bu komut dosyasını üç HiveQL ifadelerini içerir:</span><span class="sxs-lookup"><span data-stu-id="c080b-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="c080b-187">**Merhaba DROP TABLE deyimi** siler hello log4j Hive tablosu varsa.</span><span class="sxs-lookup"><span data-stu-id="c080b-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="c080b-188">**Merhaba CREATE TABLE deyimi** toohello günlük dosyasının konumu hello log4j; gösteren bir log4j Hive dış tablo oluşturur</span><span class="sxs-lookup"><span data-stu-id="c080b-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="c080b-189">**Merhaba hello log4j günlük dosyasının konumunu**.</span><span class="sxs-lookup"><span data-stu-id="c080b-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="c080b-190">Merhaba alan sınırlayıcı ",".</span><span class="sxs-lookup"><span data-stu-id="c080b-190">hello field delimiter is ",".</span></span> <span data-ttu-id="c080b-191">Merhaba varsayılan satır ayırıcı "\n" dir.</span><span class="sxs-lookup"><span data-stu-id="c080b-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="c080b-192">Birden çok kez toorun hello Oozie iş akışı istemeniz durumunda Hive dış tablo hello özgün konumundan kaldırılmakta kullanılan tooavoid hello veri dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c080b-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="c080b-193">**Merhaba Ekle üzerine deyimi** her günlük düzeyi türünden hello oluşumlarını sayar log4j Hive tablosu hello ve hello çıkış tooan Azure Blob Depolama konumu kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c080b-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="c080b-194">Bilinen bir Hive yolu sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="c080b-194">There is a known Hive path issue.</span></span> <span data-ttu-id="c080b-195">Bu sorunla Oozie iş gönderirken çalışır.</span><span class="sxs-lookup"><span data-stu-id="c080b-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="c080b-196">Merhaba yönergeleri hello sorunu düzeltme hello TechNet Wiki üzerinde bulunabilir: [Hdınsight Hive hata: oluşturulamıyor toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="c080b-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="c080b-197">**Merhaba akışı tarafından çağırılan toodefine hello HiveQL komut dosyası toobe**</span><span class="sxs-lookup"><span data-stu-id="c080b-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="c080b-198">Bir metin dosyası aşağıdaki hello ile içerik oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c080b-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="c080b-199">Merhaba komut dosyasında kullanılan üç değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c080b-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="c080b-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="c080b-200">${hiveTableName}</span></span>
   * <span data-ttu-id="c080b-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="c080b-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="c080b-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="c080b-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="c080b-203">Merhaba iş akışı tanımı dosyası (Bu öğreticide workflow.xml) bu değerleri toothis HiveQL betiğini çalışma zamanında geçer.</span><span class="sxs-lookup"><span data-stu-id="c080b-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="c080b-204">Merhaba dosyası olarak kaydetmeniz **C:\Tutorials\UseOozie\useooziewf.hql** ANSI (ASCII) kodlama kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="c080b-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="c080b-205">(Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.) Bu komut dosyası dağıtılan toohello Hdınsight kümesi daha sonra hello öğreticide olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c080b-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="c080b-206">**toodefine bir iş akışı**</span><span class="sxs-lookup"><span data-stu-id="c080b-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="c080b-207">Bir metin dosyası aşağıdaki hello ile içerik oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c080b-207">Create a text file with hello following content:</span></span>

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

    <span data-ttu-id="c080b-208">Merhaba iş akışında tanımlanan iki eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="c080b-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="c080b-209">Merhaba start-tooaction olan *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="c080b-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="c080b-210">Merhaba eylem çalıştırıyorsa *Tamam*, hello İleri eylem *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="c080b-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="c080b-211">Merhaba RunHiveScript birkaç değişkeni yok.</span><span class="sxs-lookup"><span data-stu-id="c080b-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="c080b-212">Azure PowerShell kullanarak hello Oozie iş istasyonunuzdan gönderdiğinizde hello değerler geçer.</span><span class="sxs-lookup"><span data-stu-id="c080b-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="c080b-213">İş akışı değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c080b-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c080b-214">İş akışı değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c080b-214">Workflow variables</span></span></th><th><span data-ttu-id="c080b-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c080b-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c080b-216">${Jobtracker'a}</span><span class="sxs-lookup"><span data-stu-id="c080b-216">${jobTracker}</span></span></td><td><span data-ttu-id="c080b-217">Merhaba Hadoop işi İzleyicisi Merhaba URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c080b-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="c080b-218">Kullanım <strong>jobtrackerhost:9010</strong> Hdınsight sürüm 3.0 ve 2.0 küme.</span><span class="sxs-lookup"><span data-stu-id="c080b-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-219">${İş}</span><span class="sxs-lookup"><span data-stu-id="c080b-219">${nameNode}</span></span></td><td><span data-ttu-id="c080b-220">Merhaba Hadoop adı düğümü Hello URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c080b-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="c080b-221">Merhaba varsayılan dosya sistemi wasb kullanın: / / adres, örneğin, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="c080b-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="c080b-222">${queueName}</span></span></td><td><span data-ttu-id="c080b-223">İş hello hello sıra adı için gönderilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="c080b-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="c080b-224">Kullanım <strong>varsayılan</strong>.</span><span class="sxs-lookup"><span data-stu-id="c080b-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="c080b-225">Hive eylem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c080b-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c080b-226">Eylem değişkeni yığını</span><span class="sxs-lookup"><span data-stu-id="c080b-226">Hive action variable</span></span></th><th><span data-ttu-id="c080b-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c080b-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c080b-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="c080b-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="c080b-229">Merhaba Hive Create Table komutu için kaynak dizini Hello.</span><span class="sxs-lookup"><span data-stu-id="c080b-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="c080b-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="c080b-231">Merhaba Ekle üzerine deyimi için Hello çıkış klasörü.</span><span class="sxs-lookup"><span data-stu-id="c080b-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="c080b-232">${hiveTableName}</span></span></td><td><span data-ttu-id="c080b-233">Merhaba log4j veri dosyalarına başvuran hello Hive tablosu Hello adı.</span><span class="sxs-lookup"><span data-stu-id="c080b-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="c080b-234">Sqoop eylem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c080b-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c080b-235">Sqoop eylem değişkeni</span><span class="sxs-lookup"><span data-stu-id="c080b-235">Sqoop action variable</span></span></th><th><span data-ttu-id="c080b-236">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c080b-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c080b-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="c080b-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="c080b-238">SQL veritabanı bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="c080b-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="c080b-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="c080b-240">Hello Azure SQL veritabanı tablosu toowhere hello verileri dışarı aktarılır.</span><span class="sxs-lookup"><span data-stu-id="c080b-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="c080b-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="c080b-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="c080b-242">Merhaba Hive Ekle üzerine deyimi için Hello çıkış klasörü.</span><span class="sxs-lookup"><span data-stu-id="c080b-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="c080b-243">Merhaba budur aynı klasöre hello Sqoop verme (verme-dir).</span><span class="sxs-lookup"><span data-stu-id="c080b-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="c080b-244">Oozie iş akışı ve hello iş akışı eylemlerinin kullanma hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (için Hdınsight kümesi sürüm 3.0) veya [Apache Oozie 3.3.2 Belge] [ apache-oozie-332] (için Hdınsight kümesi sürüm 2.1).</span><span class="sxs-lookup"><span data-stu-id="c080b-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="c080b-245">Merhaba dosyası olarak kaydetmeniz **C:\Tutorials\UseOozie\workflow.xml** ANSI (ASCII) kodlama kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="c080b-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="c080b-246">(Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.)</span><span class="sxs-lookup"><span data-stu-id="c080b-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="c080b-247">**toodefine Düzenleyicisi**</span><span class="sxs-lookup"><span data-stu-id="c080b-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="c080b-248">Bir metin dosyası aşağıdaki hello ile içerik oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c080b-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="c080b-249">Merhaba tanım dosyasında kullanılan beş değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c080b-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="c080b-250">Değişken</span><span class="sxs-lookup"><span data-stu-id="c080b-250">Variable</span></span> | <span data-ttu-id="c080b-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c080b-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="c080b-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="c080b-252">${coordFrequency}</span></span> |<span data-ttu-id="c080b-253">İş duraklatma süresi.</span><span class="sxs-lookup"><span data-stu-id="c080b-253">Job pause time.</span></span> <span data-ttu-id="c080b-254">Sıklık, her zaman dakika cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="c080b-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="c080b-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="c080b-255">${coordStart}</span></span> |<span data-ttu-id="c080b-256">İş başlangıç zamanı.</span><span class="sxs-lookup"><span data-stu-id="c080b-256">Job start time.</span></span> |
   | <span data-ttu-id="c080b-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="c080b-257">${coordEnd}</span></span> |<span data-ttu-id="c080b-258">İş bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="c080b-258">Job end time.</span></span> |
   | <span data-ttu-id="c080b-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="c080b-259">${coordTimezone}</span></span> |<span data-ttu-id="c080b-260">Oozie Düzenleyicisi işleri sabit bir saat diliminde hiçbir gün ışığından yararlanma saati (UTC kullanarak tipik olarak gösterilir) ile işler.</span><span class="sxs-lookup"><span data-stu-id="c080b-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="c080b-261">Bu saat dilimi hello "Oozie işleme saat dilimi." olarak adlandırılır</span><span class="sxs-lookup"><span data-stu-id="c080b-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="c080b-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="c080b-262">${wfPath}</span></span> |<span data-ttu-id="c080b-263">Merhaba workflow.xml Hello yolu.</span><span class="sxs-lookup"><span data-stu-id="c080b-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="c080b-264">Merhaba iş akışı dosyası adı hello varsayılan dosya adı (workflow.xml) değilse, belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c080b-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="c080b-265">Merhaba dosyası olarak kaydetmeniz **C:\Tutorials\UseOozie\coordinator.xml** ANSI (ASCII) hello kodlama kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="c080b-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="c080b-266">(Bu seçenek, metin düzenleyici sağlamıyorsa Notepad kullanın.)</span><span class="sxs-lookup"><span data-stu-id="c080b-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="c080b-267">Merhaba Oozie projesini dağıtma ve hello öğretici hazırlama</span><span class="sxs-lookup"><span data-stu-id="c080b-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="c080b-268">Bir Azure PowerShell komut dosyası tooperform hello aşağıdaki çalışır:</span><span class="sxs-lookup"><span data-stu-id="c080b-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="c080b-269">Kopya hello HiveQL betiğini (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="c080b-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="c080b-270">Workflow.XML toowasb:///tutorials/useoozie/workflow.xml kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c080b-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="c080b-271">Coordinator.XML toowasb:///tutorials/useoozie/coordinator.xml kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c080b-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="c080b-272">Kopya hello veri dosyası (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="c080b-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="c080b-273">Sqoop verme verileri depolamak için bir Azure SQL veritabanı tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c080b-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="c080b-274">Merhaba tablo adı *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="c080b-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="c080b-275">**Hdınsight depolama anlama**</span><span class="sxs-lookup"><span data-stu-id="c080b-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="c080b-276">Hdınsight Azure Blob Depolama, veri depolaması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c080b-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="c080b-277">wasb: / / Azure Blob depolamada hello Hadoop dağıtılmış dosya sistemi (HDFS) Microsoft uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="c080b-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="c080b-278">Daha fazla bilgi için bkz: [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="c080b-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="c080b-279">Hdınsight kümesi sağladığınızda, Azure Blob Depolama hesabı ve bu hesaptan belirli bir kapsayıcıya tasarlanmış hello varsayılan dosya sistemi olarak gibi HDFS'de.</span><span class="sxs-lookup"><span data-stu-id="c080b-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="c080b-280">Ayrıca toothis depolama hesabı, ek depolama hesapları hello aynı ekleyebileceğiniz Azure aboneliği ya da farklı Azure aboneliklerinden hello sağlama işlemi sırasında.</span><span class="sxs-lookup"><span data-stu-id="c080b-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="c080b-281">Ek depolama hesapları ekleme hakkında yönergeler için bkz: [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="c080b-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="c080b-282">Bu öğreticide kullanılan toosimplify hello Azure PowerShell Betiği, tüm dosyaları hello varsayılan dosya sistemi kapsayıcısında depolanır hello bulunan */öğreticileri/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="c080b-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="c080b-283">Varsayılan olarak, bu kapsayıcı hello aynı hello Hdınsight küme adı vardır.</span><span class="sxs-lookup"><span data-stu-id="c080b-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="c080b-284">Merhaba sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c080b-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="c080b-285">Yalnızca hello *wasb: / /* söz dizimi Hdınsight kümesi sürüm 3.0 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c080b-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="c080b-286">Merhaba eski *asv: / /* söz dizimi Hdınsight 2.1 ve 1.6 kümeleri desteklenir, ancak Hdınsight 3.0 kümelerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c080b-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="c080b-287">Merhaba wasb: / / yolu olan bir sanal yol.</span><span class="sxs-lookup"><span data-stu-id="c080b-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="c080b-288">Daha fazla bilgi için bkz: [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="c080b-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="c080b-289">Merhaba varsayılan dosya sistemi kapsayıcısında depolanır bir dosya (workflow.xml örnek olarak kullanıyorum) URI'ler aşağıdaki hello birini kullanarak Hdınsight'ta erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="c080b-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="c080b-290">Tooaccess hello dosyanın hello depolama hesabından doğrudan istiyorsanız hello blob hello dosya adıdır:</span><span class="sxs-lookup"><span data-stu-id="c080b-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="c080b-291">**Hive iç ve dış tablolar anlama**</span><span class="sxs-lookup"><span data-stu-id="c080b-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="c080b-292">Hive iç ve dış tablolar hakkında tooknow gereken birkaç nokta vardır:</span><span class="sxs-lookup"><span data-stu-id="c080b-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="c080b-293">Merhaba CREATE TABLE komutu bir iç tablosu olarak da bilinen yönetilen bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c080b-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="c080b-294">Merhaba veri dosyası hello varsayılan kapsayıcısında bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c080b-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="c080b-295">Merhaba CREATE TABLE komutu taşır hello veri toohello dosya / / ambarı/hive<TableName> hello varsayılan kapsayıcı klasöründe.</span><span class="sxs-lookup"><span data-stu-id="c080b-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="c080b-296">Merhaba dış tablo oluşturma komut bir dış tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c080b-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="c080b-297">Merhaba veri dosyası hello varsayılan kapsayıcı bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c080b-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="c080b-298">Merhaba dış tablo oluşturma komut hello veri dosyası taşımaz.</span><span class="sxs-lookup"><span data-stu-id="c080b-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="c080b-299">Merhaba dış tablo oluşturma komut hello konumu yan tümcesinde belirtilen hello klasörü altındaki tüm alt izin vermez.</span><span class="sxs-lookup"><span data-stu-id="c080b-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="c080b-300">Neden hello öğretici hello sample.log dosyasının bir kopyasını yapar hello nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="c080b-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="c080b-301">Daha fazla bilgi için bkz: [Hdınsight: Hive iç ve dış tablolar giriş][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="c080b-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="c080b-302">**tooprepare başlangıç Öğreticisi**</span><span class="sxs-lookup"><span data-stu-id="c080b-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="c080b-303">Açık hello Windows PowerShell ISE (Merhaba ekranında Windows 8 Başlat, yazın **PowerShell_ISE**ve ardından **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="c080b-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="c080b-304">Daha fazla bilgi için bkz: [Başlat Windows PowerShell Windows 8 ve Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="c080b-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="c080b-305">Merhaba alt bölmede komutu tooconnect tooyour Azure aboneliği aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c080b-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="c080b-306">Azure hesabı kimlik bilgileriniz istendiğinde tooenter olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c080b-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="c080b-307">Bu yöntem bir abonelik bağlantısı ekleme zaman aşımına uğradı ve 12 saat sonra toorun hello cmdlet'ini yeniden sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c080b-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c080b-308">Birden çok Azure aboneliğiniz varsa ve hello varsayılan abonelik hello toouse istediğiniz değil, hello kullan <strong>Select-AzureSubscription</strong> cmdlet tooselect bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="c080b-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="c080b-309">Merhaba betik bölmesine komut dosyası izleyen hello kopyalayın ve ardından hello ilk altı değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c080b-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

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

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="c080b-310">Merhaba hello değişkenleri daha fazla açıklamaları için bkz [Önkoşullar](#prerequisites) Bu öğretici bölümünde.</span><span class="sxs-lookup"><span data-stu-id="c080b-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="c080b-311">Toohello betik hello betik bölmesinde aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c080b-311">Append hello following toohello script in hello script pane:</span></span>

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
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
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

        #Create hello log4jLogsCount table
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

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="c080b-312">Tıklatın **komut dosyasını Çalıştır** veya basın **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="c080b-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="c080b-313">Merhaba çıktı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="c080b-313">hello output will be similar to:</span></span>

    ![Eğitmen hazırlık çıktı][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="c080b-315">Merhaba Oozie projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c080b-315">Run hello Oozie project</span></span>
<span data-ttu-id="c080b-316">Azure PowerShell cmdlet'lerin Oozie işleri tanımlamak için şu anda sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="c080b-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="c080b-317">Merhaba kullanabilirsiniz **Invoke-RestMethod** cmdlet tooinvoke Oozie web hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="c080b-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="c080b-318">bir HTTP REST JSON API Hello Oozie web hizmetleri API'si var.</span><span class="sxs-lookup"><span data-stu-id="c080b-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="c080b-319">Merhaba Oozie web hizmetleri API'si hakkında daha fazla bilgi için bkz: [Apache Oozie 4.0 belgelerine] [ apache-oozie-400] (için Hdınsight kümesi sürüm 3.0) veya [Apache Oozie 3.3.2 belgelerine] [ apache-oozie-332] (için Hdınsight kümesi sürüm 2.1).</span><span class="sxs-lookup"><span data-stu-id="c080b-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="c080b-320">**toosubmit Oozie işi**</span><span class="sxs-lookup"><span data-stu-id="c080b-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="c080b-321">Açık hello Windows PowerShell ISE (Windows 8 Başlat ekranında, yazın **PowerShell_ISE**ve ardından **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="c080b-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="c080b-322">Daha fazla bilgi için bkz: [Başlat Windows PowerShell Windows 8 ve Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="c080b-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="c080b-323">Kopya hello aşağıdaki betiği hello betik bölmesine ve ardından kümesi hello ilk on dört değişkenleri (ancak, atla **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="c080b-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
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

    <span data-ttu-id="c080b-324">Merhaba hello değişkenleri daha fazla açıklamaları için bkz [Önkoşullar](#prerequisites) Bu öğretici bölümünde.</span><span class="sxs-lookup"><span data-stu-id="c080b-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="c080b-325">$coordstart ve $coordend hello iş akışı başlangıç ve bitiş saati ' dir.</span><span class="sxs-lookup"><span data-stu-id="c080b-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="c080b-326">toofind hello UTC/GMT zaman aşımına uğrar aratıp "utc saat" araması yapın. Merhaba $coordFrequency toorun hello iş akışının istediğiniz sıklıkta dakikadır.</span><span class="sxs-lookup"><span data-stu-id="c080b-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="c080b-327">Toohello komut dosyası izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c080b-327">Append hello following toohello script.</span></span> <span data-ttu-id="c080b-328">Bu bölümü hello Oozie yükünü tanımlar:</span><span class="sxs-lookup"><span data-stu-id="c080b-328">This part defines hello Oozie payload:</span></span>

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
   > <span data-ttu-id="c080b-329">Merhaba kıyasla önemli fark toohello iş akışı gönderme yükü dosyası hello değişkenidir **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="c080b-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="c080b-330">İş akışının gönderdiğinizde, kullandığınız **oozie.wf.application.path** yerine.</span><span class="sxs-lookup"><span data-stu-id="c080b-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="c080b-331">Toohello komut dosyası izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c080b-331">Append hello following toohello script.</span></span> <span data-ttu-id="c080b-332">Bu bölümü hello Oozie web hizmetinin durumunu denetler:</span><span class="sxs-lookup"><span data-stu-id="c080b-332">This part checks hello Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="c080b-333">Toohello komut dosyası izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c080b-333">Append hello following toohello script.</span></span> <span data-ttu-id="c080b-334">Bu bölümü Oozie işi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c080b-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="c080b-335">İş akışının gönderdiğinizde hello işi oluşturulduktan sonra başka bir web hizmeti çağrısı toostart hello işi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c080b-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="c080b-336">Bu durumda, hello Düzenleyicisi işi zaman tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="c080b-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="c080b-337">Merhaba iş otomatik olarak başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="c080b-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="c080b-338">Toohello komut dosyası izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c080b-338">Append hello following toohello script.</span></span> <span data-ttu-id="c080b-339">Bu bölümü hello Oozie iş durumunu denetler:</span><span class="sxs-lookup"><span data-stu-id="c080b-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
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

7. <span data-ttu-id="c080b-340">(İsteğe bağlı) Toohello komut dosyası izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c080b-340">(Optional) Append hello following toohello script.</span></span>

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
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="c080b-341">Toohello komut dosyası izleyen hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c080b-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="c080b-342">Toorun hello ek işlevler istiyorsanız hello # işareti kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c080b-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="c080b-343">Hdınsight kümesi sürüm 2.1 ise "https://$clusterName.azurehdinsight.net:443/oozie/v2/" "https://$clusterName.azurehdinsight.net:443/oozie/v1/" ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c080b-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="c080b-344">Hdınsight kümesi sürüm 2.1 değil destekler 2 hello web hizmetlerini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="c080b-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="c080b-345">Tıklatın **komut dosyasını Çalıştır** veya basın **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="c080b-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="c080b-346">Merhaba çıktı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="c080b-346">hello output will be similar to:</span></span>

     ![İş akışı çıkış öğreticisini çalıştırma][img-runworkflow-output]
11. <span data-ttu-id="c080b-348">SQL veritabanı toosee dışarı hello veri tooyour bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c080b-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="c080b-349">**toocheck hello iş hatası günlüğü**</span><span class="sxs-lookup"><span data-stu-id="c080b-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="c080b-350">tootroubleshoot bir iş akışı, hello Oozie günlük dosyası hello küme headnode C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c080b-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="c080b-351">RDP hakkında daha fazla bilgi için bkz: [kullanarak yönetme Hdınsight kümelerini hello Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="c080b-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="c080b-352">**toorerun başlangıç Öğreticisi**</span><span class="sxs-lookup"><span data-stu-id="c080b-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="c080b-353">toorerun hello iş akışı, hello aşağıdaki görevleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c080b-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="c080b-354">Merhaba Hive betiği çıktı dosyasını silin.</span><span class="sxs-lookup"><span data-stu-id="c080b-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="c080b-355">Merhaba log4jLogsCount tablosunda Hello veri silin.</span><span class="sxs-lookup"><span data-stu-id="c080b-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="c080b-356">Kullanabileceğiniz örnek Windows PowerShell betiğini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c080b-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="c080b-357">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c080b-357">Next steps</span></span>
<span data-ttu-id="c080b-358">Bu öğreticide, nasıl öğrenilen toodefine Oozie iş akışı ve Oozie Düzenleyicisi ve nasıl toorun Oozie Düzenleyicisi iş Azure PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c080b-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="c080b-359">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="c080b-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c080b-360">[Hdınsight kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c080b-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c080b-361">[Hdınsight ile Azure Blob storage kullanma][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="c080b-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="c080b-362">[Hdınsight Azure PowerShell kullanarak yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="c080b-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="c080b-363">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c080b-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c080b-364">[Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="c080b-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="c080b-365">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c080b-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c080b-366">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c080b-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c080b-367">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="c080b-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
