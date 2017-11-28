---
title: "hdınsight'ta Hadoop işleri için aaaUpload verileri | Microsoft Docs"
description: "Azure CLI, Azure Storage Gezgini, Azure PowerShell, hello Hadoop komut satırı veya Sqoop kullanarak Hdınsight'ta Hadoop işleri için tooupload ve erişim verileri nasıl hello öğrenin."
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
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="9305c-104">HDInsight'ta Hadoop işleri için veri yükleme</span><span class="sxs-lookup"><span data-stu-id="9305c-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="9305c-105">Azure Hdınsight tam özellikli Hadoop dağıtılmış dosya sistemi (HDFS) üzerinden Azure Blob Depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="9305c-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="9305c-106">Bunun tasarlandığından toocustomers bir HDFS uzantısı tooprovide sorunsuz bir deneyim.</span><span class="sxs-lookup"><span data-stu-id="9305c-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="9305c-107">Merhaba Hadoop ekosistemi toooperate doğrudan yönettiği hello verileri bileşenlerinde hello kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9305c-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="9305c-108">Azure Blob Depolama ve HDFS depolama verilerinin ve bu verileri hesaplamalar için iyileştirilmiş farklı dosya sistemleridir.</span><span class="sxs-lookup"><span data-stu-id="9305c-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="9305c-109">Azure Blob storage kullanma hello yararları hakkında bilgi için [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="9305c-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="9305c-110">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="9305c-110">**Prerequisites**</span></span>

<span data-ttu-id="9305c-111">Başlamadan önce aşağıdaki gereksinim hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9305c-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="9305c-112">Azure Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="9305c-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="9305c-113">Yönergeler için bkz: [Azure Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="9305c-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="9305c-114">Neden blob depolama?</span><span class="sxs-lookup"><span data-stu-id="9305c-114">Why blob storage?</span></span>
<span data-ttu-id="9305c-115">Azure Hdınsight kümeleri genellikle olan toorun MapReduce işleri dağıtılır ve bu işlemler tamamlandıktan sonra hello kümeleri bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9305c-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="9305c-116">Hesaplamalar tamamlandıktan sonra hello HDFS kümelerde hello veri tutma pahalı yolu toostore bu verileri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9305c-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="9305c-117">Azure Blob Depolama, yüksek oranda kullanılabilir, yüksek düzeyde ölçeklenebilir, yüksek kapasite, Hdınsight kullanarak işlenen toobe veriler için düşük maliyetli ve paylaşılabilir depolama seçeneği değil.</span><span class="sxs-lookup"><span data-stu-id="9305c-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="9305c-118">Bir blob verileri depolamak verilerini kaybetmeden güvenle yayımlanan hesaplama toobe için kullanılan hello Hdınsight kümeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9305c-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="9305c-119">Dizinler</span><span class="sxs-lookup"><span data-stu-id="9305c-119">Directories</span></span>
<span data-ttu-id="9305c-120">Azure Blob storage kapsayıcıları verileri anahtar/değer çiftleri olarak depolar ve dizin hiyerarşisi yok.</span><span class="sxs-lookup"><span data-stu-id="9305c-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="9305c-121">Ancak hello "/" karakteri görünür bir dosyayı dizin yapısında depolanmış gibi hello anahtar adı toomake içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9305c-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="9305c-122">Gerçek dizinleri varsa gibi Hdınsight bu görür.</span><span class="sxs-lookup"><span data-stu-id="9305c-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="9305c-123">Örneğin, bir blob'un anahtarı *input/log1.txt* şeklinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="9305c-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="9305c-124">Hiçbir gerçek "Giriş" dizini var, ancak hello toohello varlığını son "/" karakterini hello anahtar adı, bir dosya yolu hello görünümünü içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9305c-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="9305c-125">Azure Explorer Araçları kullanırsanız, bu nedenle, bazı 0 bayt dosyaları fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9305c-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="9305c-126">Bu dosyaları iki amaca hizmet eder:</span><span class="sxs-lookup"><span data-stu-id="9305c-126">These files serve two purposes:</span></span>

