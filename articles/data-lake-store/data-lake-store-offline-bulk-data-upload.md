---
title: "Çevrimdışı yöntemleri kullanarak Data Lake Store verisine büyük miktarlarda aaaUpload | Microsoft Docs"
description: "Kullanım hello AdlCopy aracı toocopy verileri Azure depolama biriminden tooData Lake Store BLOB"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="4e545-103">Veri tooData Lake deposu çevrimdışı kopyası için Hello Azure içeri/dışarı aktarma hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="4e545-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="4e545-104">Bu makalede, nasıl toocopy çok büyük veri ayarlar öğreneceksiniz (> 200 GB) hello gibi çevrimdışı kopya yöntemleri kullanarak bir Azure Data Lake Store içine [Azure içeri/dışarı aktarma hizmeti](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="4e545-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="4e545-105">Özellikle, bu makaledeki örnek olarak kullanılan hello 339,420,860,416 bayt ya da yaklaşık 319 GB disk üzerindeki dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4e545-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="4e545-106">Şimdi bu dosya 319GB.tsv çağırın.</span><span class="sxs-lookup"><span data-stu-id="4e545-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="4e545-107">Hello Azure içeri/dışarı aktarma hizmeti, büyük miktarlarda veri daha fazla güvenli bir şekilde tooAzure Blob Depolama sevkiyat sabit disk tarafından tooan Azure veri merkezi sürücüleri tootransfer yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4e545-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e545-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e545-108">Prerequisites</span></span>
<span data-ttu-id="4e545-109">Başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e545-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="4e545-110">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="4e545-110">**An Azure subscription**.</span></span> <span data-ttu-id="4e545-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e545-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4e545-112">**Bir Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="4e545-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="4e545-113">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="4e545-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="4e545-114">Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4e545-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="4e545-115">Merhaba verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="4e545-115">Preparing hello data</span></span>
<span data-ttu-id="4e545-116">Merhaba içeri/dışarı aktarma hizmeti kullanmadan önce sonu hello veri dosyası toobe aktarılan **200 GB daha az olan kopyaları içine** boyutu.</span><span class="sxs-lookup"><span data-stu-id="4e545-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="4e545-117">Merhaba içeri aktarma aracını 200 GB'den büyük dosyalarla çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="4e545-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="4e545-118">Bu öğreticide, biz 100 GB öbeklere hello dosya bölün.</span><span class="sxs-lookup"><span data-stu-id="4e545-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="4e545-119">Kullanarak bunu yapabilirsiniz [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="4e545-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="4e545-120">Cygwin Linux komutları destekler.</span><span class="sxs-lookup"><span data-stu-id="4e545-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="4e545-121">Bu durumda, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="4e545-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="4e545-122">Merhaba bölme işlemi ile Merhaba adları aşağıdaki dosyaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e545-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="4e545-123">Veri diskleri hazırlanın</span><span class="sxs-lookup"><span data-stu-id="4e545-123">Get disks ready with data</span></span>
<span data-ttu-id="4e545-124">Merhaba yönergeleri izleyin [hello Azure içeri/dışarı aktarma hizmeti kullanma](../storage/common/storage-import-export-service.md) (Merhaba altında **sürücülerinizin hazırlama** bölüm) tooprepare sabit sürücüler.</span><span class="sxs-lookup"><span data-stu-id="4e545-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="4e545-125">İşte hello genel dizisi:</span><span class="sxs-lookup"><span data-stu-id="4e545-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="4e545-126">Hello Azure içeri/dışarı aktarma hizmeti için kullanılan hello gereksinim toobe karşılayan bir sabit disk temin edin.</span><span class="sxs-lookup"><span data-stu-id="4e545-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="4e545-127">Sevk edilen toohello Azure veri merkezi sonra hello veri kopyalanacağı bir Azure depolama hesabı belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4e545-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="4e545-128">Kullanım hello [Azure içeri/dışarı aktarma aracı](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), bir komut satırı yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="4e545-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="4e545-129">Nasıl toouse hello aracı gösteren bir örnek parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4e545-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="4e545-130">Bkz: [hello Azure içeri/dışarı aktarma hizmeti kullanma](../storage/common/storage-import-export-service.md) daha fazla örnek kod parçacıkları için.</span><span class="sxs-lookup"><span data-stu-id="4e545-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="4e545-131">Merhaba yukarıdaki komut bir günlük oluşturur hello dosyasını belirtilen konum.</span><span class="sxs-lookup"><span data-stu-id="4e545-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="4e545-132">Bu günlük dosyası toocreate hello alma işleminden kullanmak [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4e545-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="4e545-133">Bir içeri aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e545-133">Create an import job</span></span>
<span data-ttu-id="4e545-134">Hello konusundaki yönergeleri kullanarak, bir içeri aktarma işi şimdi oluşturabilirsiniz [hello Azure içeri/dışarı aktarma hizmeti kullanma](../storage/common/storage-import-export-service.md) (Merhaba altında **oluşturma hello alma işi** bölümü).</span><span class="sxs-lookup"><span data-stu-id="4e545-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="4e545-135">Bu içeri aktarma işi için diğer ayrıntılarla hello disk sürücüleri hazırlanırken oluşturduğunuz hello günlük dosyası da sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e545-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="4e545-136">Fiziksel olarak hello diskleri sevk</span><span class="sxs-lookup"><span data-stu-id="4e545-136">Physically ship hello disks</span></span>
<span data-ttu-id="4e545-137">Merhaba diskleri tooan Azure veri merkezi şimdi fiziksel olarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e545-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="4e545-138">Burada, hello veriler hello alma işi oluşturulurken sağlanan toohello Azure Storage blobları üzerinden kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4e545-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="4e545-139">İzleme bilgileri daha sonra tooprovide hello ettiyseniz ayrıca hello iş oluşturulurken şimdi izleme numarası tooyour alma işi ve güncelleştirme hello dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e545-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="4e545-140">Verileri Azure Storage blobları tooAzure Data Lake Deposu'ndan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="4e545-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="4e545-141">Merhaba Hello durumunu sonra alma işi tamamlandığında, hello veri belirtilen hello Azure Storage bloblarında kullanılabilir olup olmadığını doğrulayabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e545-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="4e545-142">Daha sonra hello verilerden tooAzure Data Lake Store BLOB yöntemleri toomove çeşitli kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e545-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="4e545-143">Tüm veri yüklemek için kullanılabilir seçenekler hello için bkz: [Data Lake Store veri alma](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="4e545-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="4e545-144">Bu bölümde, hello JSON tanımlarla toocreate bir Azure Data Factory işlem hattı verileri kopyalamak için kullanabilirsiniz sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="4e545-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="4e545-145">Bu JSON tanımları hello kullanabilirsiniz [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), veya [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4e545-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="4e545-146">Bağlantılı kaynak hizmeti (Azure Storage blobu)</span><span class="sxs-lookup"><span data-stu-id="4e545-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="4e545-147">Bağlantılı hizmet (Azure Data Lake Store) hedef</span><span class="sxs-lookup"><span data-stu-id="4e545-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="4e545-148">Giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="4e545-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="4e545-149">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="4e545-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="4e545-150">Etkinliğiniz (kopyalama etkinliği)</span><span class="sxs-lookup"><span data-stu-id="4e545-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="4e545-151">Daha fazla bilgi için bkz: [verileri Azure depolama biriminden blob Azure Data Factory kullanarak tooAzure Data Lake Store taşıma](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4e545-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="4e545-152">Azure Data Lake Store'da Hello veri dosyalarını yeniden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e545-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="4e545-153">319 GB ve böylece hello Azure içeri/dışarı aktarma hizmetini kullanarak aktarılabilir, daha küçük boyutu dosyalarına ihlal dosyası ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="4e545-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="4e545-154">Azure Data Lake Store'da Hello veridir, biz hello dosya tooits özgün boyutunu yeniden oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="4e545-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="4e545-155">Azure PowerShell cmldts toodo şekilde aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e545-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="4e545-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e545-156">Next steps</span></span>
* [<span data-ttu-id="4e545-157">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="4e545-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="4e545-158">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="4e545-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4e545-159">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="4e545-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
