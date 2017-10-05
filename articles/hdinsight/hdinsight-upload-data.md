---
title: "Hdınsight'ta Hadoop işleri için veri yükleme | Microsoft Docs"
description: "Karşıya yükleme ve Azure CLI, Azure Storage Gezgini, Azure PowerShell, Hadoop komut satırı veya Sqoop kullanarak hdınsight'ta Hadoop işleri için veri erişim hakkında bilgi edinin."
keywords: "etl hadoop alma verileri hadoop, hadoop veri yükleme"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="96e34-104">HDInsight'ta Hadoop işleri için veri yükleme</span><span class="sxs-lookup"><span data-stu-id="96e34-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="96e34-105">Azure Hdınsight tam özellikli Hadoop dağıtılmış dosya sistemi (HDFS) üzerinden Azure Blob Depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e34-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="96e34-106">HDFS uzantı olarak, müşteriler için sorunsuz bir deneyim sağlamak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="96e34-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="96e34-107">Doğrudan yönettiği veriler üzerinde çalışmak için Hadoop ekosistemi bileşenlerini tam kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e34-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="96e34-108">Azure Blob Depolama ve HDFS depolama verilerinin ve bu verileri hesaplamalar için iyileştirilmiş farklı dosya sistemleridir.</span><span class="sxs-lookup"><span data-stu-id="96e34-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="96e34-109">Azure Blob Depolama kullanmanın yararları hakkında bilgi için [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="96e34-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="96e34-110">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="96e34-110">**Prerequisites**</span></span>

