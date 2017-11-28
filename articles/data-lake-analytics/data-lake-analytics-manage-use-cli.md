---
title: "Azure komut satırı arabirimi kullanarak Azure Data Lake Analytics aaaManage | Microsoft Docs"
description: "Toomanage Data Lake Analytics hesaplarını, veri kaynakları, işlerin nasıl ve Azure CLI kullanarak kullanıcıların bilgi edinin"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="598e2-103">Azure komut satırı arabirimi (CLI) kullanarak Azure Data Lake Analytics yönetme</span><span class="sxs-lookup"><span data-stu-id="598e2-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="598e2-104">Azure CLI toomanage Azure Data Lake Analytics hesaplarını, veri kaynakları, kullanıcılar ve işleri kullanarak nasıl hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="598e2-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="598e2-105">diğer araçları kullanarak toosee yönetimi konuları yukarıdaki hello sekme seçimine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="598e2-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="598e2-106">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="598e2-106">**Prerequisites**</span></span>

<span data-ttu-id="598e2-107">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="598e2-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="598e2-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="598e2-108">**An Azure subscription**.</span></span> <span data-ttu-id="598e2-109">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="598e2-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="598e2-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="598e2-110">**Azure CLI**.</span></span> <span data-ttu-id="598e2-111">Bkz. [Azure CLI'yı yükleme ve yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="598e2-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="598e2-112">Merhaba yükleyip **yayın öncesi** [Azure CLI araçlarını](https://github.com/MicrosoftBigData/AzureDataLake/releases) içinde bu demo toocomplete sipariş.</span><span class="sxs-lookup"><span data-stu-id="598e2-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="598e2-113">**Kimlik doğrulama**kullanarak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="598e2-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="598e2-114">Bir iş veya Okul hesabı kullanarak kimlik doğrulaması ile ilgili daha fazla bilgi için bkz: [tooan Azure aboneliği hello Azure CLI ' bağlanma](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="598e2-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="598e2-115">**Anahtar toohello Azure Resource Manager moduna**kullanarak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="598e2-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="598e2-116">**Data Lake Store ve Data Lake Analytics toolist hello komutlar:**</span><span class="sxs-lookup"><span data-stu-id="598e2-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="598e2-117">Hesapları yönetme</span><span class="sxs-lookup"><span data-stu-id="598e2-117">Manage accounts</span></span>
<span data-ttu-id="598e2-118">Herhangi bir Data Lake Analytics işi çalıştırmadan önce bir Data Lake Analytics hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="598e2-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="598e2-119">Azure Hdınsight, bir iş çalışmadığı zaman Analytics hesabı için ödemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="598e2-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="598e2-120">Yalnızca bir iş çalışırken hello zaman için ödeme yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="598e2-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="598e2-121">Daha fazla bilgi için bkz: [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="598e2-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="598e2-122">Hesapları oluşturma</span><span class="sxs-lookup"><span data-stu-id="598e2-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="598e2-123">Güncelleştirme hesapları</span><span class="sxs-lookup"><span data-stu-id="598e2-123">Update accounts</span></span>
<span data-ttu-id="598e2-124">Merhaba aşağıdaki komutu güncelleştirmeleri varolan bir Data Lake Analytics hesabı hello özellikleri</span><span class="sxs-lookup"><span data-stu-id="598e2-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="598e2-125">Hesapları listeleme</span><span class="sxs-lookup"><span data-stu-id="598e2-125">List accounts</span></span>
<span data-ttu-id="598e2-126">Liste Data Lake Analytics hesapları</span><span class="sxs-lookup"><span data-stu-id="598e2-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="598e2-127">Belirli bir kaynak grubunun içinde listesi Data Lake Analytics hesapları</span><span class="sxs-lookup"><span data-stu-id="598e2-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="598e2-128">Belirli bir Data Lake Analytics hesabı ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="598e2-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="598e2-129">Data Lake Analytics hesapları silme</span><span class="sxs-lookup"><span data-stu-id="598e2-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="598e2-130">Hesabı veri kaynaklarını yönet</span><span class="sxs-lookup"><span data-stu-id="598e2-130">Manage account data sources</span></span>
<span data-ttu-id="598e2-131">Data Lake Analytics şu anda aşağıdaki veri kaynaklar hello destekler:</span><span class="sxs-lookup"><span data-stu-id="598e2-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="598e2-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="598e2-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="598e2-133">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="598e2-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="598e2-134">Analytics hesabı oluşturduğunuzda, bir Azure Data Lake Storage hesabı toobe hello varsayılan depolama hesabı atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="598e2-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="598e2-135">Merhaba varsayılan ADL depolama hesabı kullanılan toostore işi meta verileri ve iş denetim günlükleri.</span><span class="sxs-lookup"><span data-stu-id="598e2-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="598e2-136">Analytics hesabı oluşturduktan sonra ek Data Lake Storage hesaplarını ve/veya Azure Storage hesabı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="598e2-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="598e2-137">Merhaba varsayılan ADL depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="598e2-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="598e2-138">Merhaba değer özellikler: datalakeStoreAccount:name altında listelenir.</span><span class="sxs-lookup"><span data-stu-id="598e2-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="598e2-139">Ek Azure Blob storage hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="598e2-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="598e2-140">Yalnızca Blob Depolama kısa adları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="598e2-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="598e2-141">FQDN, örneğin "myblob.blob.core.windows.net" kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="598e2-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="598e2-142">Ek Data Lake Store hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="598e2-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="598e2-143">[-d] hello eklenmekte olan Data Lake hello varsayılan Data Lake hesabı olup bir isteğe bağlı bir anahtar tooindicate değil.</span><span class="sxs-lookup"><span data-stu-id="598e2-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="598e2-144">Güncelleştirme mevcut veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="598e2-144">Update existing data source</span></span>
<span data-ttu-id="598e2-145">Mevcut bir Data Lake Store hesabı toobe hello varsayılan tooset:</span><span class="sxs-lookup"><span data-stu-id="598e2-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="598e2-146">tooupdate mevcut bir Blob Depolama hesabı anahtarı:</span><span class="sxs-lookup"><span data-stu-id="598e2-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="598e2-147">Liste veri kaynakları:</span><span class="sxs-lookup"><span data-stu-id="598e2-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics veri kaynağı listesi](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="598e2-149">Veri kaynaklarını silin:</span><span class="sxs-lookup"><span data-stu-id="598e2-149">Delete data sources:</span></span>
<span data-ttu-id="598e2-150">bir Data Lake Store hesabı toodelete:</span><span class="sxs-lookup"><span data-stu-id="598e2-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="598e2-151">toodelete bir Blob Depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="598e2-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="598e2-152">İşleri yönetme</span><span class="sxs-lookup"><span data-stu-id="598e2-152">Manage jobs</span></span>
<span data-ttu-id="598e2-153">Bir proje oluşturmadan önce bir Data Lake Analytics hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="598e2-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="598e2-154">Daha fazla bilgi için bkz: [yönetmek Data Lake Analytics hesapları](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="598e2-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="598e2-155">Liste işleri</span><span class="sxs-lookup"><span data-stu-id="598e2-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics veri kaynağı listesi](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="598e2-157">İş ayrıntılarını almak</span><span class="sxs-lookup"><span data-stu-id="598e2-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="598e2-158">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="598e2-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="598e2-159">bir işin Hello varsayılan öncelik 1000'dir ve hello varsayılan paralellik derecesi bir iş için 1'dir.</span><span class="sxs-lookup"><span data-stu-id="598e2-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="598e2-160">İşlerini iptal edin</span><span class="sxs-lookup"><span data-stu-id="598e2-160">Cancel jobs</span></span>
<span data-ttu-id="598e2-161">Merhaba listesi komutu toofind hello iş kimliği kullanın ve daha sonra iptal toocancel hello işlemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="598e2-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="598e2-162">Katalog Yönetimi</span><span class="sxs-lookup"><span data-stu-id="598e2-162">Manage catalog</span></span>
<span data-ttu-id="598e2-163">U-SQL komut dosyaları tarafından paylaşılabilmesi hello U-SQL kullanılan toostructure veri ve kod kataloğudur.</span><span class="sxs-lookup"><span data-stu-id="598e2-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="598e2-164">başlangıç kataloğu hello Azure Data Lake verilerle olası en yüksek performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="598e2-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="598e2-165">Daha fazla bilgi için bkz. [U-SQL kataloğunu kullanma](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="598e2-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="598e2-166">Liste katalog öğeleri</span><span class="sxs-lookup"><span data-stu-id="598e2-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="598e2-167">Veritabanı, şema, derleme, dış veri kaynağı, tablo, tablo değerli fonksiyon veya tablo istatistikleri Hello türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="598e2-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="598e2-168">ARM grupları kullanma</span><span class="sxs-lookup"><span data-stu-id="598e2-168">Use ARM groups</span></span>
<span data-ttu-id="598e2-169">Uygulamalar genellikle web uygulaması, veritabanı, veritabanı sunucusu, depolama alanı ve 3. taraf hizmetleri gibi birçok bileşenden oluşur.</span><span class="sxs-lookup"><span data-stu-id="598e2-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="598e2-170">Azure Resource Manager (ARM), bir grup, başvurulan tooas Azure kaynak grubu olarak hello kaynaklarla toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="598e2-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="598e2-171">Dağıtma, güncelleştirme, izlemek veya hello kaynakların tümünü tek ve eşgüdümlü bir işlemle uygulamanızda için silin.</span><span class="sxs-lookup"><span data-stu-id="598e2-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="598e2-172">Dağıtım için bir şablon kullanabilirsiniz. Üstelik bu şablon test, hazırlık ve üretim gibi farklı ortamlarda da çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="598e2-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="598e2-173">Merhaba hello tüm grup için aktarılmış maliyetleri görüntüleyerek kuruluşunuzun fatura açıklık getirebilir.</span><span class="sxs-lookup"><span data-stu-id="598e2-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="598e2-174">Daha fazla bilgi için bkz. [Azure Resource Manager'a Genel Bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="598e2-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="598e2-175">Bir Data Lake Analytics hizmeti aşağıdaki bileşenleri hello içerebilir:</span><span class="sxs-lookup"><span data-stu-id="598e2-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="598e2-176">Azure Data Lake Analytics hesabı</span><span class="sxs-lookup"><span data-stu-id="598e2-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="598e2-177">Gerekli varsayılan Azure Data Lake Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="598e2-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="598e2-178">Ek Azure Data Lake Storage hesapları</span><span class="sxs-lookup"><span data-stu-id="598e2-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="598e2-179">Ek Azure depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="598e2-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="598e2-180">Tüm bu bileşenlerin bir ARM Grup toomake altında oluşturabilirsiniz onları daha kolay toomanage.</span><span class="sxs-lookup"><span data-stu-id="598e2-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Azure Data Lake Analytics hesabı ve depolama](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="598e2-182">Bir Data Lake Analytics hesabı ve hello bağımlı depolama hesapları hello aynı yerleştirilmelidir Azure veri merkezi.</span><span class="sxs-lookup"><span data-stu-id="598e2-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="598e2-183">Merhaba ARM Grup ancak farklı veri merkezinde yer alabilir.</span><span class="sxs-lookup"><span data-stu-id="598e2-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="598e2-184">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="598e2-184">See also</span></span>
* [<span data-ttu-id="598e2-185">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="598e2-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="598e2-186">Azure Portal'ı kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="598e2-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="598e2-187">Azure Data Lake Analytics'i Azure Portal'ı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="598e2-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="598e2-188">Azure Portal'ı kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="598e2-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

