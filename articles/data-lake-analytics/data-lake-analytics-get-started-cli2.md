---
title: "aaaGet kullanarak Azure Data Lake Azure CLI 2.0 Analytics ile çalışmaya | Microsoft Docs"
description: "Toouse hello Azure komut satırı arabirimi 2.0 toocreate Data Lake Analytics hesabı, U-SQL'yi kullanarak Data Lake Analytics işi oluşturma ve hello işi göndermek öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="54daa-103">Azure CLI 2.0 aracını kullanarak Azure Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="54daa-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="54daa-104">Bu öğreticide, sekmeyle ayrılmış değerler (TSV) dosyasını okuyan ve bu dosyayı virgülle ayrılmış değerler (CSV) dosyasına dönüştüren bir iş geliştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="54daa-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="54daa-105">aynı öğreticiyi diğer kullanarak desteklenen hello aracılığıyla toogo araçları, bu bölümün hello üstte hello açılır listesi kullan.</span><span class="sxs-lookup"><span data-stu-id="54daa-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54daa-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="54daa-106">Prerequisites</span></span>
<span data-ttu-id="54daa-107">Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="54daa-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="54daa-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="54daa-108">**An Azure subscription**.</span></span> <span data-ttu-id="54daa-109">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54daa-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="54daa-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="54daa-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="54daa-111">Bkz. [Azure CLI'yı yükleme ve yapılandırma](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54daa-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="54daa-112">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="54daa-112">Log in tooAzure</span></span>

<span data-ttu-id="54daa-113">toolog tooyour Azure abonelik içinde:</span><span class="sxs-lookup"><span data-stu-id="54daa-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="54daa-114">İstenen toobrowse tooa URL olan ve bir kimlik doğrulaması kodunu girin.</span><span class="sxs-lookup"><span data-stu-id="54daa-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="54daa-115">Ve ardından kimlik bilgilerinizi hello yönergeleri tooenter izleyin.</span><span class="sxs-lookup"><span data-stu-id="54daa-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="54daa-116">Oturum açtıktan sonra hello oturum açma komut aboneliklerinizi listeler.</span><span class="sxs-lookup"><span data-stu-id="54daa-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="54daa-117">belirli bir aboneliği toouse:</span><span class="sxs-lookup"><span data-stu-id="54daa-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="54daa-118">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="54daa-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="54daa-119">Herhangi bir işi çalıştırmadan önce bir Data Lake Analytics hesabına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54daa-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="54daa-120">toocreate Data Lake Analytics hesabı, aşağıdaki öğelerindeki hello belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="54daa-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="54daa-121">**Azure Kaynak Grubu**.</span><span class="sxs-lookup"><span data-stu-id="54daa-121">**Azure Resource Group**.</span></span> <span data-ttu-id="54daa-122">Azure Kaynak Grubu'nda bir Data Lake Analytics hesabı oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="54daa-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="54daa-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toowork hello kaynaklarla bir grup olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="54daa-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="54daa-124">Dağıtma, güncelleştirme veya hello kaynakların tümünü tek ve eşgüdümlü bir işlemle uygulamanızda için silme.</span><span class="sxs-lookup"><span data-stu-id="54daa-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="54daa-125">toolist hello varolan kaynak gruplarını aboneliğinizi altında:</span><span class="sxs-lookup"><span data-stu-id="54daa-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="54daa-126">Yeni bir kaynak grubu toocreate:</span><span class="sxs-lookup"><span data-stu-id="54daa-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="54daa-127">**Data Lake Analytics hesap adı**.</span><span class="sxs-lookup"><span data-stu-id="54daa-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="54daa-128">Her Data Lake Analytics hesabının bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="54daa-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="54daa-129">**Konum**.</span><span class="sxs-lookup"><span data-stu-id="54daa-129">**Location**.</span></span> <span data-ttu-id="54daa-130">Data Lake Analytics destekleyen hello Azure veri merkezlerinde birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="54daa-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="54daa-131">**Varsayılan Data Lake Store hesabı**: Her Data Lake Analytics hesabı, bir varsayılan Data Lake Store hesabına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="54daa-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="54daa-132">toolist hello varolan Data Lake Store hesabı:</span><span class="sxs-lookup"><span data-stu-id="54daa-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="54daa-133">toocreate yeni bir Data Lake Store hesabı:</span><span class="sxs-lookup"><span data-stu-id="54daa-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="54daa-134">Sözdizimi toocreate Data Lake Analytics hesabı aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="54daa-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="54daa-135">Bir hesap oluşturduktan sonra aşağıdaki komutları toolist hello hesapları hello kullanın ve hesap ayrıntıları göster:</span><span class="sxs-lookup"><span data-stu-id="54daa-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="54daa-136">Veri tooData Lake deposu karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="54daa-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="54daa-137">Bu eğiticide, bazı arama günlüklerini işleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="54daa-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="54daa-138">Merhaba arama günlüğü, Data Lake store veya Azure Blob storage ' depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="54daa-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="54daa-139">Hello Azure portal, bir arama günlüğü dosyası içeren bazı örnek veri dosyalarını toohello varsayılan Data Lake Store hesabı, kopyalamak için bir kullanıcı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="54daa-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="54daa-140">Bkz: [kaynak verileri hazırlama](data-lake-analytics-get-started-portal.md) tooupload hello veri toohello varsayılan Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="54daa-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="54daa-141">CLI 2.0 kullanarak tooupload dosyaları hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="54daa-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="54daa-142">Data Lake Analytics ayrıca Azure Blob depolama alanına da erişebilir.</span><span class="sxs-lookup"><span data-stu-id="54daa-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="54daa-143">Veri tooAzure Blob Depolama yüklemek için bkz: [kullanma hello Azure Storage ile Azure CLI](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54daa-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="54daa-144">Data Lake Analytics işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="54daa-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="54daa-145">Hello Data Lake Analytics işleri, U-SQL dili hello yazılır.</span><span class="sxs-lookup"><span data-stu-id="54daa-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="54daa-146">U-SQL hakkında daha fazla toolearn bkz [U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md) ve [U-SQL dili eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="54daa-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="54daa-147">**toocreate bir Data Lake Analytics işi betiği**</span><span class="sxs-lookup"><span data-stu-id="54daa-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="54daa-148">Aşağıdaki U-SQL betiği ile bir metin dosyası oluşturun ve hello metin dosyası tooyour iş istasyonu kaydedin:</span><span class="sxs-lookup"><span data-stu-id="54daa-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="54daa-149">Bu U-SQL betiği hello kullanarak kaynak veri dosyasını okur **Extractors.Tsv()**ve ardından bir csv dosyası kullanarak oluşturan **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="54daa-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="54daa-150">Merhaba kaynak dosyayı farklı bir konuma kopyalayın sürece hello iki yolu değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="54daa-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="54daa-151">Yoksa, data Lake Analytics hello çıkış klasörü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54daa-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="54daa-152">Daha basit toouse varsayılan Data Lake Store hesaplarında depolanan dosyalar için göreli yolların olur.</span><span class="sxs-lookup"><span data-stu-id="54daa-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="54daa-153">Mutlak yol da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54daa-153">You can also use absolute paths.</span></span>  <span data-ttu-id="54daa-154">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54daa-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="54daa-155">Mutlak yollar tooaccess dosyaları, bağlı Storage hesaplarındaki kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54daa-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="54daa-156">bağlı Azure Storage hesabında depolanan dosyalar için Hello sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="54daa-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="54daa-157">Genel bloblar ile Azure Blob kapsayıcısı desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="54daa-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="54daa-158">Genel kapsayıcılar ile Azure Blob kapsayıcısı desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="54daa-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="54daa-159">**toosubmit işleri**</span><span class="sxs-lookup"><span data-stu-id="54daa-159">**toosubmit jobs**</span></span>

<span data-ttu-id="54daa-160">Sözdizimi toosubmit bir işi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="54daa-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="54daa-161">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54daa-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="54daa-162">**toolist işler ve iş ayrıntıları göster**</span><span class="sxs-lookup"><span data-stu-id="54daa-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="54daa-163">**toocancel işleri**</span><span class="sxs-lookup"><span data-stu-id="54daa-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="54daa-164">İş sonuçlarını alma</span><span class="sxs-lookup"><span data-stu-id="54daa-164">Retrieve job results</span></span>

<span data-ttu-id="54daa-165">Bir işi tamamlandıktan sonra aşağıdaki komutları toolist hello çıktı dosyaları hello kullanın ve hello dosyalarını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="54daa-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="54daa-166">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54daa-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="54daa-167">İşlem hatları ve tekrarlar</span><span class="sxs-lookup"><span data-stu-id="54daa-167">Pipelines and recurrences</span></span>

<span data-ttu-id="54daa-168">**İşlem hatları ve tekrarlar hakkında bilgi edinin**</span><span class="sxs-lookup"><span data-stu-id="54daa-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="54daa-169">Kullanım hello `az dla job pipeline` toosee hello ardışık düzen bilgi işleri daha önce gönderilen komutları.</span><span class="sxs-lookup"><span data-stu-id="54daa-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="54daa-170">Kullanım hello `az dla job recurrence` daha önce gönderilen işlerinin toosee hello yinelenme bilgilerini komutları.</span><span class="sxs-lookup"><span data-stu-id="54daa-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="54daa-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54daa-171">Next steps</span></span>

* <span data-ttu-id="54daa-172">toosee hello Data Lake Analytics CLI 2.0 başvuru belgesini bkz [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="54daa-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="54daa-173">toosee hello Data Lake deposu CLI 2.0 başvuru belgesini bkz [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="54daa-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="54daa-174">toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="54daa-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
