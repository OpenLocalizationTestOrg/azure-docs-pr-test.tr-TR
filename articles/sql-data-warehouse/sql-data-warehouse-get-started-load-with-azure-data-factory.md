---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: Azure Data Factory ile aaaLoad veri | Microsoft Docs
description: "Azure Data Factory ile tooload veri öğrenin"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a>Azure Data Factory ile veri yükleme
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

Bu öğretici şunların nasıl yapıldığını gösterir toocreate bir işlem hattı Azure Data Factory toomove verileri Azure Storage Blobuna tooAzure SQL veri ambarı. Aşağıdaki adımları hello ile şunları yapacaksınız:

* Bir Azure Depolama Blobunda örnek veri oluşturma.
* Kaynakları tooAzure Data Factory bağlayın.
* Ardışık Düzen toomove veri depolama BLOB'ları tooSQL veri ambarı ' oluşturun.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Başlamadan önce
toofamiliarize kendiniz Azure Data Factory ile görün [giriş tooAzure Data Factory][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Kaynak oluşturma veya tanımlama
Bu öğreticiye başlamadan önce kaynakları aşağıdaki toohave hello gerekir:

* **Azure depolama blobu**: Bu öğreticide Azure Storage Blobuna hello veri kaynağı olarak hello Azure Data Factory işlem hattı için kullanır ve gerekir böylece toohave bir kullanılabilir toostore hello örnek veri. Zaten yoksa, nasıl çok öğrenin[depolama hesabı oluşturma][Create a storage account].
* **SQL veri ambarı**: toohave hello AdventureWorksDW örnek verileri ile yüklenen bir veri ambarı çevrimiçi SQL veri ambarı ve bu nedenle çok Bu öğretici taşır hello verileri Azure Storage Blobuna gerekir. Veri ambarı zaten yoksa, nasıl çok öğrenin[sağlayacağınızı][Create a SQL Data Warehouse]. Bir veri ambarına sahip, ancak hello örnek veri sağlamadıysanız, yapabilecekleriniz [el ile yükleme][Load sample data into SQL Data Warehouse].
* **Azure Data Factory**: Azure Data Factory hello gerçek yüklemeyi tamamlar ve gerekir böylece toobuild hello veri taşıma işlem hattı kullanabilirsiniz toohave biri. Zaten yoksa, bilgi nasıl toocreate bir 1. adımda, [Azure Data Factory (Data Factory Editor) ile çalışmaya başlama][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: yerel istemci tooyour Azure Storage Blobuna AZCopy toocopy hello örnek verileri gerekir. Yükleme yönergeleri için bkz: Merhaba [AZCopy belgeleri][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>1. adım: örnek veri tooAzure depolama Blob kopyalama
Tüm hello parça hazır olduktan sonra hazır toocopy örnek veri tooyour Azure Storage Blobuna demektir.

1. [Örnek verileri indirme][Download sample data]. Bu veriler üç yıla ilişkin satış verileri tooyour AdventureWorksDW örnek verileri ekler.
2. Bu AZCopy komutunu toocopy hello üç yıla kadar veri tooyour Azure Storage Blobuna kullanın.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>2. adım: kaynakları tooAzure Data Factory bağlanma
Merhaba veri bulunduğundan şimdi biz hello Azure Data Factory işlem hattı toomove hello verileri Azure blob depolama alanından SQL Data Warehouse'a oluşturabilirsiniz.

tooget başlatıldı, açık hello [Azure portal] [ Azure portal] ve hello sol taraftaki menüden veri fabrikanızı seçin.

### <a name="step-21-create-linked-service"></a>2.1. Adım: Bağlı Hizmet oluşturma
Azure depolama hesabı ve SQL Data Warehouse tooyour veri fabrikası bağlayın.  

1. Öncelikle veri fabrikanızın hello 'Bağlantılı Hizmetleri' bölümüne tıklayarak hello kayıt işlemine başlamak ve 'Yeni veri deposu' ı Ad tooregister azure depolama alanınızı, select Azure depolama alanı olarak türünüzü seçin ve ardından hesap adı ve hesap anahtarını girin.
2. tooregister SQL veri ambarı toohello 'Geliştir ve Dağıt' bölümüne gidin, 'Yeni veri deposu' ve 'Azure SQL veri ambarı' nı seçin. Kopyalama ve yapıştırma işlemlerini bu şablonda gerçekleştirip size özgü bilgileri girin.
   
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

### <a name="step-22-define-hello-dataset"></a>2.2. adım: hello dataset tanımlama
Merhaba oluşturma hizmetleri bağlandıktan sonra biz toodefine hello veri kümelerini sahip olur.  Burada bu depolama tooyour veri ambarından taşındığı hello verilerin hello yapısını tanımlanması anlamına gelir.  Oluşturma işlemi hakkında daha fazla bilgi edinebilirsiniz

1. Veri fabrikanızın toohello "Geliştir ve Dağıt" bölümüne giderek bu işlemi başlatın.
2. 'Yeni veri kümesi' ve 'Azure Blob storage' toolink depolama tooyour veri fabrikası'ı tıklatın.  Komut dosyası toodefine aşağıda hello verileriniz Azure Blob depolama alanına kullanabilirsiniz:
   
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
3. Şimdi SQL Veri Ambarı'na ilişkin veri kümemizi tanımlayacağız. Biz hello Başlat 'Yeni veri kümesi' ve 'Azure SQL Data Warehouse ''ı tıklatarak aynı şekilde.
   
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

## <a name="step-3-create-and-run-your-pipeline"></a>3. Adım: İşlem hattınızı oluşturma ve çalıştırma
Son olarak, biz ayarlamak ve Azure Data Factory'de hello ardışık düzen çalıştırın.  Bu hello gerçek veri taşıma tamamlayan hello işlemdir.  SQL Data Warehouse ve Azure Data Factory ile tamamlayabilirsiniz hello operations tam görünümünü bulabilirsiniz [burada][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

Hello 'Geliştir ve Dağıt' bölümüne, 'Başka komutlar' ardından 'Yeni işlem hattı' öğesini tıklatın.  Merhaba işlem hattını oluşturduktan sonra kodu tootransfer hello veri tooyour veri ambarı hello kullanabilirsiniz:

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

## <a name="next-steps"></a>Sonraki adımlar
toolearn daha görüntüleyerek başlatın:

* [Azure Data Factory öğrenme yolu][Azure Data Factory learning path].
* [Azure SQL Veri Ambarı Bağlayıcısı][Azure SQL Data Warehouse Connector]. Bu, Azure SQL Data Warehouse ile Azure Data Factory kullanma hello temel başvuru konu başlığıdır.

Bu konu başlıklarında Azure Data Factory hakkında ayrıntılı bilgi sağlanmıştır. Azure SQL Database veya HDInsight ele ancak hello bilgiler tooAzure SQL Data Warehouse için de geçerlidir.

* [Öğretici: Azure Data Factory ile çalışmaya başlama] [ Tutorial: Get started with Azure Data Factory] bu Azure Data Factory ile veri işlemeye hello temel öğreticidir. Bu öğreticide, Hdınsight tootransform kullanan ilk işlem hattınızı oluşturma ve web günlüklerini aylık olarak analiz edin. Not: Bu öğreticide herhangi bir kopyalama etkinliği yoktur.
* [Öğretici: Azure Storage Blobuna tooAzure SQL veritabanı ' veri kopyalama][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. Bu öğreticide, Azure Storage Blobuna tooAzure SQL veritabanı ' Azure Data Factory toocopy veri işlem hattı oluşturun.

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
