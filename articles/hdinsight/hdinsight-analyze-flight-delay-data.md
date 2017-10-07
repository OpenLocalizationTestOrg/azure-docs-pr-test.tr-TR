---
title: "hdınsight'ta - Azure Hadoop ile aaaAnalyze uçuş gecikme veri | Microsoft Docs"
description: "Merhaba kümesini silmek ve Sqoop iş Hive işini çalıştır toouse bir Windows PowerShell komut dosyası toocreate bir Hdınsight kümesi çalışma şeklini öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="39bf3-103">Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="39bf3-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="39bf3-104">Hive sağlar Hadoop MapReduce işleri adlı bir SQL benzeri komut dosyası dili ile çalışan bir  *[HiveQL][hadoop-hiveql]*, hangi uygulanabilir özetlemeye doğrultusunda, sorgulama, ve büyük miktarda veriyi analiz etme.</span><span class="sxs-lookup"><span data-stu-id="39bf3-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39bf3-105">Merhaba bu belgedeki adımlar Windows tabanlı Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="39bf3-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="39bf3-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="39bf3-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="39bf3-108">Linux tabanlı bir küme ile çalışma adımları için bkz: [(Linux) hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümlemek](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="39bf3-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="39bf3-109">Merhaba önemli yararlarından biri Azure Hdınsight hello veri depolama ve işlem ayrılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="39bf3-110">Hdınsight Azure Blob Depolama, veri depolaması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="39bf3-111">Tipik bir işi üç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="39bf3-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="39bf3-112">**Verileri Azure Blob Depolama alanında depolar.**</span><span class="sxs-lookup"><span data-stu-id="39bf3-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="39bf3-113">Örneğin, verileri, algılayıcı verilerini, web günlükleri hava durumu ve bu durumda, uçuş gecikme verileri Azure Blob depolama alanına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="39bf3-114">**İşlerini çalıştırın.**</span><span class="sxs-lookup"><span data-stu-id="39bf3-114">**Run jobs.**</span></span> <span data-ttu-id="39bf3-115">Zaman tooprocess hello veriler olduğunda, bir Windows PowerShell komut dosyası (veya bir istemci uygulaması) çalıştırmak toocreate bir Hdınsight kümesi işleri çalıştırma ve hello küme silin.</span><span class="sxs-lookup"><span data-stu-id="39bf3-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="39bf3-116">Çıktı veri tooAzure Blob Depolama kaydetme Hello işler.</span><span class="sxs-lookup"><span data-stu-id="39bf3-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="39bf3-117">hatta hello kümesi silindikten sonra hello çıktı verileri korunur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="39bf3-118">Bu şekilde, yalnızca ne, tüketilen için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="39bf3-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="39bf3-119">**Azure Blob depolama alanından Hello çıkış almak**, veya Bu öğreticide, hello veri tooan Azure SQL veritabanını dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="39bf3-120">Merhaba Aşağıdaki diyagramda hello senaryo ve bu öğreticinin hello yapısı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="39bf3-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="39bf3-122">Merhaba diyagramı Hello numaraları toohello bölüm başlıkları karşılık unutmayın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="39bf3-123">**M** hello ana işlem için anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-123">**M** stands for hello main process.</span></span> <span data-ttu-id="39bf3-124">**A** hello ek hello içeriği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="39bf3-125">Merhaba ana bölümü hello öğreticinin nasıl toouse bir Windows PowerShell komut dosyası tooperform hello aşağıdaki görevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="39bf3-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="39bf3-126">Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39bf3-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="39bf3-127">Bir Hive işi hello küme toocalculate ortalama gecikme üzerinde havaalanları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="39bf3-128">Merhaba uçuş gecikme veriler bir Azure Blob Depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="39bf3-129">Sqoop iş tooexport hello Hive işi çıkış tooan Azure SQL veritabanı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="39bf3-130">Merhaba Hdınsight kümesi silin.</span><span class="sxs-lookup"><span data-stu-id="39bf3-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="39bf3-131">Merhaba çok içinde uçuş gecikme veri yüklemek, Hive sorgu dizesi oluşturma/yükleme ve hello Azure SQL veritabanı için hello Sqoop işi hazırlama hello yönergelerini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39bf3-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="39bf3-132">Merhaba bu belgedeki belirli tooWindows tabanlı Hdınsight kümeleri adımlardır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="39bf3-133">Linux tabanlı bir küme ile çalışma adımları için bkz: [(Linux) hdınsight'ta Hive kullanarak uçuş gecikme verileri analiz](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="39bf3-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="39bf3-134">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="39bf3-134">Prerequisites</span></span>
<span data-ttu-id="39bf3-135">Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="39bf3-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="39bf3-136">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="39bf3-136">**An Azure subscription**.</span></span> <span data-ttu-id="39bf3-137">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="39bf3-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="39bf3-138">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="39bf3-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="39bf3-139">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="39bf3-140">Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="39bf3-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="39bf3-141">Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="39bf3-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="39bf3-142">Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="39bf3-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="39bf3-143">**Bu öğreticide kullanılan dosyaları**</span><span class="sxs-lookup"><span data-stu-id="39bf3-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="39bf3-144">Bu öğretici hello zamanında performans uçak uçuş verilerini kullanır [araştırma ve yenilikçi teknoloji yönetim, taşıma İstatistik Enstitüsü veya RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="39bf3-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="39bf3-145">Veriler hello kopyasını tooan Azure Blob Depolama kapsayıcısını hello ortak Blob erişim iznine sahip karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="39bf3-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="39bf3-146">PowerShell Betiği parçası hello ortak blob kapsayıcısı toohello varsayılan blob kapsayıcısından kümenizin hello verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="39bf3-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="39bf3-147">Merhaba betiğidir de HiveQL kopyalanan toohello aynı Blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="39bf3-148">Toolearn istiyorsanız tooget/karşıya yükleme hello veri tooyour nasıl kendi depolama hesabı ve nasıl toocreate/karşıya yükleme hello HiveQL komut dosyası, bkz: [ek A](#appendix-a) ve [ek B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="39bf3-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="39bf3-149">Merhaba aşağıdaki tabloda Bu öğreticide kullanılan hello dosyaları listeler:</span><span class="sxs-lookup"><span data-stu-id="39bf3-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="39bf3-150">Dosyalar</span><span class="sxs-lookup"><span data-stu-id="39bf3-150">Files</span></span></th><th><span data-ttu-id="39bf3-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="39bf3-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="39bf3-152">Merhaba HiveQL komut dosyası tarafından hello Hive işi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="39bf3-153">Bu komut dosyasını karşıya yüklenen tooan hello genel erişim ile Azure Blob Depolama hesabı olmuştur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="39bf3-154"><a href="#appendix-b">Ek B</a> hazırlama ve bu dosyayı tooyour kendi Azure Blob Depolama hesabı karşıya yükleme hakkında yönergeler vardır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="39bf3-155">Merhaba Hive işi için giriş verileri.</span><span class="sxs-lookup"><span data-stu-id="39bf3-155">Input data for hello Hive job.</span></span> <span data-ttu-id="39bf3-156">Merhaba verileri karşıya yüklenen tooan hello genel erişim ile Azure Blob Depolama hesabı olmuştur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="39bf3-157"><a href="#appendix-a">Ek A</a> hello verileri almak ve hello veri tooyour kendi Azure Blob Depolama hesabı karşıya yükleme yönergeleri açmıştır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="39bf3-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="39bf3-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="39bf3-159">Merhaba Hive işi Hello çıkış yolu.</span><span class="sxs-lookup"><span data-stu-id="39bf3-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="39bf3-160">Merhaba varsayılan kapsayıcı hello çıktı verilerini depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="39bf3-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="39bf3-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="39bf3-162">Merhaba Hive işi durumu klasör hello varsayılan kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="39bf3-163">Küme oluşturma ve Hive/Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="39bf3-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="39bf3-164">Hadoop MapReduce toplu işlemesidir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="39bf3-165">Merhaba en uygun maliyetli şekilde toorun Hive işi toocreate hello işi için bir kümedir ve hello iş tamamlandıktan sonra hello işi silin.</span><span class="sxs-lookup"><span data-stu-id="39bf3-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="39bf3-166">Merhaba aşağıdaki betiği hello tüm işlem kapsar.</span><span class="sxs-lookup"><span data-stu-id="39bf3-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="39bf3-167">Hdınsight kümesi oluşturma ve Hive işleri çalıştırma hakkında daha fazla bilgi için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri] [ hdinsight-provision] ve [Hdınsight ile Hive kullanma] [hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="39bf3-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="39bf3-168">**Azure PowerShell toorun hello Hive sorguları**</span><span class="sxs-lookup"><span data-stu-id="39bf3-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="39bf3-169">Merhaba yönergeleri kullanarak hello Sqoop iş çıktısı için bir Azure SQL veritabanı ve hello tablo oluşturma [ek C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="39bf3-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="39bf3-170">Windows PowerShell ISE açın ve komut dosyası izleyen hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
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
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="39bf3-171">Tooyour SQL veritabanına bağlanmak ve hello AvgDelays tablo şehirde ortalama uçuş gecikmelerinden bakın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="39bf3-173"><a id="appendix-a"></a>Ek A - karşıya yükleme uçuş gecikme veri tooAzure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="39bf3-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="39bf3-174">Merhaba veri dosyası ve hello HiveQL komut dosyaları karşıya yükleme (bkz [ek B](#appendix-b)) bazı planlama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="39bf3-175">Merhaba toostore hello veri dosyaları ve Hdınsight kümesi oluşturma ve hello Hive işi çalıştırma önce hello HiveQL dosya olur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="39bf3-176">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="39bf3-176">You have two options:</span></span>

* <span data-ttu-id="39bf3-177">**Kullanım hello aynı hello Hdınsight küme tarafından hello varsayılan dosya sistemi olarak kullanılacak Azure depolama hesabı.**</span><span class="sxs-lookup"><span data-stu-id="39bf3-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="39bf3-178">Merhaba Hdınsight kümesi hello depolama hesabının erişim anahtarı olacağı için ek değişiklikler toomake gerekmez.</span><span class="sxs-lookup"><span data-stu-id="39bf3-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="39bf3-179">**Merhaba Hdınsight küme varsayılan dosya sistemi farklı bir Azure Storage hesabını kullanın.**</span><span class="sxs-lookup"><span data-stu-id="39bf3-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="39bf3-180">Merhaba Durum buysa, hello oluşturma hello Windows PowerShell komut dosyası bulundu parçası değiştirmelisiniz [oluşturma Hdınsight kümesi ve çalışma Hive/Sqoop işleri](#runjob) toolink hello ek depolama alanı hesabı olarak depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="39bf3-181">Yönergeler için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="39bf3-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="39bf3-182">Merhaba Hdınsight kümesi sonra hello hello depolama hesabı için erişim anahtarı bilir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="39bf3-183">Merhaba Blob Depolama yolu hello veri dosyası için sabit kodlanmış içinde hello HiveQL komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="39bf3-184">Buna uygun şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-184">You must update it accordingly.</span></span>

<span data-ttu-id="39bf3-185">**toodownload hello uçuş veri**</span><span class="sxs-lookup"><span data-stu-id="39bf3-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="39bf3-186">Çok Gözat[araştırma ve yenilikçi teknoloji yönetim, taşıma İstatistik Enstitüsü][rita-website].</span><span class="sxs-lookup"><span data-stu-id="39bf3-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="39bf3-187">Başlangıç sayfasında, aşağıdaki değerleri hello seçin:</span><span class="sxs-lookup"><span data-stu-id="39bf3-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="39bf3-188">Ad</span><span class="sxs-lookup"><span data-stu-id="39bf3-188">Name</span></span></th><th><span data-ttu-id="39bf3-189">Değer</span><span class="sxs-lookup"><span data-stu-id="39bf3-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="39bf3-190">Filtre yıl</span><span class="sxs-lookup"><span data-stu-id="39bf3-190">Filter Year</span></span></td><td><span data-ttu-id="39bf3-191">2013</span><span class="sxs-lookup"><span data-stu-id="39bf3-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="39bf3-192">Dönem filtre</span><span class="sxs-lookup"><span data-stu-id="39bf3-192">Filter Period</span></span></td><td><span data-ttu-id="39bf3-193">Ocak</span><span class="sxs-lookup"><span data-stu-id="39bf3-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-194">Alanları</span><span class="sxs-lookup"><span data-stu-id="39bf3-194">Fields</span></span></td><td><span data-ttu-id="39bf3-195">*Yıl*, *FlightDate*, *UniqueCarrier*, *taşıyıcı*, *FlightNum*, *OriginAirportID* , *Kaynak*, *OriginCityName*, *OriginState*, *DestAirportID*, *hedef* , *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*,  *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*,  *LateAircraftDelay* (diğer tüm alanlar Temizle)</span><span class="sxs-lookup"><span data-stu-id="39bf3-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="39bf3-196">
3.Tıklatın **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="39bf3-196">
3. Click **Download**.</span></span>
<span data-ttu-id="39bf3-197">4.</span><span class="sxs-lookup"><span data-stu-id="39bf3-197">4.</span></span> <span data-ttu-id="39bf3-198">Merhaba dosya toohello sıkıştırmasını **C:\Tutorials\FlightDelay\2013Data** klasör.</span><span class="sxs-lookup"><span data-stu-id="39bf3-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="39bf3-199">Her dosya, bir CSV dosyası ve yaklaşık 60 GB boyutunda.</span><span class="sxs-lookup"><span data-stu-id="39bf3-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="39bf3-200">5.</span><span class="sxs-lookup"><span data-stu-id="39bf3-200">5.</span></span> <span data-ttu-id="39bf3-201">Merhaba toohello verilerini içeren hello ayın yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="39bf3-202">Örneğin, hello dosya hello Ocak verileri içeren adlandırılmış *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="39bf3-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="39bf3-203">6.</span><span class="sxs-lookup"><span data-stu-id="39bf3-203">6.</span></span> <span data-ttu-id="39bf3-204">Adım 2 ve 5 toodownload bir dosyayı her hello için 12 ay 2013'te yineleyin.</span><span class="sxs-lookup"><span data-stu-id="39bf3-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="39bf3-205">En az bir dosya toorun hello öğreticinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="39bf3-206">**tooupload hello uçuş gecikme veri tooAzure Blob Depolama**</span><span class="sxs-lookup"><span data-stu-id="39bf3-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="39bf3-207">Merhaba parametreleri hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="39bf3-208">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="39bf3-208">Variable Name</span></span></th><th><span data-ttu-id="39bf3-209">Notlar</span><span class="sxs-lookup"><span data-stu-id="39bf3-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="39bf3-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="39bf3-210">$storageAccountName</span></span></td><td><span data-ttu-id="39bf3-211">Merhaba tooupload hello verilerin istediğiniz Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="39bf3-212">$blobContainerName</span></span></td><td><span data-ttu-id="39bf3-213">Blob kapsayıcısı tooupload hello verilerin istediğiniz hello.</span><span class="sxs-lookup"><span data-stu-id="39bf3-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="39bf3-214">Azure PowerShell ISE açın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="39bf3-215">3.</span><span class="sxs-lookup"><span data-stu-id="39bf3-215">3.</span></span> <span data-ttu-id="39bf3-216">Komut dosyası hello betik bölmesine aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="39bf3-217">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="39bf3-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="39bf3-218">Lütfen hello dosyaları karşıya yükleme için farklı bir yöntem toouse seçerseniz, flightdelay/öğreticileri/veri hello dosya yolu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="39bf3-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="39bf3-219">Merhaba dosyalara erişmek için hello sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="39bf3-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="39bf3-220">Merhaba yolu öğreticileri/flightdelay/verilerini hello dosyaları karşıya yüklediğiniz sırada oluşturulan hello sanal klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="39bf3-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="39bf3-221">12 dosyaları, her ay için bir tane olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="39bf3-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="39bf3-222">Merhaba Hive sorgusu tooread hello yeni konumdan güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="39bf3-223">Merhaba kapsayıcı erişim izni toobe ortak yapılandırmak veya hello depolama hesabı toohello Hdınsight kümesine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="39bf3-224">Aksi takdirde hello Hive sorgu dizesi mümkün tooaccess hello veri dosyalarını olmaz.</span><span class="sxs-lookup"><span data-stu-id="39bf3-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="39bf3-225"><a id="appendix-b"></a>Ek B - oluşturun ve HiveQL betiğini yükleyin</span><span class="sxs-lookup"><span data-stu-id="39bf3-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="39bf3-226">Azure PowerShell kullanarak, birden çok HiveQL ifadelerini tek bir saat veya paket hello HiveQL deyimi bir komut dosyasına çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39bf3-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="39bf3-227">Bu bölümde, nasıl toocreate HiveQL betiğini ve karşıya yükleme hello tooAzure Blob Depolama Azure PowerShell kullanarak komut dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="39bf3-228">Hive Azure Blob depolamada depolanan hello HiveQL betikleri toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="39bf3-229">Merhaba HiveQL betiğini hello aşağıdakileri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="39bf3-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="39bf3-230">**Merhaba delays_raw tablo bırakma**, hello tablo zaten mevcut durumda.</span><span class="sxs-lookup"><span data-stu-id="39bf3-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="39bf3-231">**Merhaba delays_raw dış Hive tablosu oluşturmak** hello uçuş gecikme dosyalarıyla toohello Blob depolama konumuna işaret eden.</span><span class="sxs-lookup"><span data-stu-id="39bf3-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="39bf3-232">Bu sorgu alanları tarafından sınırlandırılır belirtir "," ve "tarafından \n" satırları sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="39bf3-233">Alan değerleri virgül içerdiğinde Hive alan sınırlayıcı virgül ve alan değeri parçası olan bir tane arasında ayrım çünkü bu bir sorun oluşturur (kaynak için alan değerlerini hello durumda olduğu\_ŞEHİR\_adı ve hedef\_ ŞEHİR\_adı).</span><span class="sxs-lookup"><span data-stu-id="39bf3-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="39bf3-234">tooaddress Bu, hello sorgu sütunlara yanlış bölme toohold veri TEMP sütunları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="39bf3-235">**Başlangıç gecikmeleri tablo bırakma**, hello tablo zaten mevcut durumda.</span><span class="sxs-lookup"><span data-stu-id="39bf3-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="39bf3-236">**Merhaba gecikmeler tablosu oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="39bf3-236">**Create hello delays table**.</span></span> <span data-ttu-id="39bf3-237">Merhaba verileri yararlı tooclean başka bir işleme önce yoktur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="39bf3-238">Bu sorgu yeni bir tablo oluşturur *gecikmeler*, hello delays_raw tablosundan.</span><span class="sxs-lookup"><span data-stu-id="39bf3-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="39bf3-239">(Daha önce belirtildiği gibi) hello TEMP sütunları kopyalanmadı Not ve o hello **substring** kullanılan tooremove tırnak işaretleri hello verilerden işlevdir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="39bf3-240">**Merhaba ortalama hava durumu gecikme ve grupları hello sonuçları Şehir ada göre işlem.**</span><span class="sxs-lookup"><span data-stu-id="39bf3-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="39bf3-241">Ayrıca hello sonuçları tooBlob depolama çıktı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="39bf3-242">Hello sorgulayan kesme hello verilerden kaldıracak ve burada hello değeri için satır dışladığı Not **weather_delay** null.</span><span class="sxs-lookup"><span data-stu-id="39bf3-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="39bf3-243">Daha sonra Bu öğreticide kullanılan Sqoop, bu değerler varsayılan olarak işleyebilmesini değil çünkü bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="39bf3-244">Merhaba HiveQL komutları tam bir listesi için bkz: [Hive veri tanımlama dili][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="39bf3-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="39bf3-245">Noktalı virgül Sonlandır her HiveQL komutu gerekir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="39bf3-246">**toocreate HiveQL komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="39bf3-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="39bf3-247">Merhaba parametreleri hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="39bf3-248">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="39bf3-248">Variable Name</span></span></th><th><span data-ttu-id="39bf3-249">Notlar</span><span class="sxs-lookup"><span data-stu-id="39bf3-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="39bf3-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="39bf3-250">$storageAccountName</span></span></td><td><span data-ttu-id="39bf3-251">Merhaba tooupload hello HiveQL betiğini istediğiniz Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="39bf3-252">$blobContainerName</span></span></td><td><span data-ttu-id="39bf3-253">Blob kapsayıcısı tooupload hello HiveQL betiğini istediğiniz hello.</span><span class="sxs-lookup"><span data-stu-id="39bf3-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="39bf3-254">Azure PowerShell ISE açın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="39bf3-255">3.</span><span class="sxs-lookup"><span data-stu-id="39bf3-255">3.</span></span> <span data-ttu-id="39bf3-256">Kopyalama ve yapıştırma hello betik bölmesine komut dosyası izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="39bf3-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="39bf3-257">Merhaba komut dosyasında kullanılan hello değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="39bf3-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="39bf3-258">**$hqlLocalFileName** -hello betik kaydeder hello HiveQL komut dosyası yerel olarak yüklemeden önce tooBlob depolama.</span><span class="sxs-lookup"><span data-stu-id="39bf3-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="39bf3-259">Merhaba dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="39bf3-259">This is hello file name.</span></span> <span data-ttu-id="39bf3-260">Merhaba varsayılan değer <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="39bf3-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="39bf3-261">**$hqlBlobName** -hello Azure Blob Depolama kullanılan hello HiveQL komut dosyası blob adı budur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="39bf3-262">tutorials/flightdelay/flightdelays.hql Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="39bf3-263">Merhaba dosyasını doğrudan tooAzure Blob depolama alanına yazılır, var olmadığından bir "/" Merhaba başında hello blob adı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="39bf3-264">Blob depolama biriminden tooaccess hello dosyanın istiyorsanız, tooadd gerekir bir "/" Merhaba başında hello dosya adı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="39bf3-265">**$srcDataFolder** ve **$dstDataFolder** -"flightdelay/öğreticileri/data" = "flightdelay/öğreticileri/çıktı" =</span><span class="sxs-lookup"><span data-stu-id="39bf3-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="39bf3-266"><a id="appendix-c"></a>Ek C - hello Sqoop iş çıktısı için bir Azure SQL veritabanı hazırlama</span><span class="sxs-lookup"><span data-stu-id="39bf3-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="39bf3-267">**tooprepare hello SQL veritabanı (Merhaba Sqoop betik ile Birleştir)**</span><span class="sxs-lookup"><span data-stu-id="39bf3-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="39bf3-268">Merhaba parametreleri hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="39bf3-269">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="39bf3-269">Variable Name</span></span></th><th><span data-ttu-id="39bf3-270">Notlar</span><span class="sxs-lookup"><span data-stu-id="39bf3-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="39bf3-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="39bf3-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="39bf3-272">hello Azure SQL veritabanı sunucusunun adını Hello.</span><span class="sxs-lookup"><span data-stu-id="39bf3-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="39bf3-273">Hiçbir şey girin toocreate yeni bir sunucu.</span><span class="sxs-lookup"><span data-stu-id="39bf3-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="39bf3-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="39bf3-275">hello Azure SQL veritabanı sunucusu için Hello oturum açma adı.</span><span class="sxs-lookup"><span data-stu-id="39bf3-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="39bf3-276">$SqlDatabaseServerName var olan bir sunucu varsa hello oturum açma ve oturum açma parolası hello sunucusuyla kullanılan tooauthenticate edilir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="39bf3-277">Aksi takdirde kullanılan toocreate yeni bir sunucu oldukları.</span><span class="sxs-lookup"><span data-stu-id="39bf3-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="39bf3-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="39bf3-279">hello Azure SQL veritabanı sunucusuna Hello oturum açma parolası.</span><span class="sxs-lookup"><span data-stu-id="39bf3-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="39bf3-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="39bf3-281">Yalnızca yeni bir Azure veritabanı sunucusu oluştururken bu değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="39bf3-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="39bf3-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="39bf3-283">Merhaba SQL veritabanı toocreate hello AvgDelays tablo hello Sqoop işi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="39bf3-284">Boş bırakarak HDISqoop adlı bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="39bf3-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="39bf3-285">Merhaba tablo hello Sqoop iş çıktısı AvgDelays adıdır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="39bf3-286">Azure PowerShell ISE açın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="39bf3-287">3.</span><span class="sxs-lookup"><span data-stu-id="39bf3-287">3.</span></span> <span data-ttu-id="39bf3-288">Kopyalama ve yapıştırma hello betik bölmesine komut dosyası izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="39bf3-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="39bf3-289">Merhaba komut dosyası kullanan bir temsili durum aktarımı (REST) hizmeti, http://bot.whatismyipaddress.com, tooretrieve dış IP adresi.</span><span class="sxs-lookup"><span data-stu-id="39bf3-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="39bf3-290">Başlangıç IP adresi, SQL veritabanı sunucunuz için bir güvenlik duvarı kuralı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="39bf3-291">Merhaba komut dosyasında kullanılan bazı değişkenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="39bf3-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="39bf3-292">**$ipAddressRestService** -hello varsayılan değerdir http://bot.whatismyipaddress.com. Bir ortak IP adresi, dış IP adresi almak için REST hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="39bf3-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="39bf3-293">İsterseniz diğer hizmetler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39bf3-293">You can use other services if you want.</span></span> <span data-ttu-id="39bf3-294">(bir Windows PowerShell komut dosyası kullanarak) istasyonunuzdan hello veritabanı erişebilmeniz hello hizmeti aracılığıyla alınan hello dış IP adresi kullanılan toocreate Azure SQL veritabanı sunucunuz için bir güvenlik duvarı kuralı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="39bf3-295">**$fireWallRuleName** -bu hello hello güvenlik duvarı kuralı hello Azure SQL veritabanı sunucusunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="39bf3-296">Merhaba varsayılan ad <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="39bf3-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="39bf3-297">İstiyorsanız, onu yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39bf3-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="39bf3-298">**$sqlDatabaseMaxSizeGB** -yalnızca yeni bir Azure SQL veritabanı sunucusu oluştururken bu değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="39bf3-299">Merhaba varsayılan değer 10 GB'tır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-299">hello default value is 10GB.</span></span> <span data-ttu-id="39bf3-300">Bu öğretici için 10GB yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="39bf3-301">**$sqlDatabaseName** -yalnızca yeni bir Azure SQL veritabanı oluştururken bu değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39bf3-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="39bf3-302">HDISqoop Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="39bf3-303">Adlandırırsanız, hello Sqoop Windows PowerShell Betiği uygun şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="39bf3-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="39bf3-304">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="39bf3-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="39bf3-305">Merhaba komut dosyası çıkışını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-305">Validate hello script output.</span></span> <span data-ttu-id="39bf3-306">Merhaba komut dosyası başarıyla çalıştırıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="39bf3-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="39bf3-307"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="39bf3-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="39bf3-308">Anladığınızdan artık nasıl tooupload dosya tooAzure Blob storage, toopopulate bir Hive tablosu nasıl hello verileri Azure Blob depolama biriminden kullanarak nasıl toorun Hive sorguları ve nasıl toouse HDFS tooan Azure SQL veritabanından Sqoop tooexport veri.</span><span class="sxs-lookup"><span data-stu-id="39bf3-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="39bf3-309">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="39bf3-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="39bf3-310">[Hdınsight kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="39bf3-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="39bf3-311">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="39bf3-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="39bf3-312">[Oozie Hdınsight ile kullanma][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="39bf3-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="39bf3-313">[Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="39bf3-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="39bf3-314">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="39bf3-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="39bf3-315">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="39bf3-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