<span data-ttu-id="96e34-111">Başlamadan önce aşağıdaki gereksinimleri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="96e34-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="96e34-112">Azure Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="96e34-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="96e34-113">Yönergeler için bkz: [Azure Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="96e34-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="96e34-114">Neden blob depolama?</span><span class="sxs-lookup"><span data-stu-id="96e34-114">Why blob storage?</span></span>
<span data-ttu-id="96e34-115">Azure Hdınsight kümeleri genellikle MapReduce işleri çalıştırmak için dağıtılan ve bu işleri tamamladıktan sonra kümeleri bırakılır.</span><span class="sxs-lookup"><span data-stu-id="96e34-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="96e34-116">HDFS veri tutma hesaplamalar tamamlandıktan sonra kümeleri bu verileri depolamak için pahalı bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="96e34-117">Azure Blob Depolama, yüksek oranda kullanılabilir, yüksek düzeyde ölçeklenebilir, yüksek kapasite, Hdınsight kullanılarak işlenmesi için verileri için düşük maliyetli ve paylaşılabilir depolama seçeneği değil.</span><span class="sxs-lookup"><span data-stu-id="96e34-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="96e34-118">Bir blob verileri depolamak için hesaplama verilerini kaybetmeden güvenle yayımlanması için kullanılan Hdınsight kümeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e34-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="96e34-119">Dizinler</span><span class="sxs-lookup"><span data-stu-id="96e34-119">Directories</span></span>
<span data-ttu-id="96e34-120">Azure Blob storage kapsayıcıları verileri anahtar/değer çiftleri olarak depolar ve dizin hiyerarşisi yok.</span><span class="sxs-lookup"><span data-stu-id="96e34-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="96e34-121">Ancak "/" karakterini anahtar adında bir dosyayı dizin yapısında depolanmış gibi görünmesini sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="96e34-122">Gerçek dizinleri varsa gibi Hdınsight bu görür.</span><span class="sxs-lookup"><span data-stu-id="96e34-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="96e34-123">Örneğin, bir blob'un anahtarı *input/log1.txt* şeklinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="96e34-124">Hiçbir gerçek "Giriş" dizini var, ancak anahtar adında "/" karakterini varlığı nedeniyle, bir dosya yolu görünümünü içeriyor.</span><span class="sxs-lookup"><span data-stu-id="96e34-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="96e34-125">Azure Explorer Araçları kullanırsanız, bu nedenle, bazı 0 bayt dosyaları fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e34-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="96e34-126">Bu dosyaları iki amaca hizmet eder:</span><span class="sxs-lookup"><span data-stu-id="96e34-126">These files serve two purposes:</span></span>

* <span data-ttu-id="96e34-127">Boş klasörleri varsa, bunlar klasörü varlığını işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="96e34-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="96e34-128">Azure Blob Depolama foo/çubuğu adlı bir blob varsa adlı bir klasörü olduğunu bilmek akıllı **foo**.</span><span class="sxs-lookup"><span data-stu-id="96e34-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="96e34-129">Ancak adlı boş bir klasör belirtmek için tek yolu **foo** yerinde bu özel 0 bayt dosya sağlayarak değil.</span><span class="sxs-lookup"><span data-stu-id="96e34-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="96e34-130">Bunlar, özellikle izinleri ve klasörleri sahiplerini Hadoop dosya sistemi için gerekli olan özel meta veriler basılı tutun.</span><span class="sxs-lookup"><span data-stu-id="96e34-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="96e34-131">Komut satırı yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="96e34-131">Command-line utilities</span></span>
<span data-ttu-id="96e34-132">Microsoft Azure Blob storage ile çalışmak için aşağıdaki yardımcı programlar sağlar:</span><span class="sxs-lookup"><span data-stu-id="96e34-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="96e34-133">Aracı</span><span class="sxs-lookup"><span data-stu-id="96e34-133">Tool</span></span> | <span data-ttu-id="96e34-134">Linux</span><span class="sxs-lookup"><span data-stu-id="96e34-134">Linux</span></span> | <span data-ttu-id="96e34-135">OS X</span><span class="sxs-lookup"><span data-stu-id="96e34-135">OS X</span></span> | <span data-ttu-id="96e34-136">Windows</span><span class="sxs-lookup"><span data-stu-id="96e34-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="96e34-137">[Azure komut satırı arabirimi][azurecli]</span><span class="sxs-lookup"><span data-stu-id="96e34-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="96e34-138">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-138">✔</span></span> |<span data-ttu-id="96e34-139">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-139">✔</span></span> |<span data-ttu-id="96e34-140">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-140">✔</span></span> |
| <span data-ttu-id="96e34-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="96e34-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="96e34-142">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-142">✔</span></span> |
| <span data-ttu-id="96e34-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="96e34-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="96e34-144">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-144">✔</span></span> |
| [<span data-ttu-id="96e34-145">Hadoop komutu</span><span class="sxs-lookup"><span data-stu-id="96e34-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="96e34-146">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-146">✔</span></span> |<span data-ttu-id="96e34-147">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-147">✔</span></span> |<span data-ttu-id="96e34-148">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="96e34-149">Azure CLI, Azure PowerShell ve AzCopy tüm edebilirsiniz dış azure'dan komutu yalnızca Hdınsight kümesinde kullanılabilir ve yalnızca yerel dosya sisteminden Azure Blob depolama alanına veri yükleme verir Hadoop kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="96e34-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96e34-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="96e34-151">Azure CLI Azure hizmetlerini yönetmenize olanak sağlayan platformlar arası bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="96e34-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="96e34-152">Verileri Azure Blob depolama alanına yüklemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="96e34-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="96e34-153">[Yükleme ve Mac, Linux ve Windows için Azure CLI yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="96e34-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="96e34-154">Bir komut istemi, bash ya da diğer kabuğunu açın ve Azure aboneliğinize kimliğini doğrulamak için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e34-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="96e34-155">İstendiğinde, aboneliğiniz için kullanıcı adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="96e34-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="96e34-156">Aboneliğiniz için depolama hesaplarını listelemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="96e34-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="96e34-157">Çalışmak istediğiniz blob içeren depolama hesabını seçin ve ardından bu hesap için anahtar almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="96e34-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="96e34-158">Bu döndürmelidir **birincil** ve **ikincil** anahtarları.</span><span class="sxs-lookup"><span data-stu-id="96e34-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="96e34-159">Kopya **birincil** sonraki adımlarda kullanılacak çünkü anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="96e34-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="96e34-160">Depolama hesabı blob kapsayıcılara listesini almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="96e34-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="96e34-161">Karşıya yükleme ve blob dosyalarını indirmek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="96e34-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="96e34-162">Bir dosyayı karşıya yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="96e34-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="96e34-163">Bir dosyayı indirmek için:</span><span class="sxs-lookup"><span data-stu-id="96e34-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="96e34-164">Her zaman aynı depolama hesabı ile çalışacaksınız hesabı belirtme yerine aşağıdaki ortam değişkenlerini ayarlama ve her komut için anahtar:</span><span class="sxs-lookup"><span data-stu-id="96e34-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="96e34-165">**AZURE\_depolama\_hesap**: depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="96e34-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="96e34-166">**AZURE\_depolama\_erişim\_anahtar**: depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="96e34-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="96e34-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="96e34-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="96e34-168">Azure PowerShell denetlemek ve dağıtımını ve yönetimini azure'da, iş yüklerini otomatikleştirmek için kullanabileceğiniz bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="96e34-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="96e34-169">Azure PowerShell'i çalıştırmak için iş istasyonunuzu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96e34-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="96e34-170">**Bir yerel dosyayı Azure Blob depolama alanına yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="96e34-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="96e34-171">Belirtildiği gibi Azure PowerShell konsolu açın [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96e34-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="96e34-172">Aşağıdaki komut dosyasında ilk beş değişkenlerin değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="96e34-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="96e34-173">Komut dosyasını çalıştırmak için dosyayı kopyalamak için Azure PowerShell konsolunda yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="96e34-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="96e34-174">Örneğin bkz: Hdınsight ile çalışmak için oluşturulan PowerShell komut dosyalarını [Hdınsight Araçları](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="96e34-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="96e34-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="96e34-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="96e34-176">AzCopy içine ve dışına bir Azure Storage hesabı veri aktarma görevini kolaylaştırmak için tasarlanmış bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="96e34-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="96e34-177">Ayrı bir araç olarak kullanabilir veya varolan bir uygulama bu aracı içerecek.</span><span class="sxs-lookup"><span data-stu-id="96e34-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="96e34-178">[AzCopy karşıdan][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="96e34-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="96e34-179">AzCopy sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="96e34-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="96e34-180">Daha fazla bilgi için bkz: [dosyaları Azure BLOB'ları için karşıya yükleme/indirme AzCopy -][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="96e34-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="96e34-181"><a id="commandline"></a>Hadoop komut satırı</span><span class="sxs-lookup"><span data-stu-id="96e34-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="96e34-182">Hadoop komut satırı, yalnızca veri kümesi baş düğümünde zaten geldiğinde, verileri blob depolama alanına depolamak için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="96e34-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="96e34-183">Hadoop komutu kullanmak için aşağıdaki yöntemlerden birini kullanarak headnode bağlanın:</span><span class="sxs-lookup"><span data-stu-id="96e34-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="96e34-184">**Windows tabanlı Hdınsight**: [Uzak Masaüstü kullanarak bağlan](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="96e34-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="96e34-185">**Linux tabanlı Hdınsight**: SSH kullanarak bağlan ([SSH komutu](hdinsight-hadoop-linux-use-ssh-unix.md) veya [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="96e34-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="96e34-186">Bağlantı kurulduktan sonra bir dosya depolama alanına yüklemek için aşağıdaki söz dizimini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e34-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="96e34-187">Örneğin, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="96e34-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="96e34-188">Hdınsight için varsayılan dosya sistemi Azure Blob depolama alanına olduğundan, /example/data.txt gerçekte Azure Blob depolama alanına değildir.</span><span class="sxs-lookup"><span data-stu-id="96e34-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="96e34-189">Dosyasına olarak başvurabilir:</span><span class="sxs-lookup"><span data-stu-id="96e34-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="96e34-190">or</span><span class="sxs-lookup"><span data-stu-id="96e34-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="96e34-191">Diğer Hadoop listesini dosyalarıyla çalışan komutlar için bkz: [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="96e34-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="96e34-192">HBase kümelerinde varsayılan bloğu boyutunu veri yazma 256 KB olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="96e34-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="96e34-193">Bu HBase API'lerini veya REST API'leri kullanırken düzgün çalışır, ancak kullanarak `hadoop` veya `hdfs dfs` ~ 12 GB'den büyük veri hatayla sonuçlanır yazmak için komutları.</span><span class="sxs-lookup"><span data-stu-id="96e34-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="96e34-194">Bkz: [blob yazma için depolama özel durumu](#storageexception) daha fazla bilgi için bölüm aşağıda.</span><span class="sxs-lookup"><span data-stu-id="96e34-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="96e34-195">Grafik istemcileri</span><span class="sxs-lookup"><span data-stu-id="96e34-195">Graphical clients</span></span>
<span data-ttu-id="96e34-196">Azure Storage ile çalışmak için bir grafik arabirim sağlayan birkaç uygulamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="96e34-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="96e34-197">Bu uygulamalar bazılarını listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="96e34-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="96e34-198">İstemci</span><span class="sxs-lookup"><span data-stu-id="96e34-198">Client</span></span> | <span data-ttu-id="96e34-199">Linux</span><span class="sxs-lookup"><span data-stu-id="96e34-199">Linux</span></span> | <span data-ttu-id="96e34-200">OS X</span><span class="sxs-lookup"><span data-stu-id="96e34-200">OS X</span></span> | <span data-ttu-id="96e34-201">Windows</span><span class="sxs-lookup"><span data-stu-id="96e34-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="96e34-202">Hdınsight için Microsoft Visual Studio Araçları</span><span class="sxs-lookup"><span data-stu-id="96e34-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="96e34-203">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-203">✔</span></span> |<span data-ttu-id="96e34-204">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-204">✔</span></span> |<span data-ttu-id="96e34-205">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-205">✔</span></span> |
| [<span data-ttu-id="96e34-206">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="96e34-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="96e34-207">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-207">✔</span></span> |<span data-ttu-id="96e34-208">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-208">✔</span></span> |<span data-ttu-id="96e34-209">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-209">✔</span></span> |
| [<span data-ttu-id="96e34-210">Bulut depolama Studio 2</span><span class="sxs-lookup"><span data-stu-id="96e34-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="96e34-211">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-211">✔</span></span> |
| [<span data-ttu-id="96e34-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="96e34-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="96e34-213">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-213">✔</span></span> |
| [<span data-ttu-id="96e34-214">Azure Gezgini</span><span class="sxs-lookup"><span data-stu-id="96e34-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="96e34-215">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-215">✔</span></span> |
| [<span data-ttu-id="96e34-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="96e34-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="96e34-217">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-217">✔</span></span> |<span data-ttu-id="96e34-218">✔</span><span class="sxs-lookup"><span data-stu-id="96e34-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="96e34-219">Hdınsight için Visual Studio Araçları</span><span class="sxs-lookup"><span data-stu-id="96e34-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="96e34-220">Daha fazla bilgi için bkz: [bağlı kaynaklara gitme](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="96e34-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="96e34-221"><a id="storageexplorer"></a>Azure Storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="96e34-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="96e34-222">*Azure Storage Gezgini* inceleme ve BLOB verileri değiştirme için yararlı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="96e34-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="96e34-223">Bu, yüklenebilir bir ücretsiz, açık kaynak aracıdır [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="96e34-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="96e34-224">Kaynak kodu, bu bağlantıdan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="96e34-225">Aracı'nı kullanmadan önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e34-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="96e34-226">Bu bilgi alma hakkında yönergeler için bkz: "nasıl yapılır: erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama" bölümünü [oluşturun, yönetmek veya bir depolama hesabını silmek][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="96e34-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="96e34-227">Azure Storage Gezgini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96e34-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="96e34-228">Bu ilk kez kullanıyorsanız Depolama Gezgini'ni çalıştırmak, için istenir **_vm hesap adı** ve **depolama hesabı anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="96e34-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="96e34-229">Daha önce çalıştırdıysanız kullanmak **Ekle** bir yeni depolama hesabı adı ve anahtar eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="96e34-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="96e34-230">Bir ad girin ve Hdınsight küme tarafından kullanılan depolama hesabı için anahtarını ve ardından **Aç & Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="96e34-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="96e34-232">Arabirim solundaki kapsayıcıları listesinde, Hdınsight kümenizle ilişkilendirilmiş kapsayıcının adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="96e34-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="96e34-233">Varsayılan olarak, bu Hdınsight kümenizin adıdır, ancak küme oluştururken, belirli bir ad girdiyseniz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="96e34-234">Araç Çubuğu'ndan karşıya yükleme simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="96e34-234">From the tool bar, select the upload icon.</span></span>

    ![Araç çubuğu vurgulanmış karşıya yükleme simgesi](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="96e34-236">Dosyayı karşıya yükleyin ve ardından belirtin **açık**.</span><span class="sxs-lookup"><span data-stu-id="96e34-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="96e34-237">İstendiğinde, seçin **karşıya** depolama kapsayıcısı köküne dosya karşıya.</span><span class="sxs-lookup"><span data-stu-id="96e34-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="96e34-238">Belirli bir yola dosyayı karşıya yüklemek istediğiniz yolu girin **hedef** alan ve ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="96e34-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Dosya yükleme iletişim kutusu](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="96e34-240">Dosyayı karşıya yüklemeyi tamamladığında, Hdınsight kümesinde işleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e34-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="96e34-241">Azure Blob Depolama Birimi yerel sürücü olarak bağlama</span><span class="sxs-lookup"><span data-stu-id="96e34-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="96e34-242">Bkz: [bağlama Azure Blob Storage yerel sürücü olarak](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="96e34-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="96e34-243">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="96e34-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="96e34-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="96e34-244">Azure Data Factory</span></span>
<span data-ttu-id="96e34-245">Azure Data Factory hizmetinin kolaylaştırılmış, ölçeklenebilir ve güvenilir veri üretim ardışık düzenlerle veri depolama, veri işleme ve veri taşıma hizmetleri oluşturmak için tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="96e34-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="96e34-246">Azure Data Factory, verileri Azure Blob depolama alanına taşıyabilir veya doğrudan Hdınsight özelliklerine Hive veya Pig gibi veri ardışık düzen oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e34-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="96e34-247">Daha fazla bilgi için bkz: [Azure Data Factory belgelerine](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="96e34-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="96e34-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="96e34-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="96e34-249">Sqoop, Hadoop ve ilişkisel veritabanları arasında veri aktarmak için tasarlanmış bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="96e34-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="96e34-250">SQL Server, MySQL ve Oracle Hadoop dağıtılmış dosya sistemi (HDFS) içine Hadoop ile MapReduce veya Hive verilerde dönüştürme ve bir RDBMS verileri dışarı aktarma gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS), veri aktarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e34-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="96e34-251">Daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="96e34-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="96e34-252">Geliştirme SDK'ları</span><span class="sxs-lookup"><span data-stu-id="96e34-252">Development SDKs</span></span>
<span data-ttu-id="96e34-253">Azure Blob Depolama aynı zamanda aşağıdaki programlama dillerini bir Azure SDK kullanılarak erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="96e34-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="96e34-254">.NET</span><span class="sxs-lookup"><span data-stu-id="96e34-254">.NET</span></span>
* <span data-ttu-id="96e34-255">Java</span><span class="sxs-lookup"><span data-stu-id="96e34-255">Java</span></span>
* <span data-ttu-id="96e34-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="96e34-256">Node.js</span></span>
* <span data-ttu-id="96e34-257">PHP</span><span class="sxs-lookup"><span data-stu-id="96e34-257">PHP</span></span>
* <span data-ttu-id="96e34-258">Python</span><span class="sxs-lookup"><span data-stu-id="96e34-258">Python</span></span>
* <span data-ttu-id="96e34-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="96e34-259">Ruby</span></span>

<span data-ttu-id="96e34-260">Azure SDK'ları yükleme hakkında daha fazla bilgi için bkz: [Azure indirir](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="96e34-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="96e34-261">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="96e34-261">Troubleshooting</span></span>
### <span data-ttu-id="96e34-262"><a id="storageexception"></a>Blob yazma için depolama özel durumu</span><span class="sxs-lookup"><span data-stu-id="96e34-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="96e34-263">**Belirtiler**: kullanırken `hadoop` veya `hdfs dfs` ~ 12 GB olan dosyaları yazmak için komutları veya daha büyük bir HBase kümesi üzerinde aşağıdaki hatalardan biriyle karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="96e34-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="96e34-264">**Neden**: hdınsight'ta HBase Azure depolama alanına yazılırken bu varsayılan bir blok boyutu 256 KB kümeleri.</span><span class="sxs-lookup"><span data-stu-id="96e34-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="96e34-265">Bu HBase API'lerini veya REST API'leri için çalışırken, onu bir hatayla kullanırken sonuçlanır `hadoop` veya `hdfs dfs` komut satırı yardımcı programları.</span><span class="sxs-lookup"><span data-stu-id="96e34-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="96e34-266">**Çözümleme**: kullanım `fs.azure.write.request.size` daha büyük bir blok boyutu belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="96e34-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="96e34-267">Bir kullanım başına temelinde kullanarak bunu yapabilirsiniz `-D` parametresi.</span><span class="sxs-lookup"><span data-stu-id="96e34-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="96e34-268">Bu parametre ile kullanan bir örnek verilmiştir `hadoop` komutu:</span><span class="sxs-lookup"><span data-stu-id="96e34-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="96e34-269">Değerini de artırabilirsiniz `fs.azure.write.request.size` Ambari kullanarak genel.</span><span class="sxs-lookup"><span data-stu-id="96e34-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="96e34-270">Aşağıdaki adımlar, Ambari Web kullanıcı arabirimini değerini değiştirmek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="96e34-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="96e34-271">Tarayıcınızda, kümeniz için Ambari Web kullanıcı arabirimini gidin.</span><span class="sxs-lookup"><span data-stu-id="96e34-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="96e34-272">Https://CLUSTERNAME.azurehdinsight.net, budur nerede **CLUSTERNAME** kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="96e34-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="96e34-273">İstendiğinde, küme için Yönetici adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="96e34-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="96e34-274">Ekranın sol taraftan seçin **HDFS**ve ardından **yapılandırmalar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="96e34-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="96e34-275">İçinde **filtre...**  alanına, `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="96e34-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="96e34-276">Bu alanı ve sayfa ortasında geçerli değeri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="96e34-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="96e34-277">Değer 262144 (256 KB) yeni değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96e34-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="96e34-278">Örneğin, 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="96e34-278">For example, 4194304 (4MB).</span></span>

![Ambari Web kullanıcı Arabirimi aracılığıyla değeri değiştirme resmi](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="96e34-280">Ambari kullanarak daha fazla bilgi için bkz: [Ambari Web kullanıcı arabirimini kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="96e34-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96e34-281">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96e34-281">Next steps</span></span>
<span data-ttu-id="96e34-282">Verileri Hdınsight'a alma nasıl anladığınıza göre Analiz gerçekleştirme hakkında bilgi edinmek için aşağıdaki makalelere okuyun:</span><span class="sxs-lookup"><span data-stu-id="96e34-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="96e34-283">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="96e34-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="96e34-284">[Hadoop işlerini programlı olarak gönderme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="96e34-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="96e34-285">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="96e34-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="96e34-286">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="96e34-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