* <span data-ttu-id="9305c-127">Boş klasörleri varsa, bunlar hello klasörü hello varlığını işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="9305c-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="9305c-128">Azure Blob Depolama birimi olan foo/çubuğu adlı bir blob varsa adlı bir klasör yok akıllı tooknow **foo**.</span><span class="sxs-lookup"><span data-stu-id="9305c-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="9305c-129">Ancak boş bir klasör olarak adlandırılan tek yolu toosignify hello **foo** yerinde bu özel 0 bayt dosya sağlayarak değil.</span><span class="sxs-lookup"><span data-stu-id="9305c-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="9305c-130">Bunlar, özel meta verileri Hadoop hello tarafından özellikle hello izinleri ve sahiplerine hello klasörler için dosya sistemi basılı tutun.</span><span class="sxs-lookup"><span data-stu-id="9305c-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="9305c-131">Komut satırı yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="9305c-131">Command-line utilities</span></span>
<span data-ttu-id="9305c-132">Microsoft Azure Blob storage ile yardımcı programları toowork aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="9305c-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="9305c-133">Aracı</span><span class="sxs-lookup"><span data-stu-id="9305c-133">Tool</span></span> | <span data-ttu-id="9305c-134">Linux</span><span class="sxs-lookup"><span data-stu-id="9305c-134">Linux</span></span> | <span data-ttu-id="9305c-135">OS X</span><span class="sxs-lookup"><span data-stu-id="9305c-135">OS X</span></span> | <span data-ttu-id="9305c-136">Windows</span><span class="sxs-lookup"><span data-stu-id="9305c-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="9305c-137">[Azure komut satırı arabirimi][azurecli]</span><span class="sxs-lookup"><span data-stu-id="9305c-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="9305c-138">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-138">✔</span></span> |<span data-ttu-id="9305c-139">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-139">✔</span></span> |<span data-ttu-id="9305c-140">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-140">✔</span></span> |
| <span data-ttu-id="9305c-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="9305c-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="9305c-142">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-142">✔</span></span> |
| <span data-ttu-id="9305c-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="9305c-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="9305c-144">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-144">✔</span></span> |
| [<span data-ttu-id="9305c-145">Hadoop komutu</span><span class="sxs-lookup"><span data-stu-id="9305c-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="9305c-146">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-146">✔</span></span> |<span data-ttu-id="9305c-147">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-147">✔</span></span> |<span data-ttu-id="9305c-148">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="9305c-149">Hello Azure CLI, Azure PowerShell ve AzCopy tüm edebilirsiniz dış azure'dan hello komutu yalnızca hello Hdınsight kümesinde kullanılabilir ve yalnızca Azure Blob depolama alanına hello yerel dosya sisteminden verileri yüklenirken verir Hadoop kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9305c-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="9305c-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9305c-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="9305c-151">Hello Azure CLI toomanage Azure sağlayan bir araçtır platformlar arası Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="9305c-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="9305c-152">Aşağıdaki adımları tooupload veri tooAzure Blob Depolama hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9305c-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="9305c-153">[Yükleme ve Mac, Linux ve Windows hello Azure CLI yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9305c-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="9305c-154">Bir komut istemi, bash ya da diğer kabuğunu açın ve tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9305c-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="9305c-155">İstendiğinde, aboneliğiniz için hello kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="9305c-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="9305c-156">Komut toolist hello depolama hesapları, aboneliğiniz için aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="9305c-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="9305c-157">Merhaba blob ile toowork istediğiniz içeren hello depolama hesabını seçin, sonra komutu tooretrieve hello anahtarı bu hesap için aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9305c-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="9305c-158">Bu döndürmelidir **birincil** ve **ikincil** anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9305c-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="9305c-159">Kopya hello **birincil** hello sonraki adımlarda kullanılacak çünkü anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="9305c-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="9305c-160">Komut tooretrieve hello depolama hesabındaki blob kapsayıcılar listesi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9305c-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="9305c-161">Dosyaları toohello blob indirmek ve aşağıdaki komutları tooupload hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9305c-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="9305c-162">bir dosya tooupload:</span><span class="sxs-lookup"><span data-stu-id="9305c-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="9305c-163">bir dosya toodownload:</span><span class="sxs-lookup"><span data-stu-id="9305c-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="9305c-164">Her zaman hello ile aynı çalışacaksınız, depolama hesabı ayarlama hello hesabı belirtme yerine ortam değişkenleri aşağıdaki hello ve anahtar her komut için:</span><span class="sxs-lookup"><span data-stu-id="9305c-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="9305c-165">**AZURE\_depolama\_hesap**: hello depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="9305c-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="9305c-166">**AZURE\_depolama\_erişim\_anahtar**: hello depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="9305c-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="9305c-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9305c-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="9305c-168">Azure PowerShell toocontrol kullanın ve hello dağıtımı ve Yönetimi azure'da iş yüklerinizin otomatikleştirmek bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="9305c-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="9305c-169">İş istasyonu toorun Azure PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9305c-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="9305c-170">**tooupload bir yerel dosya tooAzure Blob Depolama**</span><span class="sxs-lookup"><span data-stu-id="9305c-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="9305c-171">Belirtildiği gibi açık hello Azure PowerShell konsolunda [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9305c-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="9305c-172">Merhaba hello ilk beş değişkenleri komut dosyası izleyen hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9305c-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="9305c-173">Yapıştır hello komut dosyası hello Azure PowerShell konsol toorun onu toocopy hello dosya.</span><span class="sxs-lookup"><span data-stu-id="9305c-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="9305c-174">Örneğin, Hdınsight ile PowerShell oluşturulan komut dosyalarını toowork bkz [Hdınsight Araçları](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="9305c-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="9305c-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="9305c-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="9305c-176">AzCopy, bir komut satırı aracını içine ve dışına bir Azure Storage hesabı veri aktarma toosimplify hello görev tasarlanmış ' dir.</span><span class="sxs-lookup"><span data-stu-id="9305c-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="9305c-177">Ayrı bir araç olarak kullanabilir veya varolan bir uygulama bu aracı içerecek.</span><span class="sxs-lookup"><span data-stu-id="9305c-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="9305c-178">[AzCopy karşıdan][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="9305c-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="9305c-179">Merhaba AzCopy söz dizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9305c-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="9305c-180">Daha fazla bilgi için bkz: [dosyaları Azure BLOB'ları için karşıya yükleme/indirme AzCopy -][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="9305c-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="9305c-181"><a id="commandline"></a>Hadoop komut satırı</span><span class="sxs-lookup"><span data-stu-id="9305c-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="9305c-182">Merhaba Hadoop komut satırı, yalnızca hello veri hello küme baş düğümünde zaten geldiğinde, verileri blob depolama alanına depolamak için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9305c-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="9305c-183">Sipariş toouse hello Hadoop komutu, yöntemler aşağıdaki hello birini kullanarak toohello headnode önce bağlanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9305c-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="9305c-184">**Windows tabanlı Hdınsight**: [Uzak Masaüstü kullanarak bağlan](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="9305c-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="9305c-185">**Linux tabanlı Hdınsight**: SSH kullanarak bağlan ([SSH komutu hello](hdinsight-hadoop-linux-use-ssh-unix.md) veya [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="9305c-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="9305c-186">Bağlantı kurulduktan sonra aşağıdaki sözdizimi tooupload dosya toostorage hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9305c-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="9305c-187">Örneğin, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="9305c-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="9305c-188">Merhaba varsayılan dosya sistemi Hdınsight için Azure Blob depolama alanına olduğundan, /example/data.txt gerçekte Azure Blob depolama alanına değildir.</span><span class="sxs-lookup"><span data-stu-id="9305c-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="9305c-189">Toohello dosyası olarak da başvurabilir:</span><span class="sxs-lookup"><span data-stu-id="9305c-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="9305c-190">or</span><span class="sxs-lookup"><span data-stu-id="9305c-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="9305c-191">Diğer Hadoop listesini dosyalarıyla çalışan komutlar için bkz: [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="9305c-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="9305c-192">Veri yazma 256 KB HBase kümelerinde hello varsayılan blok boyutu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9305c-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="9305c-193">Merhaba kullanırken bu HBase API'lerini veya REST API'leri kullanırken düzgün çalışır, `hadoop` veya `hdfs dfs` komutları toowrite veri ~ 12 GB'den büyük hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="9305c-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="9305c-194">Merhaba bkz [blob yazma için depolama özel durumu](#storageexception) daha fazla bilgi için bölüm aşağıda.</span><span class="sxs-lookup"><span data-stu-id="9305c-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="9305c-195">Grafik istemcileri</span><span class="sxs-lookup"><span data-stu-id="9305c-195">Graphical clients</span></span>
<span data-ttu-id="9305c-196">Azure Storage ile çalışmak için bir grafik arabirim sağlayan birkaç uygulamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="9305c-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="9305c-197">Merhaba, bu uygulamaları birkaç listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9305c-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="9305c-198">İstemci</span><span class="sxs-lookup"><span data-stu-id="9305c-198">Client</span></span> | <span data-ttu-id="9305c-199">Linux</span><span class="sxs-lookup"><span data-stu-id="9305c-199">Linux</span></span> | <span data-ttu-id="9305c-200">OS X</span><span class="sxs-lookup"><span data-stu-id="9305c-200">OS X</span></span> | <span data-ttu-id="9305c-201">Windows</span><span class="sxs-lookup"><span data-stu-id="9305c-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="9305c-202">Hdınsight için Microsoft Visual Studio Araçları</span><span class="sxs-lookup"><span data-stu-id="9305c-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="9305c-203">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-203">✔</span></span> |<span data-ttu-id="9305c-204">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-204">✔</span></span> |<span data-ttu-id="9305c-205">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-205">✔</span></span> |
| [<span data-ttu-id="9305c-206">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="9305c-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="9305c-207">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-207">✔</span></span> |<span data-ttu-id="9305c-208">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-208">✔</span></span> |<span data-ttu-id="9305c-209">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-209">✔</span></span> |
| [<span data-ttu-id="9305c-210">Bulut depolama Studio 2</span><span class="sxs-lookup"><span data-stu-id="9305c-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="9305c-211">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-211">✔</span></span> |
| [<span data-ttu-id="9305c-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="9305c-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="9305c-213">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-213">✔</span></span> |
| [<span data-ttu-id="9305c-214">Azure Gezgini</span><span class="sxs-lookup"><span data-stu-id="9305c-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="9305c-215">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-215">✔</span></span> |
| [<span data-ttu-id="9305c-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="9305c-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="9305c-217">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-217">✔</span></span> |<span data-ttu-id="9305c-218">✔</span><span class="sxs-lookup"><span data-stu-id="9305c-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="9305c-219">Hdınsight için Visual Studio Araçları</span><span class="sxs-lookup"><span data-stu-id="9305c-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="9305c-220">Daha fazla bilgi için bkz: [Bul hello bağlı kaynakları](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="9305c-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="9305c-221"><a id="storageexplorer"></a>Azure Storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="9305c-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="9305c-222">*Azure Storage Gezgini* inceleme ve BLOB'lar hello verileri değiştirme için yararlı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="9305c-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="9305c-223">Bu, yüklenebilir bir ücretsiz, açık kaynak aracıdır [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9305c-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="9305c-224">Merhaba kaynak kodu, bu bağlantıdan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9305c-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="9305c-225">Merhaba aracını kullanmadan önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9305c-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="9305c-226">Hello bu bilgileri alma hakkında yönergeler için bkz "nasıl yapılır: erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama" bölümünü [oluşturma, yönetme veya bir depolama hesabı silme][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="9305c-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="9305c-227">Azure Storage Gezgini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9305c-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="9305c-228">Bu ilk kez hello ise hello Depolama Gezgini'ni çalıştırmak, Merhaba istenir **_vm hesap adı** ve **depolama hesabı anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="9305c-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="9305c-229">Daha önce çalıştırdıysanız, hello kullan **Ekle** düğmesini tooadd yeni depolama hesabı adı ve anahtar.</span><span class="sxs-lookup"><span data-stu-id="9305c-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="9305c-230">Merhaba adını ve Hdınsight küme tarafından kullanılan hello depolama hesabı için anahtar ve seçip girin **Aç & Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="9305c-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="9305c-232">Kapsayıcıları toohello hello arabirimi solundaki Hello listesinde Hdınsight kümenizle ilişkilendirilmiş hello kapsayıcı hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9305c-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="9305c-233">Varsayılan olarak, bu hello hello Hdınsight kümenizin adıdır, ancak belirli bir ad hello kümesi oluştururken girdiyseniz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9305c-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="9305c-234">Merhaba araç çubuğundan hello karşıya yükleme simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9305c-234">From hello tool bar, select hello upload icon.</span></span>

    ![Araç çubuğu vurgulanmış karşıya yükleme simgesi](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="9305c-236">Bir dosya tooupload belirtin ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="9305c-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="9305c-237">İstendiğinde, seçin **karşıya** tooupload hello dosya toohello kök hello depolama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9305c-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="9305c-238">Tooupload hello dosya tooa belirli yolu istiyorsanız hello hello yolu girin **hedef** alan ve ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="9305c-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Dosya yükleme iletişim kutusu](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="9305c-240">Merhaba dosya karşıya yükleme tamamlandıktan sonra hello Hdınsight kümesinde işleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9305c-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="9305c-241">Azure Blob Depolama Birimi yerel sürücü olarak bağlama</span><span class="sxs-lookup"><span data-stu-id="9305c-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="9305c-242">Bkz: [bağlama Azure Blob Storage yerel sürücü olarak](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="9305c-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="9305c-243">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="9305c-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="9305c-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9305c-244">Azure Data Factory</span></span>
<span data-ttu-id="9305c-245">Hello Azure Data Factory hizmetine kolaylaştırılmış, ölçeklenebilir ve güvenilir veri üretim ardışık düzenlerle veri depolama, veri işleme ve veri taşıma hizmetleri oluşturmak için tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="9305c-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="9305c-246">Azure Data Factory kullanılan toomove veriler Azure Blob depolama alanına olabilir veya doğrudan Hdınsight gibi özelliklerine toocreate veri ardışık Hive veya Pig.</span><span class="sxs-lookup"><span data-stu-id="9305c-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="9305c-247">Daha fazla bilgi için bkz: Merhaba [Azure Data Factory belgelerine](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="9305c-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="9305c-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="9305c-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="9305c-249">Sqoop, Hadoop ve ilişkisel veritabanları arasında tasarlanmış aracı tootransfer verilerdir.</span><span class="sxs-lookup"><span data-stu-id="9305c-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="9305c-250">SQL Server, MySQL veya Oracle hello Hadoop dağıtılmış dosya sistemi (HDFS) içine dönüştürme hello verileri Hadoop ile MapReduce veya Hive ve uygulamasına geri hello verileri dışarı aktarma gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) tooimport verilerden kullanabilirsiniz bir RDBMS.</span><span class="sxs-lookup"><span data-stu-id="9305c-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="9305c-251">Daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="9305c-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="9305c-252">Geliştirme SDK'ları</span><span class="sxs-lookup"><span data-stu-id="9305c-252">Development SDKs</span></span>
<span data-ttu-id="9305c-253">Azure Blob Depolama, programlama dilleri aşağıdaki hello bir Azure SDK kullanarak da erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="9305c-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="9305c-254">.NET</span><span class="sxs-lookup"><span data-stu-id="9305c-254">.NET</span></span>
* <span data-ttu-id="9305c-255">Java</span><span class="sxs-lookup"><span data-stu-id="9305c-255">Java</span></span>
* <span data-ttu-id="9305c-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="9305c-256">Node.js</span></span>
* <span data-ttu-id="9305c-257">PHP</span><span class="sxs-lookup"><span data-stu-id="9305c-257">PHP</span></span>
* <span data-ttu-id="9305c-258">Python</span><span class="sxs-lookup"><span data-stu-id="9305c-258">Python</span></span>
* <span data-ttu-id="9305c-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="9305c-259">Ruby</span></span>

<span data-ttu-id="9305c-260">Hello Azure SDK'ları yükleme hakkında daha fazla bilgi için bkz: [Azure indirir](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="9305c-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9305c-261">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9305c-261">Troubleshooting</span></span>
### <span data-ttu-id="9305c-262"><a id="storageexception"></a>Blob yazma için depolama özel durumu</span><span class="sxs-lookup"><span data-stu-id="9305c-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="9305c-263">**Belirtiler**: hello kullanırken `hadoop` veya `hdfs dfs` toowrite dosyaları ~ 12 GB komutlardır veya daha büyük bir HBase kümesi üzerinde aşağıdaki hata hello karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9305c-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="9305c-264">**Neden**: hdınsight'ta HBase kümeleri varsayılan tooa blok boyutu 256 KB tooAzure depolama yazılırken.</span><span class="sxs-lookup"><span data-stu-id="9305c-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="9305c-265">Bu HBase API'lerini veya REST API'leri için çalışırken, onu bir hatayla hello kullanırken sonuçlanır `hadoop` veya `hdfs dfs` komut satırı yardımcı programları.</span><span class="sxs-lookup"><span data-stu-id="9305c-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="9305c-266">**Çözümleme**: kullanım `fs.azure.write.request.size` toospecify daha büyük bir blok boyutu.</span><span class="sxs-lookup"><span data-stu-id="9305c-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="9305c-267">Bir kullanım başına temelinde hello kullanarak bunu yapabilirsiniz `-D` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9305c-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="9305c-268">Merhaba hello ile bu parametresini kullanarak bir örnek verilmiştir `hadoop` komutu:</span><span class="sxs-lookup"><span data-stu-id="9305c-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="9305c-269">Merhaba değerini de artırabilirsiniz `fs.azure.write.request.size` Ambari kullanarak genel.</span><span class="sxs-lookup"><span data-stu-id="9305c-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="9305c-270">Merhaba aşağıdaki adımları olabilir hello Ambari Web kullanıcı arabirimini toochange hello değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9305c-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="9305c-271">Tarayıcınızda, kümeniz için Ambari Web kullanıcı arabirimini toohello gidin.</span><span class="sxs-lookup"><span data-stu-id="9305c-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="9305c-272">Https://CLUSTERNAME.azurehdinsight.net, budur nerede **CLUSTERNAME** hello kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="9305c-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="9305c-273">İstendiğinde, hello küme için hello yönetici adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="9305c-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="9305c-274">Yan hello ekranın sol hello seçin **HDFS**ve ardından hello **yapılandırmalar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9305c-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="9305c-275">Merhaba, **filtre... ** alanına, `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="9305c-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="9305c-276">Bu hello alan ve geçerli değer hello sayfa hello ortadaki görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9305c-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="9305c-277">Merhaba değer 262144 (256 KB) toohello yeni değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9305c-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="9305c-278">Örneğin, 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="9305c-278">For example, 4194304 (4MB).</span></span>

![Ambari Web kullanıcı Arabirimi aracılığıyla hello değeri değiştirme resmi](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="9305c-280">Ambari kullanarak daha fazla bilgi için bkz: [hello Ambari Web kullanıcı arabirimini kullanarak yönetin Hdınsight kümelerini](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="9305c-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9305c-281">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9305c-281">Next steps</span></span>
<span data-ttu-id="9305c-282">Anladığınıza göre Hdınsight tooget verisine nasıl okuma makaleleri toolearn nasıl aşağıdaki hello tooperform analiz:</span><span class="sxs-lookup"><span data-stu-id="9305c-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="9305c-283">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9305c-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="9305c-284">[Hadoop işlerini programlı olarak gönderme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="9305c-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="9305c-285">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9305c-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9305c-286">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9305c-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
