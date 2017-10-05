---
title: "Azure komut satırı arabirimi kullanarak Azure Data Lake Analytics yönetme | Microsoft Docs"
description: "Data Lake Analytics hesapları, veri kaynaklarını, işlerini ve kullanıcıları Azure CLI kullanarak yönetmeyi öğrenin"
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
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="8ae4d-103">Azure komut satırı arabirimi (CLI) kullanarak Azure Data Lake Analytics yönetme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="8ae4d-104">Azure Data Lake Analytics hesaplarını, veri kaynakları, kullanıcılar ve işleri Azure CLI kullanarak yönetmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="8ae4d-105">Yönetimi konuları diğer araçları kullanarak görmek için yukarıdaki sekme seçimine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="8ae4d-106">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="8ae4d-106">**Prerequisites**</span></span>

<span data-ttu-id="8ae4d-107">Bu öğreticiye başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8ae4d-108">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-108">**An Azure subscription**.</span></span> <span data-ttu-id="8ae4d-109">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8ae4d-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-110">**Azure CLI**.</span></span> <span data-ttu-id="8ae4d-111">Bkz. [Azure CLI'yı yükleme ve yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="8ae4d-112">Bu demoyu tamamlamak için **yayın öncesi sürüm** [Azure CLI araçlarını](https://github.com/MicrosoftBigData/AzureDataLake/releases) indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="8ae4d-113">Şu komutu kullanarak **kimlik doğrulama**:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="8ae4d-114">Bir iş veya okul hesabı kullanarak kimlik doğrulama gerçekleştirme konusunda daha fazla bilgi için bkz. [Azure CLI'dan Azure aboneliğine bağlanma](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="8ae4d-115">Şu komutu kullanarak **Azure Resource Manager moduna geçin**:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="8ae4d-116">**Data Lake Store ve Data Lake Analytics komutları listelemek için:**</span><span class="sxs-lookup"><span data-stu-id="8ae4d-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="8ae4d-117">Hesapları yönetme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-117">Manage accounts</span></span>
<span data-ttu-id="8ae4d-118">Herhangi bir Data Lake Analytics işi çalıştırmadan önce bir Data Lake Analytics hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="8ae4d-119">Azure Hdınsight, bir iş çalışmadığı zaman Analytics hesabı için ödemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="8ae4d-120">Yalnızca bir iş çalışırken zaman için ödeme yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="8ae4d-121">Daha fazla bilgi için bkz: [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="8ae4d-122">Hesapları oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ae4d-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="8ae4d-123">Güncelleştirme hesapları</span><span class="sxs-lookup"><span data-stu-id="8ae4d-123">Update accounts</span></span>
<span data-ttu-id="8ae4d-124">Aşağıdaki komut varolan bir Data Lake Analytics hesabı özelliklerini güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="8ae4d-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="8ae4d-125">Hesapları listeleme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-125">List accounts</span></span>
<span data-ttu-id="8ae4d-126">Liste Data Lake Analytics hesapları</span><span class="sxs-lookup"><span data-stu-id="8ae4d-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="8ae4d-127">Belirli bir kaynak grubunun içinde listesi Data Lake Analytics hesapları</span><span class="sxs-lookup"><span data-stu-id="8ae4d-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="8ae4d-128">Belirli bir Data Lake Analytics hesabı ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="8ae4d-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="8ae4d-129">Data Lake Analytics hesapları silme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="8ae4d-130">Hesabı veri kaynaklarını yönet</span><span class="sxs-lookup"><span data-stu-id="8ae4d-130">Manage account data sources</span></span>
<span data-ttu-id="8ae4d-131">Data Lake Analytics şu anda aşağıdaki veri kaynaklarını destekler:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="8ae4d-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8ae4d-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="8ae4d-133">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="8ae4d-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="8ae4d-134">Analytics hesabı oluşturduğunuzda, varsayılan depolama hesabı olacak şekilde bir Azure Data Lake Store hesabına atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="8ae4d-135">Varsayılan ADL depolama hesabı, iş meta verileri ve iş denetim günlüklerini depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="8ae4d-136">Analytics hesabı oluşturduktan sonra ek Data Lake Storage hesaplarını ve/veya Azure Storage hesabı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="8ae4d-137">Varsayılan ADL depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ae4d-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="8ae4d-138">Değer özellikler: datalakeStoreAccount:name altında listelenir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="8ae4d-139">Ek Azure Blob storage hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="8ae4d-140">Yalnızca Blob Depolama kısa adları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="8ae4d-141">FQDN, örneğin "myblob.blob.core.windows.net" kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="8ae4d-142">Ek Data Lake Store hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="8ae4d-143">[-d] eklenmekte olan Data Lake varsayılan Data Lake hesabı olup olmadığını belirtmek için isteğe bağlı bir anahtardır.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="8ae4d-144">Güncelleştirme mevcut veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="8ae4d-144">Update existing data source</span></span>
<span data-ttu-id="8ae4d-145">Varsayılan olarak mevcut bir Data Lake Store hesabı ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="8ae4d-146">Mevcut bir Blob Depolama hesabı anahtarı güncelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="8ae4d-147">Liste veri kaynakları:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics veri kaynağı listesi](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="8ae4d-149">Veri kaynaklarını silin:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-149">Delete data sources:</span></span>
<span data-ttu-id="8ae4d-150">Bir Data Lake Store hesabını silmek için:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="8ae4d-151">Bir Blob Depolama hesabını silmek için:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="8ae4d-152">İşleri yönetme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-152">Manage jobs</span></span>
<span data-ttu-id="8ae4d-153">Bir proje oluşturmadan önce bir Data Lake Analytics hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="8ae4d-154">Daha fazla bilgi için bkz: [yönetmek Data Lake Analytics hesapları](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="8ae4d-155">Liste işleri</span><span class="sxs-lookup"><span data-stu-id="8ae4d-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics veri kaynağı listesi](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="8ae4d-157">İş ayrıntılarını almak</span><span class="sxs-lookup"><span data-stu-id="8ae4d-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="8ae4d-158">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="8ae4d-159">Bir işin varsayılan öncelik 1000'dir ve varsayılan paralellik derecesi bir iş için 1'dir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="8ae4d-160">İşlerini iptal edin</span><span class="sxs-lookup"><span data-stu-id="8ae4d-160">Cancel jobs</span></span>
<span data-ttu-id="8ae4d-161">İş kimliği ve ardından işi iptal etmek için İptal bulmak için liste komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="8ae4d-162">Katalog Yönetimi</span><span class="sxs-lookup"><span data-stu-id="8ae4d-162">Manage catalog</span></span>
<span data-ttu-id="8ae4d-163">U-SQL kataloğunu, U-SQL komut dosyaları tarafından paylaşılabilmesi veri ve kod yapısı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="8ae4d-164">Katalog Azure Data Lake verilerle olası en yüksek performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="8ae4d-165">Daha fazla bilgi için bkz. [U-SQL kataloğunu kullanma](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="8ae4d-166">Liste katalog öğeleri</span><span class="sxs-lookup"><span data-stu-id="8ae4d-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="8ae4d-167">Veritabanı, şema, derleme, dış veri kaynağı, tablo, tablo değerli fonksiyon veya tablo istatistikleri türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="8ae4d-168">ARM grupları kullanma</span><span class="sxs-lookup"><span data-stu-id="8ae4d-168">Use ARM groups</span></span>
<span data-ttu-id="8ae4d-169">Uygulamalar genellikle web uygulaması, veritabanı, veritabanı sunucusu, depolama alanı ve 3. taraf hizmetleri gibi birçok bileşenden oluşur.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="8ae4d-170">Azure Resource Manager (ARM), uygulamanızdaki kaynaklarla Azure Kaynak Grubu şeklinde adlandırılan bir grup olarak çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="8ae4d-171">Uygulamanıza yönelik tüm kaynakları tek ve eşgüdümlü bir işlemle dağıtabilir, güncelleştirebilir, izleyebilir veya silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="8ae4d-172">Dağıtım için bir şablon kullanabilirsiniz. Üstelik bu şablon test, hazırlık ve üretim gibi farklı ortamlarda da çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="8ae4d-173">Tüm grup için aktarılmış maliyetleri görüntüleyerek kuruluşunuzun fatura işlemlerine açıklık getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="8ae4d-174">Daha fazla bilgi için bkz. [Azure Resource Manager'a Genel Bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ae4d-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="8ae4d-175">Bir Data Lake Analytics hizmeti aşağıdaki bileşenleri şunları içerebilir:</span><span class="sxs-lookup"><span data-stu-id="8ae4d-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="8ae4d-176">Azure Data Lake Analytics hesabı</span><span class="sxs-lookup"><span data-stu-id="8ae4d-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="8ae4d-177">Gerekli varsayılan Azure Data Lake Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="8ae4d-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="8ae4d-178">Ek Azure Data Lake Storage hesapları</span><span class="sxs-lookup"><span data-stu-id="8ae4d-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="8ae4d-179">Ek Azure depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="8ae4d-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="8ae4d-180">Tüm bu bileşenlerin yönetmeyi kolaylaştırmak için bir ARM grubu altında oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Azure Data Lake Analytics hesabı ve depolama](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="8ae4d-182">Bir Data Lake Analytics hesabı ve bağımlı depolama hesapları aynı Azure veri merkezinde yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="8ae4d-183">ARM Grup ancak farklı veri merkezinde yer alabilir.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8ae4d-184">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8ae4d-184">See also</span></span>
* [<span data-ttu-id="8ae4d-185">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="8ae4d-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8ae4d-186">Azure Portal'ı kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8ae4d-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8ae4d-187">Azure Data Lake Analytics'i Azure Portal'ı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="8ae4d-188">Azure Portal'ı kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="8ae4d-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

