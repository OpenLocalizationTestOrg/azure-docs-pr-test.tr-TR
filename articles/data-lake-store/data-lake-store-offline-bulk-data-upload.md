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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Veri tooData Lake deposu çevrimdışı kopyası için Hello Azure içeri/dışarı aktarma hizmeti kullanma
Bu makalede, nasıl toocopy çok büyük veri ayarlar öğreneceksiniz (> 200 GB) hello gibi çevrimdışı kopya yöntemleri kullanarak bir Azure Data Lake Store içine [Azure içeri/dışarı aktarma hizmeti](../storage/common/storage-import-export-service.md). Özellikle, bu makaledeki örnek olarak kullanılan hello 339,420,860,416 bayt ya da yaklaşık 319 GB disk üzerindeki dosyasıdır. Şimdi bu dosya 319GB.tsv çağırın.

Hello Azure içeri/dışarı aktarma hizmeti, büyük miktarlarda veri daha fazla güvenli bir şekilde tooAzure Blob Depolama sevkiyat sabit disk tarafından tooan Azure veri merkezi sürücüleri tootransfer yardımcı olur.

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure depolama hesabı**.
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Merhaba verileri hazırlama
Merhaba içeri/dışarı aktarma hizmeti kullanmadan önce sonu hello veri dosyası toobe aktarılan **200 GB daha az olan kopyaları içine** boyutu. Merhaba içeri aktarma aracını 200 GB'den büyük dosyalarla çalışmaz. Bu öğreticide, biz 100 GB öbeklere hello dosya bölün. Kullanarak bunu yapabilirsiniz [Cygwin](https://cygwin.com/install.html). Cygwin Linux komutları destekler. Bu durumda, komutu aşağıdaki hello kullan:

    split -b 100m 319GB.tsv

Merhaba bölme işlemi ile Merhaba adları aşağıdaki dosyaları oluşturur.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Veri diskleri hazırlanın
Merhaba yönergeleri izleyin [hello Azure içeri/dışarı aktarma hizmeti kullanma](../storage/common/storage-import-export-service.md) (Merhaba altında **sürücülerinizin hazırlama** bölüm) tooprepare sabit sürücüler. İşte hello genel dizisi:

1. Hello Azure içeri/dışarı aktarma hizmeti için kullanılan hello gereksinim toobe karşılayan bir sabit disk temin edin.
2. Sevk edilen toohello Azure veri merkezi sonra hello veri kopyalanacağı bir Azure depolama hesabı belirleyin.
3. Kullanım hello [Azure içeri/dışarı aktarma aracı](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), bir komut satırı yardımcı programı. Nasıl toouse hello aracı gösteren bir örnek parçacığı aşağıda verilmiştir.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Bkz: [hello Azure içeri/dışarı aktarma hizmeti kullanma](../storage/common/storage-import-export-service.md) daha fazla örnek kod parçacıkları için.
4. Merhaba yukarıdaki komut bir günlük oluşturur hello dosyasını belirtilen konum. Bu günlük dosyası toocreate hello alma işleminden kullanmak [Klasik Azure portalı](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Bir içeri aktarma işi oluşturma
Hello konusundaki yönergeleri kullanarak, bir içeri aktarma işi şimdi oluşturabilirsiniz [hello Azure içeri/dışarı aktarma hizmeti kullanma](../storage/common/storage-import-export-service.md) (Merhaba altında **oluşturma hello alma işi** bölümü). Bu içeri aktarma işi için diğer ayrıntılarla hello disk sürücüleri hazırlanırken oluşturduğunuz hello günlük dosyası da sağlar.

## <a name="physically-ship-hello-disks"></a>Fiziksel olarak hello diskleri sevk
Merhaba diskleri tooan Azure veri merkezi şimdi fiziksel olarak gönderebilirsiniz. Burada, hello veriler hello alma işi oluşturulurken sağlanan toohello Azure Storage blobları üzerinden kopyalanır. İzleme bilgileri daha sonra tooprovide hello ettiyseniz ayrıca hello iş oluşturulurken şimdi izleme numarası tooyour alma işi ve güncelleştirme hello dönebilirsiniz.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Verileri Azure Storage blobları tooAzure Data Lake Deposu'ndan veri kopyalama
Merhaba Hello durumunu sonra alma işi tamamlandığında, hello veri belirtilen hello Azure Storage bloblarında kullanılabilir olup olmadığını doğrulayabilirsiniz gösterir. Daha sonra hello verilerden tooAzure Data Lake Store BLOB yöntemleri toomove çeşitli kullanabilirsiniz. Tüm veri yüklemek için kullanılabilir seçenekler hello için bkz: [Data Lake Store veri alma](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

Bu bölümde, hello JSON tanımlarla toocreate bir Azure Data Factory işlem hattı verileri kopyalamak için kullanabilirsiniz sunuyoruz. Bu JSON tanımları hello kullanabilirsiniz [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), veya [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Bağlantılı kaynak hizmeti (Azure Storage blobu)
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

### <a name="target-linked-service-azure-data-lake-store"></a>Bağlantılı hizmet (Azure Data Lake Store) hedef
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
### <a name="input-data-set"></a>Giriş veri kümesi
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
### <a name="output-data-set"></a>Çıktı veri kümesi
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
### <a name="pipeline-copy-activity"></a>Etkinliğiniz (kopyalama etkinliği)
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
Daha fazla bilgi için bkz: [verileri Azure depolama biriminden blob Azure Data Factory kullanarak tooAzure Data Lake Store taşıma](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Azure Data Lake Store'da Hello veri dosyalarını yeniden yapılandırma
319 GB ve böylece hello Azure içeri/dışarı aktarma hizmetini kullanarak aktarılabilir, daha küçük boyutu dosyalarına ihlal dosyası ile başlatıldı. Azure Data Lake Store'da Hello veridir, biz hello dosya tooits özgün boyutunu yeniden oluşturabilir. Azure PowerShell cmldts toodo şekilde aşağıdaki hello kullanabilirsiniz.

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

## <a name="next-steps"></a>Sonraki adımlar
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
