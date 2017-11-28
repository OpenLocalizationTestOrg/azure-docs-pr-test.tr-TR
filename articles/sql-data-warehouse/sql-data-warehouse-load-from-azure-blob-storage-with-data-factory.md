---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: aaaLoad verileri Azure blob depolamada Azure SQL Data Warehouse'a (Azure Data Factory) | Microsoft Docs
description: "Azure Data Factory ile tooload veri öğrenin"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="c830b-103">Azure blob depolama alanından Azure SQL Data Warehouse'a (Azure Data Factory) veri yükleme</span><span class="sxs-lookup"><span data-stu-id="c830b-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c830b-104">Data Factory</span><span class="sxs-lookup"><span data-stu-id="c830b-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="c830b-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="c830b-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="c830b-106">Bu öğretici şunların nasıl yapıldığını gösterir toocreate bir işlem hattı Azure Data Factory toomove verileri Azure Storage Blobuna tooSQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="c830b-106">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooSQL Data Warehouse.</span></span> <span data-ttu-id="c830b-107">Aşağıdaki adımları hello ile şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="c830b-107">With hello following steps you will:</span></span>

* <span data-ttu-id="c830b-108">Bir Azure Storage Blobunda örnek veri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c830b-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="c830b-109">Kaynakları tooAzure Data Factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c830b-109">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="c830b-110">Ardışık Düzen toomove veri depolama BLOB'ları tooSQL veri ambarı ' oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c830b-110">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="c830b-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="c830b-111">Before you begin</span></span>
<span data-ttu-id="c830b-112">toofamiliarize kendiniz Azure Data Factory ile görün [giriş tooAzure Data Factory][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="c830b-112">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="c830b-113">Kaynak oluşturma veya tanımlama</span><span class="sxs-lookup"><span data-stu-id="c830b-113">Create or identify resources</span></span>
<span data-ttu-id="c830b-114">Bu öğreticiye başlamadan önce kaynakları aşağıdaki toohave hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="c830b-114">Before starting this tutorial, you need toohave hello following resources.</span></span>

* <span data-ttu-id="c830b-115">**Azure depolama blobu**: Bu öğreticide Azure Storage Blobuna hello veri kaynağı olarak hello Azure Data Factory işlem hattı için kullanır ve gerekir böylece toohave bir kullanılabilir toostore hello örnek veri.</span><span class="sxs-lookup"><span data-stu-id="c830b-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="c830b-116">Zaten yoksa, nasıl çok öğrenin[depolama hesabı oluşturma][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="c830b-116">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="c830b-117">**SQL veri ambarı**: toohave hello AdventureWorksDW örnek verileri ile yüklenen bir veri ambarı çevrimiçi SQL veri ambarı ve bu nedenle çok Bu öğretici taşır hello verileri Azure Storage Blobuna gerekir.</span><span class="sxs-lookup"><span data-stu-id="c830b-117">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="c830b-118">Veri ambarı zaten yoksa, nasıl çok öğrenin[sağlayacağınızı][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c830b-118">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="c830b-119">Bir veri ambarına sahip, ancak hello örnek veri sağlamadıysanız, yapabilecekleriniz [el ile yükleme][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c830b-119">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="c830b-120">**Azure Data Factory**: Azure Data Factory hello gerçek yük tamamlanır ve gerekir böylece toobuild hello veri taşıma işlem hattı kullanabilirsiniz toohave biri. Zaten yoksa, bilgi nasıl toocreate bir 1. adımda, [Azure Data Factory (Data Factory Editor) ile çalışmaya başlama][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="c830b-120">**Azure Data Factory**: Azure Data Factory will complete hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="c830b-121">**AZCopy**: yerel istemci tooyour Azure Storage Blobuna AZCopy toocopy hello örnek verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="c830b-121">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="c830b-122">Yükleme yönergeleri için bkz: Merhaba [AZCopy belgeleri][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="c830b-122">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="c830b-123">1. adım: örnek veri tooAzure depolama Blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="c830b-123">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="c830b-124">Tüm hello parçaları hazır olduktan sonra hazır toocopy örnek veri tooyour Azure Storage Blobuna demektir.</span><span class="sxs-lookup"><span data-stu-id="c830b-124">Once you have all of hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="c830b-125">[Örnek verileri indirme][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="c830b-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="c830b-126">Bu veriler üç yıla ilişkin satış verileri tooyour AdventureWorksDW örnek verileri ekler.</span><span class="sxs-lookup"><span data-stu-id="c830b-126">This data will add another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="c830b-127">Bu AZCopy komutunu toocopy hello üç yıla kadar veri tooyour Azure Storage Blobuna kullanın.</span><span class="sxs-lookup"><span data-stu-id="c830b-127">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="c830b-128">2. adım: kaynakları tooAzure Data Factory bağlanma</span><span class="sxs-lookup"><span data-stu-id="c830b-128">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="c830b-129">Merhaba veri bulunduğundan şimdi biz hello Azure Data Factory işlem hattı toomove hello verileri Azure blob depolama alanından SQL Data Warehouse'a oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c830b-129">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="c830b-130">tooget başlatıldı, açık hello [Azure portal] [ Azure portal] ve hello sol taraftaki menüden veri fabrikanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="c830b-130">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="c830b-131">2.1. Adım: Bağlı Hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="c830b-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="c830b-132">Azure depolama hesabı ve SQL Data Warehouse tooyour veri fabrikası bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c830b-132">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="c830b-133">Öncelikle veri fabrikanızın hello 'Bağlantılı Hizmetleri' bölümüne tıklayarak hello kayıt işlemine başlamak ve 'Yeni veri deposu' ı</span><span class="sxs-lookup"><span data-stu-id="c830b-133">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="c830b-134">Ad tooregister azure depolama alanınızı, select Azure depolama alanı olarak türünüzü seçin ve ardından hesap adı ve hesap anahtarını girin.</span><span class="sxs-lookup"><span data-stu-id="c830b-134">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="c830b-135">tooregister SQL veri ambarı toohello 'Geliştir ve Dağıt' bölümüne gidin, 'Yeni veri deposu' ve 'Azure SQL veri ambarı' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="c830b-135">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="c830b-136">Kopyalama ve yapıştırma işlemlerini bu şablonda gerçekleştirip size özgü bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="c830b-136">Copy and paste in this template, and then fill in your specific information.</span></span>

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="c830b-137">2.2. adım: hello dataset tanımlama</span><span class="sxs-lookup"><span data-stu-id="c830b-137">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="c830b-138">Merhaba oluşturma hizmetleri bağlandıktan sonra biz toodefine hello veri kümelerini sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c830b-138">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="c830b-139">Burada bu depolama tooyour veri ambarından taşındığı hello verilerin hello yapısını tanımlanması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c830b-139">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="c830b-140">Oluşturma işlemi hakkında daha fazla bilgi edinebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c830b-140">You can read more about creating</span></span>

1. <span data-ttu-id="c830b-141">Veri fabrikanızın toohello "Geliştir ve Dağıt" bölümüne giderek bu işlemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="c830b-141">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="c830b-142">'Yeni veri kümesi' ve 'Azure Blob storage' toolink depolama tooyour veri fabrikası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c830b-142">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="c830b-143">Komut dosyası toodefine aşağıda hello verileriniz Azure Blob depolama alanına kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c830b-143">You can use hello below script toodefine your data in Azure Blob storage:</span></span>

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```


1. <span data-ttu-id="c830b-144">Şimdi biz de SQL Data Warehouse'a ilişkin veri kümemizi tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="c830b-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="c830b-145">Biz hello Başlat 'Yeni veri kümesi' ve 'Azure SQL Data Warehouse ''ı tıklatarak aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="c830b-145">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="c830b-146">3. Adım: İşlem hattınızı oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c830b-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="c830b-147">Son olarak, Kurulum ve Çalıştır hello Azure Data Factory'de işlem hattı olur.</span><span class="sxs-lookup"><span data-stu-id="c830b-147">Finally, we will set-up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="c830b-148">Bu hello gerçek veri taşıma tamamlayacak hello işlemdir.</span><span class="sxs-lookup"><span data-stu-id="c830b-148">This is hello operation that will complete hello actual data movement.</span></span>  <span data-ttu-id="c830b-149">SQL Data Warehouse ve Azure Data Factory ile tamamlayabilirsiniz hello operations tam görünümünü bulabilirsiniz [burada][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="c830b-149">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="c830b-150">Merhaba "Geliştir ve Dağıt" bölümünde şimdi 'Başka komutlar' ve 'Yeni işlem hattı' tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c830b-150">In hello 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="c830b-151">Merhaba işlem hattını oluşturduktan sonra kodu tootransfer hello veri tooyour veri ambarı hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c830b-151">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c830b-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c830b-152">Next steps</span></span>
<span data-ttu-id="c830b-153">toolearn daha görüntüleyerek başlatın:</span><span class="sxs-lookup"><span data-stu-id="c830b-153">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="c830b-154">[Azure Data Factory öğrenme yolu][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="c830b-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="c830b-155">[Azure SQL Veri Ambarı Bağlayıcısı][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="c830b-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="c830b-156">Bu, Azure SQL Data Warehouse ile Azure Data Factory kullanma hello temel başvuru konu başlığıdır.</span><span class="sxs-lookup"><span data-stu-id="c830b-156">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="c830b-157">Bu konu başlıklarında Azure Data Factory hakkında ayrıntılı bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c830b-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="c830b-158">Azure SQL Database veya HDinsight ele ancak hello bilgiler tooAzure SQL Data Warehouse için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c830b-158">They discuss Azure SQL Database or HDinsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="c830b-159">[Öğretici: Azure Data Factory ile çalışmaya başlama] [ Tutorial: Get started with Azure Data Factory] bu Azure Data Factory ile veri işlemeye hello temel öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="c830b-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="c830b-160">Bu öğreticide, Hdınsight tootransform kullanan ilk işlem hattınızı oluşturma ve web günlüklerini aylık olarak analiz edin.</span><span class="sxs-lookup"><span data-stu-id="c830b-160">In this tutorial you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="c830b-161">Not: Bu öğreticide herhangi bir kopyalama etkinliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="c830b-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="c830b-162">[Öğretici: Azure Storage Blobuna tooAzure SQL veritabanı ' veri kopyalama][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="c830b-162">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="c830b-163">Bu öğreticide, Azure Storage Blobuna tooAzure SQL veritabanı ' Azure Data Factory toocopy verilerdeki bir işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c830b-163">In this tutorial, you will create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
