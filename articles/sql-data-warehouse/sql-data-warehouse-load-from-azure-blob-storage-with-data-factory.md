---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Verileri Azure blob depolama alanından Azure SQL Data warehouse'a (Azure Data Factory) | Microsoft Docs"
description: "Azure Data Factory ile veri yüklemeyi öğrenin"
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
ms.openlocfilehash: ca8bdfc21582253e8709a33eb624547fed4461d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="bac07-103">Azure blob depolama alanından Azure SQL Data Warehouse'a (Azure Data Factory) veri yükleme</span><span class="sxs-lookup"><span data-stu-id="bac07-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bac07-104">Data Factory</span><span class="sxs-lookup"><span data-stu-id="bac07-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="bac07-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="bac07-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="bac07-106">Bu öğreticide, Azure Storage Blobundan SQL Data Warehouse'a veri taşımak üzere Azure Data Factory'de nasıl işlem hattı oluşturacağınız gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bac07-106">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to SQL Data Warehouse.</span></span> <span data-ttu-id="bac07-107">Sonraki adımlarda şunları gerçekleştireceksiniz:</span><span class="sxs-lookup"><span data-stu-id="bac07-107">With the following steps you will:</span></span>

* <span data-ttu-id="bac07-108">Bir Azure Storage Blobunda örnek veri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bac07-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="bac07-109">Kaynakları Azure Data Factory'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="bac07-109">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="bac07-110">Storage Bloblarından SQL Data Warehouse'a veri taşımak üzere bir işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bac07-110">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="bac07-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="bac07-111">Before you begin</span></span>
<span data-ttu-id="bac07-112">Azure Data Factory hakkında bilgi edinmek için bkz. [Azure Data Factory'ye giriş][Introduction to Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="bac07-112">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="bac07-113">Kaynak oluşturma veya tanımlama</span><span class="sxs-lookup"><span data-stu-id="bac07-113">Create or identify resources</span></span>
<span data-ttu-id="bac07-114">Bu öğreticiye başlamadan önce aşağıdaki kaynaklara sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bac07-114">Before starting this tutorial, you need to have the following resources.</span></span>

* <span data-ttu-id="bac07-115">**Azure Storage Blobu**: Bu öğreticide Azure Data Factory işlem hattı için veri kaynağı olarak Azure Storage Blobu kullanılır; bu nedenle örnek verileri saklamak için bir Azure Storage Blobuna sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bac07-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="bac07-116">Azure Depolama Blobunuz yoksa [Depolama hesabı oluşturma][Create a storage account] işlemini nasıl gerçekleştireceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bac07-116">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="bac07-117">**SQL Data Warehouse**: Bu öğreticide Azure Storage Blobundan SQL Data Warehouse'a veri taşınır; bu nedenle AdventureWorksDW örnek verileriyle yüklü çevrimiçi bir veri ambarınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bac07-117">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="bac07-118">Veri ambarınız yoksa nasıl [sağlayacağınızı][Create a SQL Data Warehouse] öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bac07-118">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="bac07-119">Veri ambarınız var ancak bu veri ambarına örnek veri sağlamadıysanız [el ile yükleme][Load sample data into SQL Data Warehouse] işlemini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bac07-119">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="bac07-120">**Azure Data Factory**: Azure Data Factory gerçek yüklemeyi tamamlanır ve bu nedenle veri taşıma işlem hattı oluşturmak için kullanabileceğiniz bir olması gerekir. Zaten yoksa, adım 1 / birinde oluşturmayı öğrenin [Azure Data Factory (Data Factory Editor) ile çalışmaya başlama][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="bac07-120">**Azure Data Factory**: Azure Data Factory will complete the actual load and so you need to have one that you can use to build the data movement pipeline.If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="bac07-121">**AZCopy**: Yerel istemcinizden Azure Storage Blobuna örnek veri kopyalamak için AZCopy gerekir.</span><span class="sxs-lookup"><span data-stu-id="bac07-121">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="bac07-122">Yükleme yönergeleri için bkz. [AZCopy belgeleri][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="bac07-122">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="bac07-123">1. Adım: Azure Storage Blobuna örnek veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="bac07-123">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="bac07-124">Her şey hazırsa Azure Storage Blobunuza örnek veri kopyalamaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bac07-124">Once you have all of the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="bac07-125">[Örnek verileri indirme][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="bac07-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="bac07-126">Bu işlem sonrasında AdventureWorksDW örnek verilerinize üç yıla ilişkin satış verileri eklenir.</span><span class="sxs-lookup"><span data-stu-id="bac07-126">This data will add another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="bac07-127">Üç yıla ilişkin verileri Azure Storage Blobunuza kopyalamak için bu AZCopy komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="bac07-127">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="bac07-128">2. Adım: Kaynakları Azure Data Factory'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="bac07-128">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="bac07-129">Verileri aldığınıza göre verileri Azure Blob depolama alanından SQL Data Warehouse'a taşımak üzere Azure Data Factory işlem hattını oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="bac07-129">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="bac07-130">Başlamak için [Azure portalını][Azure portal] açıp sol taraftaki menüden veri fabrikanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="bac07-130">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="bac07-131">2.1. Adım: Bağlı Hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="bac07-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="bac07-132">Azure depolama hesabınızı ve SQL Data Warehouse'unuzu veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="bac07-132">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="bac07-133">Öncelikle veri fabrikanızın "Bağlı Hizmetler" bölümüne ve ardından "Yeni veri deposu" öğesine tıklayarak kayıt işlemine başlayın.</span><span class="sxs-lookup"><span data-stu-id="bac07-133">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="bac07-134">Azure depolama alanınızı hangi adla kaydedeceğinizi seçin. Tür olarak Azure Storage'ı belirleyip Hesap Adı ve Hesap Anahtarı bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="bac07-134">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="bac07-135">SQL Data Warehouse'u kaydetmek için "Geliştir ve Dağıt" bölümüne giderek "Yeni Veri Deposu" seçeneğini ve ardından "Azure SQL Data Warehouse" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bac07-135">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="bac07-136">Kopyalama ve yapıştırma işlemlerini bu şablonda gerçekleştirip size özgü bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="bac07-136">Copy and paste in this template, and then fill in your specific information.</span></span>

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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="bac07-137">2.2. Adım: Veri kümesini tanımlama</span><span class="sxs-lookup"><span data-stu-id="bac07-137">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="bac07-138">Bağlı hizmetleri oluşturduktan sonra veri kümelerini tanımlamamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bac07-138">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="bac07-139">Bu, depolama alanınızdan veri ambarınıza taşınan verilerin yapısının tanımlanması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="bac07-139">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="bac07-140">Oluşturma işlemi hakkında daha fazla bilgi edinebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bac07-140">You can read more about creating</span></span>

1. <span data-ttu-id="bac07-141">Veri fabrikanızın "Geliştir ve Dağıt" bölümüne giderek bu işlemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="bac07-141">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="bac07-142">Depolama alanınızı veri fabrikanıza bağlamak için "Yeni veri kümesi" ve ardından "Azure Blob depolama alanı" seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bac07-142">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="bac07-143">Azure Blob depolama alanındaki verilerinizi tanımlamak için şu betiği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bac07-143">You can use the below script to define your data in Azure Blob storage:</span></span>

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


1. <span data-ttu-id="bac07-144">Şimdi biz de SQL Data Warehouse'a ilişkin veri kümemizi tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="bac07-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="bac07-145">Aynı şekilde başlayarak önce "Yeni veri kümesi" seçeneğine ve ardından "Azure SQL Data Warehouse" seçeneğine tıklıyoruz.</span><span class="sxs-lookup"><span data-stu-id="bac07-145">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="bac07-146">3. Adım: İşlem hattınızı oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bac07-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="bac07-147">Son olarak Azure Data Factory'de işlem hattı oluşturup çalıştıracağız.</span><span class="sxs-lookup"><span data-stu-id="bac07-147">Finally, we will set-up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="bac07-148">Bu işlem ile gerçek veri taşıma işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="bac07-148">This is the operation that will complete the actual data movement.</span></span>  <span data-ttu-id="bac07-149">SQL Veri Ambarı ve Azure Data Factory ile gerçekleştirebileceğiniz işlemlerin tam görünümünü [burada][Move data to and from Azure SQL Data Warehouse using Azure Data Factory] bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bac07-149">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="bac07-150">Şimdi ise "Geliştir ve Dağıt" bölümünde "Daha Fazla Komut" seçeneğine ve ardından "Yeni İşlem Hattı" seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bac07-150">In the 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="bac07-151">İşlem hattını oluşturduktan sonra verileri veri ambarınıza aktarmak için aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bac07-151">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bac07-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bac07-152">Next steps</span></span>
<span data-ttu-id="bac07-153">Şunları görüntüleyerek daha fazla bilgi edinmeye başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bac07-153">To learn more, start by viewing:</span></span>

* <span data-ttu-id="bac07-154">[Azure Data Factory öğrenme yolu][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="bac07-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="bac07-155">[Azure SQL Veri Ambarı Bağlayıcısı][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="bac07-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="bac07-156">Bu, Azure SQL Data Warehouse ile Azure Data Factory kullanımına yönelik temel başvuru konu başlığıdır.</span><span class="sxs-lookup"><span data-stu-id="bac07-156">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="bac07-157">Bu konu başlıklarında Azure Data Factory hakkında ayrıntılı bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bac07-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="bac07-158">Bunlarda, Azure SQL Database veya HDinsight hakkında bilgi verilmiştir ancak bu bilgiler Azure SQL Data Warehouse için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bac07-158">They discuss Azure SQL Database or HDinsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="bac07-159">[Öğretici: Azure Data Factory ile çalışmaya başlama][Tutorial: Get started with Azure Data Factory] Azure Data Factory ile veri işlemeye yönelik temel öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="bac07-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="bac07-160">Bu öğreticide web günlüklerini aylık olarak dönüştürmek ve çözümlemek üzere HDInsight'ı kullanan ilk işlem hattınızı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bac07-160">In this tutorial you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="bac07-161">Not: Bu öğreticide herhangi bir kopyalama etkinliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="bac07-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="bac07-162">[Öğretici: Azure Depolama Blobundan Azure SQL Veritabanı'na veri kopyalama][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="bac07-162">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="bac07-163">Bu öğreticide Azure Storage Blobundan Azure SQL Database'e veri kopyalamak üzere Azure Data Factory'de bir işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bac07-163">In this tutorial, you will create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
