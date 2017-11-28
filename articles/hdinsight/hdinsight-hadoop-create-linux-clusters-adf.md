---
title: "Data Factory - Azure Hdınsight kullanarak isteğe bağlı Hadoop kümelerini aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure Data Factory kullanarak Hdınsight'ta isteğe bağlı Hadoop kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="81ebb-103">Azure Data Factory kullanarak Hdınsight'ta isteğe bağlı Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="81ebb-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="81ebb-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="81ebb-105">Bu bir Hdınsight Hadoop kümesi yalnızca zaman tooprocess bir giriş veri dilimi oluşturma ve hello işlem tamamlandığında hello küme silme.</span><span class="sxs-lookup"><span data-stu-id="81ebb-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="81ebb-106">Bir isteğe bağlı Hdınsight Hadoop kümesi kullanarak hello avantajlarından bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="81ebb-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="81ebb-107">Yalnızca ödeme hello süresi işi için Hdınsight Hadoop küme (bir kısa yapılandırılabilir boşta kalma süresi) hello çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="81ebb-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="81ebb-108">Hdınsight kümeleri için Hello fatura pro-dakika başına, bunları veya kullanıp kullanmadığınızı derecelendirilir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="81ebb-109">Veri fabrikasında bir isteğe bağlı Hdınsight bağlı hizmeti kullandığınızda, isteğe bağlı hello kümeleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="81ebb-110">Ve hello işleri tamamlandığında hello kümeleri otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="81ebb-111">Bu nedenle, yalnızca süresi ve hello kısa boşta kalma süresi (yaşam süresi ayarı) çalıştıran hello işi için ödeme yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="81ebb-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="81ebb-112">Data Factory işlem hattı kullanarak bir iş akışı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="81ebb-113">Örneğin, bir şirket içi SQL Server tooan Azure blob depolama, bir isteğe bağlı Hdınsight Hadoop kümesinde bir Hive betiği ve Pig betiği çalıştırarak işlem hello verileri hello ardışık düzen toocopy verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="81ebb-114">Ardından, BI uygulamaları tooconsume için hello sonuç veri tooan Azure SQL Data Warehouse kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="81ebb-115">Merhaba iş akışı toorun düzenli aralıklarla (saatlik, günlük, haftalık, aylık, vb.) zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="81ebb-116">Azure Data Factory'de veri fabrikası bir veya daha fazla veri işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="81ebb-117">Veri ardışık bir veya daha fazla etkinlikler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="81ebb-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="81ebb-118">İki tür etkinlik vardır: [veri taşıma etkinlikleri](../data-factory/data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="81ebb-119">Bir kaynak veri deposu tooa hedef veri deposundan veri taşıma etkinlikleri (şu anda, yalnızca kopyalama etkinliği) toomove verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="81ebb-120">Veri dönüştürme etkinlikleri tootransform/işlem verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="81ebb-121">Hdınsight Hive etkinliği Data Factory ile desteklenen hello dönüştürme etkinlikleri biridir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="81ebb-122">Bu öğreticide hello Hive dönüşüm etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="81ebb-123">Hive etkinliği toouse kendi Hdınsight Hadoop kümesi veya bir isteğe bağlı Hdınsight Hadoop kümesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="81ebb-124">Bu öğreticide, hello hello data factory işlem hattı Hive etkinliğiyle yapılandırılmış toouse isteğe bağlı Hdınsight kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="81ebb-125">Bu nedenle, hello etkinlik veri dilimi tooprocess çalıştırıldığında, şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="81ebb-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="81ebb-126">Hdınsight Hadoop kümesi, yalnızca zaman tooprocess hello dilim için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="81ebb-127">Merhaba giriş verisi hello kümede HiveQL betiğini çalıştırarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="81ebb-128">Merhaba Hdınsight Hadoop kümesi hello işlem tamamlandıktan sonra hello küme yapılandırılmış hello süreyi (timeToLive ayarını) için boşta silinir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="81ebb-129">Merhaba sonraki veri dilimi varsa bu timeToLive boşta kalma süresi ile işlemek için hello aynı kümede kullanılan tooprocess hello dilim olur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="81ebb-130">Bu öğreticide, hello hello hive etkinliği ile ilişkili HiveQL betiğini hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="81ebb-131">Bir Azure Blob depolamada depolanan ham web günlüğü verilerini başvuruları hello bir dış tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="81ebb-132">Yıl ve ay tarafından bölümleri hello ham verileri.</span><span class="sxs-lookup"><span data-stu-id="81ebb-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="81ebb-133">Depoları hello Azure blob depolama bölümlenmiş verilerde hello.</span><span class="sxs-lookup"><span data-stu-id="81ebb-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="81ebb-134">Bu öğreticide, hello hello hive etkinliği ile ilişkili HiveQL betiğini başvuruları hello Azure Blob Storage depolanan ham web günlüğü verilerini hello bir dış tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="81ebb-135">Merhaba girdi dosyasında her ay hello örnek satırları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="81ebb-136">Merhaba HiveQL betiğini bölümleri, ay ve yıl ham verileri hello.</span><span class="sxs-lookup"><span data-stu-id="81ebb-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="81ebb-137">Merhaba önceki girişinize göre üç çıkış klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="81ebb-138">Her klasör her ay girişlerinden sahip bir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="81ebb-139">Data Factory veri dönüştürme etkinlikleri toplama tooHive etkinliğinde bir listesi için bkz: [dönüştürme ve Azure Data Factory kullanarak Analiz](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="81ebb-140">Şu anda, Azure veri fabrikası'ndan yalnızca Hdınsight kümesi sürüm 3.2 oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81ebb-141">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="81ebb-141">Prerequisites</span></span>
<span data-ttu-id="81ebb-142">Bu makaledeki yönergeleri hello başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="81ebb-143">[Azure aboneliği](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="81ebb-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="81ebb-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81ebb-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="81ebb-145">Depolama hesabını hazırlama</span><span class="sxs-lookup"><span data-stu-id="81ebb-145">Prepare storage account</span></span>
<span data-ttu-id="81ebb-146">Bu senaryoda toothree depolama hesaplarını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="81ebb-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="81ebb-147">Merhaba Hdınsight kümesi için varsayılan depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="81ebb-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="81ebb-148">Merhaba giriş verileri için depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="81ebb-148">storage account for hello input data</span></span>
- <span data-ttu-id="81ebb-149">Merhaba çıktı verileri için depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="81ebb-149">storage account for hello output data</span></span>

<span data-ttu-id="81ebb-150">toosimplify hello öğretici, bir depolama hesabı tooserve hello üç amacıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="81ebb-151">Bu bölümde bulunan hello Azure PowerShell örnek betiği hello aşağıdaki görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="81ebb-152">TooAzure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="81ebb-153">Bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ebb-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="81ebb-154">Bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ebb-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="81ebb-155">Merhaba depolama hesabında Blob kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="81ebb-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="81ebb-156">İki dosyaları toohello Blob kapsayıcısı aşağıdaki hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="81ebb-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="81ebb-157">Giriş veri dosyasını: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="81ebb-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="81ebb-158">HiveQL betiğini: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="81ebb-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="81ebb-159">Her iki dosyaları bir ortak Blob kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="81ebb-160">**Azure PowerShell kullanarak tooprepare hello depolama ve kopyalama hello dosyalar:**</span><span class="sxs-lookup"><span data-stu-id="81ebb-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="81ebb-161">Hello Azure kaynak grubu ve hello komut dosyası tarafından oluşturulacak hello Azure depolama hesabı adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="81ebb-162">Yazma **kaynak grubu adı**, **depolama hesabı adı**, ve **depolama hesabı anahtarı** hello komut dosyası tarafından yüzdelik.</span><span class="sxs-lookup"><span data-stu-id="81ebb-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="81ebb-163">Merhaba sonraki bölümde gereksinim duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="81ebb-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="81ebb-164">Merhaba PowerShell Betiği yardıma gereksinim duyarsanız, bkz: [kullanma hello Azure PowerShell'i Azure Storage ile](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="81ebb-165">Azure CLI toouse gibi bunun yerine, hello görürseniz [ek](#appendix) hello Azure CLI komut dosyası için bölüm.</span><span class="sxs-lookup"><span data-stu-id="81ebb-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="81ebb-166">**tooexamine, hello depolama hesabı ve hello içeriği**</span><span class="sxs-lookup"><span data-stu-id="81ebb-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="81ebb-167">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81ebb-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="81ebb-168">Tıklatın **kaynak grupları** hello sol bölmedeki.</span><span class="sxs-lookup"><span data-stu-id="81ebb-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="81ebb-169">PowerShell komut dosyasında oluşturulan hello kaynak grubu adı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="81ebb-170">Listelenen çok fazla kaynak grupları varsa hello filtresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="81ebb-171">Merhaba üzerinde **kaynakları** kutucuğu, diğer projelerle hello kaynak grubu paylaşmak sürece listelenen bir kaynak sahip.</span><span class="sxs-lookup"><span data-stu-id="81ebb-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="81ebb-172">Bu kaynak hello depolama hesabını daha önce belirtilen hello ada sahip değil.</span><span class="sxs-lookup"><span data-stu-id="81ebb-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="81ebb-173">Merhaba depolama hesabının adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="81ebb-174">Merhaba tıklatın **BLOB'lar** döşeme.</span><span class="sxs-lookup"><span data-stu-id="81ebb-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="81ebb-175">Merhaba tıklatın **adfgetstarted** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="81ebb-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="81ebb-176">İki klasör bkz: **inputdata** ve **betik**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="81ebb-177">Merhaba klasörünü açın ve hello klasörlerdeki hello dosyaları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="81ebb-178">Merhaba inputdata girdi verileriyle hello input.log dosya ve hello betik klasörü hello HiveQL komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="81ebb-179">Resource Manager şablonu kullanarak bir veri fabrikası oluşturun</span><span class="sxs-lookup"><span data-stu-id="81ebb-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="81ebb-180">Merhaba depolama hesabı, hello giriş verileri ve hello hazırlanmış HiveQL betiğini ile hazır toocreate bir Azure data factory değildir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="81ebb-181">Veri Fabrikası oluşturmaya yönelik birkaç yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="81ebb-182">Bu öğreticide, veri fabrikası hello Azure portal kullanarak bir Azure Resource Manager şablonu dağıtarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ebb-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="81ebb-183">Kullanarak bir Resource Manager şablonu dağıtabilirsiniz [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) ve [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="81ebb-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="81ebb-184">Diğer veri fabrikası oluşturma yöntemleri için bkz: [Öğreticisi: ilk data factory'nizi derleme](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="81ebb-185">Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="81ebb-186">Merhaba şablon https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json bulunur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="81ebb-187">Merhaba bkz [Data Factory varlıklarını hello şablonunda](#data-factory-entities-in-the-template) hello şablonda tanımlanan varlıklar hakkında ayrıntılı bilgi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="81ebb-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="81ebb-188">Seçin **kullanım varolan** hello seçeneği **kaynak grubu** ayarı ve select hello (PowerShell Betiği kullanılarak) hello önceki adımda oluşturduğunuz hello kaynak grubunun adını.</span><span class="sxs-lookup"><span data-stu-id="81ebb-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="81ebb-189">Merhaba veri fabrikası için bir ad girin (**veri fabrikası adı**).</span><span class="sxs-lookup"><span data-stu-id="81ebb-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="81ebb-190">Bu ad genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="81ebb-191">Merhaba girin **depolama hesabı adı** ve **depolama hesabı anahtarı** hello önceki adımda yazdığınız.</span><span class="sxs-lookup"><span data-stu-id="81ebb-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="81ebb-192">Seçin **toohello hüküm ve koşulları kabul ediyorum** okuma sonra yukarıda belirtilen **hüküm ve koşullar**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="81ebb-193">Seçin **PIN toodashboard** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="81ebb-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="81ebb-194">Tıklatın **satın alma ve oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="81ebb-195">Pano adlı hello üzerinde bir kutucuk gördüğünüz **dağıtma şablon dağıtımı**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="81ebb-196">Merhaba kadar bekleyin **kaynak grubu** kaynak grubunuz için bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="81ebb-197">Kaynak grubu adı tooopen hello kaynak grubu dikey pencerenizi başlıklı hello kutucuk de tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="81ebb-198">Merhaba kaynak grubu dikey zaten açık değilse hello döşeme tooopen hello kaynak grubunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="81ebb-199">Göreceksiniz artık bir daha fazla veri fabrikası kaynak ayrıca toohello depolama hesabı kaynak listelenir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="81ebb-200">Veri fabrikanızın Hello adına tıklayın (hello için belirtilen değer **veri fabrikası adı** parametresi).</span><span class="sxs-lookup"><span data-stu-id="81ebb-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="81ebb-201">Merhaba Data Factory dikey penceresinde hello tıklayın **diyagramı** döşeme.</span><span class="sxs-lookup"><span data-stu-id="81ebb-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="81ebb-202">bir etkinliği bir girdi veri kümesi ve bir çıkış veri kümesi ile Merhaba diyagramda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure veri fabrikası Hdınsight isteğe bağlı Hive etkinlik ardışık düzeni diyagramı](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="81ebb-204">Merhaba adları hello Resource Manager şablonunda tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="81ebb-205">Çift **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="81ebb-206">Merhaba üzerinde **son güncelleştirilen dilimler**, bir dilim göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="81ebb-207">Merhaba durumundaysa **devam eden**, çok değiştirilmesini bekleyin**hazır**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="81ebb-208">Genellikle hakkında sürdüğünü **20 dakika** toocreate Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="81ebb-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="81ebb-209">Merhaba veri fabrikası çıktısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="81ebb-209">Check hello data factory output</span></span>

1. <span data-ttu-id="81ebb-210">Kullanım hello aynı hello son oturum toocheck Merhaba kapsayıcılara hello adfgetstarted kapsayıcısının yordamda.</span><span class="sxs-lookup"><span data-stu-id="81ebb-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="81ebb-211">Var olan iki yeni kapsayıcılar ayrıca çok**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="81ebb-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="81ebb-212">Bir kapsayıcı adıyla hello deseni izler: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="81ebb-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="81ebb-213">Merhaba varsayılan kapsayıcı hello Hdınsight kümesi için kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="81ebb-214">adfjobs: Bu kapsayıcı hello ADF iş günlükleri için hello kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="81ebb-215">Merhaba veri fabrikası çıkış depolanır **afgetstarted** hello Resource Manager şablonunda yapılandırıldığı şekilde.</span><span class="sxs-lookup"><span data-stu-id="81ebb-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="81ebb-216">Tıklatın **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="81ebb-217">Çift **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="81ebb-218">Gördüğünüz bir **yıl 2014 =** klasörü tüm hello web günlüklerini yıl 2014 tarihli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="81ebb-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Azure veri fabrikası Hdınsight isteğe bağlı Hive etkinliği ardışık düzeni çıkış](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="81ebb-220">Merhaba listede aşağı doğru ayrıntıya, Ocak, Şubat ve Mart için üç klasörleri göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="81ebb-221">Ve her ay için bir günlük yok.</span><span class="sxs-lookup"><span data-stu-id="81ebb-221">And there is a log for each month.</span></span>

    ![Azure veri fabrikası Hdınsight isteğe bağlı Hive etkinliği ardışık düzeni çıkış](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="81ebb-223">Data Factory varlıklarını hello şablonunda</span><span class="sxs-lookup"><span data-stu-id="81ebb-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="81ebb-224">Veri Fabrikası için üst düzey Resource Manager şablonu hello benzer nasıl aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="81ebb-225">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="81ebb-225">Define data factory</span></span>
<span data-ttu-id="81ebb-226">Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="81ebb-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="81ebb-227">Merhaba dataFactoryName hello şablonu dağıttığınızda belirttiğiniz hello veri fabrikası hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="81ebb-228">Veri Fabrikası şu anda yalnızca hello Doğu ABD, Batı ABD ve Kuzey Avrupa bölgelerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="81ebb-229">Merhaba veri fabrikası varlıkları tanımlama</span><span class="sxs-lookup"><span data-stu-id="81ebb-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="81ebb-230">Merhaba aşağıdaki Data Factory varlıklarını hello JSON şablonunda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="81ebb-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="81ebb-231">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="81ebb-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="81ebb-232">İsteğe bağlı HDInsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="81ebb-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="81ebb-233">Azure Blob girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="81ebb-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="81ebb-234">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="81ebb-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="81ebb-235">Kopyalama etkinliği içeren bir veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="81ebb-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="81ebb-236">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="81ebb-236">Azure Storage linked service</span></span>
<span data-ttu-id="81ebb-237">Hello Azure depolama hizmeti Azure depolama hesabı toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="81ebb-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="81ebb-238">Bu öğreticide, hello aynı depolama hesabındaki hello varsayılan Hdınsight depolama hesabı, giriş veri depolama ve çıktı veri depolama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="81ebb-239">Bu nedenle, bir Azure Storage bağlı hizmeti yalnızca tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="81ebb-240">Merhaba bağlantılı hizmet tanımında hello adı ve Azure depolama hesabınızın anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="81ebb-241">Bkz: [Azure depolama bağlantılı hizmeti](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="81ebb-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="81ebb-242">Merhaba **connectionString** hello storageAccountName ve storageAccountKey parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="81ebb-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="81ebb-243">Merhaba şablonu dağıtırken bu parametrelerin değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="81ebb-244">İsteğe bağlı HDInsight bağlantılı hizmeti</span><span class="sxs-lookup"><span data-stu-id="81ebb-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="81ebb-245">Hello hizmet tanımı isteğe bağlı Hdınsight bağlı olarak bir Hdınsight Hadoop kümesi çalışma zamanında hello Data Factory hizmeti toocreate tarafından kullanılan yapılandırma parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="81ebb-246">Bkz: [işlem bağlı Hizmetleri](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) bir Hdınsight isteğe bağlı hizmet makalesi JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="81ebb-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="81ebb-247">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="81ebb-247">Note hello following points:</span></span>

* <span data-ttu-id="81ebb-248">Merhaba Data Factory oluşturur bir **Linux tabanlı** , Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="81ebb-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="81ebb-249">Merhaba Hdınsight Hadoop kümesi hello aynı oluşturulan hello depolama hesabı bölgeye.</span><span class="sxs-lookup"><span data-stu-id="81ebb-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="81ebb-250">Bildirim hello *timeToLive* ayarı.</span><span class="sxs-lookup"><span data-stu-id="81ebb-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="81ebb-251">Merhaba küme 30 dakika boşta kaldıktan sonra hello veri fabrikası hello küme otomatik olarak siler.</span><span class="sxs-lookup"><span data-stu-id="81ebb-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="81ebb-252">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="81ebb-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="81ebb-253">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="81ebb-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="81ebb-254">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-254">This behavior is by design.</span></span> <span data-ttu-id="81ebb-255">Mevcut canlı bir küme olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="81ebb-256">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="81ebb-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81ebb-257">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="81ebb-258">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="81ebb-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="81ebb-259">Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="81ebb-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="81ebb-260">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="81ebb-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="81ebb-261">Azure blob girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="81ebb-261">Azure blob input dataset</span></span>
<span data-ttu-id="81ebb-262">Merhaba girdi veri kümesi tanımında blob kapsayıcı, klasör ve hello giriş verisi içeren dosya hello adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="81ebb-263">Bkz: [Azure Blob veri kümesi özellikleri](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="81ebb-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="81ebb-264">Merhaba JSON tanımında belirli ayarları aşağıdaki hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="81ebb-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="81ebb-265">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="81ebb-265">Azure Blob output dataset</span></span>
<span data-ttu-id="81ebb-266">Merhaba çıkış veri kümesi tanımında blob kapsayıcısı ve hello çıktı verilerini tutan klasör hello adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="81ebb-267">Bkz: [Azure Blob veri kümesi özellikleri](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="81ebb-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="81ebb-268">Merhaba folderPath hello çıktı verilerini tutan hello yolu toohello klasörü belirtir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="81ebb-269">Merhaba [dataset kullanılabilirliği](../data-factory/data-factory-create-datasets.md#dataset-availability) ayarı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="81ebb-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="81ebb-270">Azure Data Factory'de dataset kullanılabilirliği sürücüleri hello ardışık düzeni çıkış.</span><span class="sxs-lookup"><span data-stu-id="81ebb-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="81ebb-271">Bu örnekte, hello dilim aylık (EndOfInterval) ayın son günü hello üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="81ebb-272">Daha fazla bilgi için bkz: [veri fabrikası zamanlama ve yürütme](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="81ebb-273">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="81ebb-273">Data pipeline</span></span>
<span data-ttu-id="81ebb-274">İsteğe bağlı Azure Hdınsight kümesinde bir Hive betiği çalıştırılarak verileri dönüştüren bir ardışık düzen tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="81ebb-275">Bkz: [ardışık düzen JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) JSON kullanılan öğeleri toodefine bu örnekteki işlem hattı açıklamaları için.</span><span class="sxs-lookup"><span data-stu-id="81ebb-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="81ebb-276">Merhaba ardışık bir etkinlik, Hdınsighthive etkinliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="81ebb-277">Yalnızca bir ay (bir dilim) işlenir için Ocak 2016'da, veri hem de başlangıç ve bitiş tarihleri gibi.</span><span class="sxs-lookup"><span data-stu-id="81ebb-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="81ebb-278">Her ikisi de *Başlat* ve *son* hello etkinliğini hello Data Factory hemen hello ay için verileri işleyen için geçmiş bir tarihe sahip.</span><span class="sxs-lookup"><span data-stu-id="81ebb-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="81ebb-279">Merhaba son gelecekteki bir tarih ise, başlangıç zamanı geldiğinde hello veri fabrikası başka bir dilim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="81ebb-280">Daha fazla bilgi için bkz: [veri fabrikası zamanlama ve yürütme](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="81ebb-281">Merhaba öğreticiyi silme</span><span class="sxs-lookup"><span data-stu-id="81ebb-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="81ebb-282">İsteğe bağlı Hdınsight kümesi tarafından oluşturulan hello blob kapsayıcıları Sil</span><span class="sxs-lookup"><span data-stu-id="81ebb-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="81ebb-283">Mevcut canlı bir küme (timeToLive); olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur ve hello küme hello işlem bittiğinde silinir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="81ebb-284">Her küme için Azure Data Factory hello Azure blob depolama hello varsayılan stroage hesap olarak hello kümesi için kullanılan bir blob kapsayıcısını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81ebb-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="81ebb-285">Hdınsight kümesi silindi olsa bile, hello varsayılan blob depolama kapsayıcısını ve ilişkili hello depolama hesabı silinmez.</span><span class="sxs-lookup"><span data-stu-id="81ebb-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="81ebb-286">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-286">This behavior is by design.</span></span> <span data-ttu-id="81ebb-287">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="81ebb-288">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="81ebb-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="81ebb-289">Bu kapsayıcıların Hello adları izleyen bir desen: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="81ebb-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="81ebb-290">Merhaba silme **adfjobs** ve **adfyourdatafactoryname linkedservicename datetimestamp** klasörler.</span><span class="sxs-lookup"><span data-stu-id="81ebb-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="81ebb-291">Merhaba adfjobs kapsayıcısı Azure Data Factory iş günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="81ebb-292">Merhaba kaynak grubunu silme</span><span class="sxs-lookup"><span data-stu-id="81ebb-292">Delete hello resource group</span></span>
<span data-ttu-id="81ebb-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) kullanılan toodeploy olan yönetebilir ve çözümünüzün bir grup olarak izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="81ebb-294">Bir kaynak grubunu silme hello grup içindeki tüm hello bileşenleri siler.</span><span class="sxs-lookup"><span data-stu-id="81ebb-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="81ebb-295">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81ebb-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="81ebb-296">Tıklatın **kaynak grupları** hello sol bölmedeki.</span><span class="sxs-lookup"><span data-stu-id="81ebb-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="81ebb-297">PowerShell komut dosyasında oluşturulan hello kaynak grubu adı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="81ebb-298">Listelenen çok fazla kaynak grupları varsa hello filtresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ebb-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="81ebb-299">Merhaba kaynak grubu yeni bir dikey pencerede açar.</span><span class="sxs-lookup"><span data-stu-id="81ebb-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="81ebb-300">Merhaba üzerinde **kaynakları** kutucuğu elinizde hello varsayılan depolama hesabı ve diğer projelerle hello kaynak grubu paylaşmak sürece listelenen hello veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="81ebb-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="81ebb-301">Tıklatın **silmek** hello dikey hello üstte.</span><span class="sxs-lookup"><span data-stu-id="81ebb-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="81ebb-302">Bunun yapılması, hello depolama hesabı ve hello depolama hesabında depolanan hello verileri siler.</span><span class="sxs-lookup"><span data-stu-id="81ebb-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="81ebb-303">Merhaba kaynak grubu adı tooconfirm silme girin ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="81ebb-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="81ebb-304">Merhaba kaynak grubunu sildiğinizde toodelete hello depolama hesabı istemediğiniz durumda hello varsayılan depolama hesabından hello iş verilerini ayırarak mimarisi aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="81ebb-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="81ebb-305">Bu durumda, hello iş verileriyle hello depolama hesabı için bir kaynak grubuna sahip ve diğer kaynak grubu hello varsayılan depolama hesabı Hdınsight bağlantılı hizmeti ve hello veri fabrikası için hello.</span><span class="sxs-lookup"><span data-stu-id="81ebb-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="81ebb-306">Merhaba ikinci kaynak grubu sildiğinizde, hello iş veri depolama hesabı etkilemez.</span><span class="sxs-lookup"><span data-stu-id="81ebb-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="81ebb-307">toodo için:</span><span class="sxs-lookup"><span data-stu-id="81ebb-307">toodo so:</span></span>

* <span data-ttu-id="81ebb-308">Merhaba, Resource Manager şablonu Microsoft.DataFactory/datafactories kaynağında birlikte toohello en üst düzey kaynak grubu aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="81ebb-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="81ebb-309">Bir depolama hesabı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="81ebb-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="81ebb-310">Yeni bağlı hizmet noktası toohello yeni bir depolama hesabı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="81ebb-310">Add a new linked service point toohello new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="81ebb-311">Merhaba Hdınsight bağlantılı ondemand hizmeti ek dependsOn ve bir additionalLinkedServiceNames yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="81ebb-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="81ebb-312">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81ebb-312">Next steps</span></span>
<span data-ttu-id="81ebb-313">Bu makalede, öğrendiğiniz nasıl toouse Azure Data Factory toocreate isteğe bağlı Hdınsight kümesi tooprocess Hive işleri.</span><span class="sxs-lookup"><span data-stu-id="81ebb-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="81ebb-314">Daha fazla tooread:</span><span class="sxs-lookup"><span data-stu-id="81ebb-314">tooread more:</span></span>

* [<span data-ttu-id="81ebb-315">Hadoop Öğreticisi: Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="81ebb-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="81ebb-316">Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="81ebb-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="81ebb-317">Hdınsight belgeleri</span><span class="sxs-lookup"><span data-stu-id="81ebb-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="81ebb-318">Veri Fabrikası belgeleri</span><span class="sxs-lookup"><span data-stu-id="81ebb-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="81ebb-319">Ek</span><span class="sxs-lookup"><span data-stu-id="81ebb-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="81ebb-320">Azure CLI komut dosyası</span><span class="sxs-lookup"><span data-stu-id="81ebb-320">Azure CLI script</span></span>
<span data-ttu-id="81ebb-321">Azure PowerShell toodo hello öğretici kullanmak yerine, Azure CLI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ebb-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="81ebb-322">Azure CLI toouse yönergeleri izleyerek hello göredir önce Azure CLI yükleyin:</span><span class="sxs-lookup"><span data-stu-id="81ebb-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="81ebb-323">Azure CLI tooprepare hello depolama kullanan ve hello dosyaları kopyalayın</span><span class="sxs-lookup"><span data-stu-id="81ebb-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="81ebb-324">Merhaba kapsayıcı adı *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="81ebb-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="81ebb-325">Olduğu gibi tutun.</span><span class="sxs-lookup"><span data-stu-id="81ebb-325">Keep it as it is.</span></span> <span data-ttu-id="81ebb-326">Aksi takdirde tooupdate hello Resource Manager şablonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="81ebb-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="81ebb-327">Bu CLI betik yardıma gereksinim duyarsanız, bkz: [kullanma hello Azure Storage ile Azure CLI](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="81ebb-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
