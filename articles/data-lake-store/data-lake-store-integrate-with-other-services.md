---
title: "Data Lake Store diğer Azure hizmetleriyle aaaIntegrating | Microsoft Docs"
description: "Data Lake Store diğer Azure hizmetleriyle nasıl tümleşik çalıştığını anlamak"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Data Lake Store’u diğer Azure Hizmetleri ile tümleştirme
Azure Data Lake Store, diğer Azure Hizmetleri tooenable geniş bir senaryo ile birlikte kullanılabilir. Merhaba aşağıdaki makalede Data Lake Store ile tümleştirilebilir hello Hizmetleri listelenmektedir.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Kullanım Data Lake Store Azure Hdınsight ile
Kaynak sağlayabilirsiniz bir [Azure Hdınsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) Data Lake Store hello HDFS uyumlu depolama alanı olarak kullanan kümesi. Bu sürümde, Windows ve Linux, Hadoop ve Storm kümeleri için Data Lake Store yalnızca ek depolama alanı kullanabilirsiniz. Bu tür kümeler hala Azure Storage (WASB) hello varsayılan depolama alanı olarak kullanın. Ancak, Windows ve Linux üzerinde HBase kümeleri için Data Lake Store hello varsayılan depolama veya ek depolama alanı ya da her ikisini de kullanabilirsiniz.

Nasıl tooprovision bir Hdınsight kümesini Data Lake Store ile ilgili yönergeler için bkz:

* [Azure Portal'ı kullanarak Data Lake Store ile Hdınsight kümesi sağlama](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Azure PowerShell kullanarak varsayılan depolama alanı olarak bir Hdınsight kümesini Data Lake Store sağlama](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Azure PowerShell kullanarak ek depolama alanı bir Hdınsight kümesini Data Lake Store sağlama](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Azure Data Lake Analytics ile kullanım veri Gölü deposu
[Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-overview.md) bulut ölçeğinde büyük verilerle toowork sağlar. Dinamik olarak kaynaklar sağlar ve terabayt ve hatta eksabayt desteklenen veri kaynakları, bir Data Lake Store olan tanesine sayısında depolanan veriler üzerinde analiz gerçekleştirmenize olanak tanır. Data Lake Analytics ile Azure Data Lake Store - büyük veri iş yüklerini performansı, verimliliği ve paralelleştirmeyi sizin için en yüksek düzeyde hello sağlayan özel en iyi duruma getirilmiş toowork ' dir.

Yönergeler için bkz: toouse Data Lake Analytics Data Lake Store ile [Data Lake Store'ı kullanarak Data Lake Analytics ile çalışmaya başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Kullanım Data Lake Store ile Azure veri fabrikası
Kullanabileceğiniz [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) Azure tabloları, Azure SQL Database, Azure SQL veri ambarı, Azure Storage Bloblarında ve şirket içi veritabanlarını tooingest verileri. Birinci sınıf vatandaşı hello Azure ekosistemi olmasının, Azure Data Factory kullanılan tooorchestrate hello alım bu kaynak tooAzure Data Lake Store verileri olabilir.

Yönergeler için Azure Data Factory Data Lake Store ile nasıl toouse bkz [veri tooand Data Factory kullanarak Data Lake Deposu'ndan veri taşıma](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Verileri Azure Storage Bloblarından Data Lake Store kopyalayın.
Azure Data Lake Store toocopy verileri Azure Blob depolama biriminden bir Data Lake Store hesabına sağlar AdlCopy, bir komut satırı aracı sağlar. Daha fazla bilgi için bkz: [Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Azure SQL veritabanı ve Data Lake Store arasında veri kopyalama
Apache Sqoop tooimport kullanın ve Azure SQL veritabanı ve Data Lake Store arasında veri dışarı aktarabilirsiniz. Daha fazla bilgi için bkz: [Data Lake Store ile Sqoop kullanarak Azure SQL veritabanı arasında veri kopyalama](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Kullanım Data Lake Store ile akış analizi
Merhaba birini kullanarak Azure Stream Analytics akışı toostore verilerin çıktısını alır, Data Lake Store kullanabilirsiniz. Daha fazla bilgi için bkz: [akış Azure depolama Blob verileri Azure akış analizi kullanarak Data Lake Store](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Kullanım Data Lake Store Power BI ile
Bir Data Lake Store hesabı tooanalyze Power BI tooimport verileri kullanan ve hello verileri görselleştirin. Daha fazla bilgi için bkz: [Power BI kullanarak Data Lake Store verileri çözümlemek](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Kullanım Data Lake Store veri Kataloğu ile
Data Lake Store verisine hello Azure veri Kataloğu toomake hello veri hello kuruluş genelinde bulunabilirlik kaydedebilirsiniz. Daha fazla bilgi için bkz: [Data Lake Store verileri Azure veri Kataloğu'nda kaydetmek](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Kullanım Data Lake Store ile SQL Server Integration Services (SSIS)
SSIS tooconnect SSIS paketi Azure Data Lake Store ile hello Azure Data Lake Store Bağlantı Yöneticisi'ni kullanabilirsiniz. Daha fazla bilgi için bkz: [kullanım Data Lake Store SSIS ile](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Kullanım Data Lake Store ile SQL veri ambarı
Azure Data Lake Deposu'ndan veri PolyBase tooload verileri SQL Data Warehouse'a kullanabilirsiniz. Daha fazla bilgi için bkz: [kullanım Data Lake Store ile SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Portal kullanarak Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* [PowerShell kullanarak Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-powershell.md)  

