---
title: Azure SQL Data Warehouse aaaLoad verisine | Microsoft Docs
description: "Merhaba ortak senaryolar için veri SQL Data Warehouse'a veri yükleme hakkında bilgi edinin. Bunlar PolyBase, Azure blob depolama, düz dosyalar ve disk sevkiyat kullanarak içerir. Üçüncü taraf araçları da kullanabilirsiniz."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse'a veri yükleme
Merhaba senaryo seçenekleri ve SQL Data Warehouse'a veri yükleme ile ilgili öneriler özeti.

veri yükleme hello en zor bir parçası genellikle hello veri hello yük için hazırlanıyor. Azure yükleme Azure blob depolama ortak bir veri deposu olarak pek çok hello Hizmetleri kullanarak basitleştirir ve Azure Data Factory kullanarak tooorchestrate iletişim ve veri taşıma arasında hello Azure Hizmetleri. Bu işlemler, SQL Data Warehouse'a (MPP) tooload verileri Azure blob depolama biriminden paralel yüksek düzeyde paralel işleme kullanan PolyBase teknolojisi ile tümleştirilir. 

Örnek veritabanları yükleme öğreticileri için bkz: [örnek veritabanları yükleme][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Azure blob depolama alanından yükleme
Merhaba hızlı şekilde tooimport SQL veri ambarında toouse PolyBase tooload verileri Azure blob depolama biriminden verilerdir. PolyBase kullanan SQL Data Warehouse's (MPP) tasarım tooload verileri Azure blob depolama biriminden paralel yüksek düzeyde paralel işleme. toouse PolyBase, T-SQL komutlarıyla veya bir Azure Data Factory işlem hattı kullanabilirsiniz.

### <a name="1-use-polybase-and-t-sql"></a>1. PolyBase ve T-SQL kullanın
Yükleme işlemi özeti:

1. Veri tooAzure blob depolama veya Azure Data Lake Store taşıyın ve metin dosyalarında depolar.
2. SQL veri ambarı toodefine hello konumu ve hello veri biçimini dış nesneleri yapılandırma
3. Bir T-SQL komut tooload hello verileri paralel olarak yeni bir veritabanı tablosuna çalıştırın.

<!-- 5. Schedule and run a loading job. --> 

Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (PolyBase) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Azure Data Factory'i kullanma
Bir basit yol toouse için PolyBase, Azure blob depolama biriminden PolyBase tooload verileri SQL Data Warehouse'a veri kullanan bir Azure Data Factory işlem hattı oluşturabilirsiniz. Toodefine hello T-SQL nesneleri gerekmeyen beri hızlı tooconfigure budur. İçe aktarmadan tooquery hello dış veri ihtiyacınız varsa, T-SQL kullanın. 

Yükleme işlemi özeti:

1. Veri tooAzure blob depolama alanınızın taşıyın ve metin dosyalarında depolar. Azure Data Factory şu anda PolyBase ile ADLS bağlantısı desteklemez).
2. Bir Azure Data Factory işlem hattı tooingest hello veri oluşturun. Merhaba PolyBase seçeneğini kullanın.
4. Zamanlama ve hello ardışık düzen çalıştırın.

Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (Azure Data Factory) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>SQL Server'dan yükleme
SQL Server tooSQL veri ambarı Integration Services (SSIS), kullanabileceğiniz tooload verileri düz dosya aktarımı veya diskleri tooMicrosoft sevk. Üzerinde toosee hello işlemleri ve bağlantıları tootutorials yüklenirken farklı özetini okuyun.

tooplan veri ambarı, SQL Server tooSQL tam veri geçişini bkz hello [geçişine genel bakış][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Integration Services (SSIS) kullanın
İçinde SQL Server Integration Services (SSIS) paketleri tooload zaten kullanıyorsanız, paketleri toouse SQL Server hello kaynak ve SQL Data Warehouse hello hedef olarak olarak güncelleştirebilirsiniz. Bu hızlı ve kolay toodo ve, yükleme toomigrate çalışmıyorsanız iyi bir seçimdir işlem zaten hello bulutta toouse veri. Merhaba kolaylığını hello yük bu SSIS paralel olarak hello yük gerçekleştirmez çünkü PolyBase kullanmaktan daha yavaş olacaktır ' dir.

Yükleme işlemi özeti:

1. Integration Services paketini toopoint toohello SQL Server örneğinizi hello kaynağı için ve hello SQL Data Warehouse veritabanı hello hedef için gözden geçirin.
2. Bunu zaten yoksa, şema tooSQL veri ambarı geçirin.
3. Değişiklik hello paketlerinizi eşlemesindeki SQL Data Warehouse tarafından desteklenen hello veri türlerini kullanın.
4. Zamanlama ve hello paketini çalıştırın.

Bir öğretici için bkz: [SQL veri ambarı (SSIS) SQL Server tooAzure veri yükleme][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>AZCopy (< 10 TB veri için önerilir) kullanın
Veri boyutu < 10 TB ise, hello veri SQL Server tooflat dosyalarından dışarı aktarabilir, hello dosyaları tooAzure blob depolama kopyalayın ve sonra PolyBase tooload hello verileri SQL Data Warehouse'a kullanın

Yükleme işlemi özeti:

1. Merhaba bcp komut satırı yardımcı programını tooexport verileri SQL Server tooflat dosyalarını kullanın.
2. Düz dosyalar tooAzure blob depolama biriminden Hello AZCopy komut satırı yardımcı programını toocopy verileri kullanın.
3. PolyBase tooload SQL Data Warehouse'a kullanın.

Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (PolyBase) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>BCP kullanın
Az miktarda veriniz varsa, doğrudan Azure SQL Data Warehouse'a bcp tooload kullanabilirsiniz.

Yükleme işlemi özeti:

1. Merhaba bcp komut satırı yardımcı programını tooexport verileri SQL Server tooflat dosyalarını kullanın.
2. Bcp tooload verileri düz kullan doğrudan tooSQL veri ambarı dosyaları.

Bir öğretici için bkz: [SQL veri ambarı (bcp) SQL Server tooAzure veri yükleme][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>İçeri/dışarı aktarma (> 10 TB veri için önerilir) kullanın
Veri boyutu > 10 TB'tır ve toomove istiyorsanız bunu tooAzure, öneririz hizmet sevkiyat bizim disk kullanmak [içeri/dışarı aktarma][Import/Export]. 

Yükleme işlemi özeti

1. SQL Server tooflat dosyalarından aktarılabilir disklerde Hello bcp komut satırı yardımcı programını tooexport verileri kullanın.
2. Merhaba diskleri tooMicrosoft birlikte.
3. Microsoft hello verileri SQL Data Warehouse'a veri yükler.

## <a name="load-from-hdinsight"></a>Hdınsight'ta yükleme
SQL veri ambarı veri PolyBase aracılığıyla hdınsight'tan destekler. Hello işlemi olan hello PolyBase tooconnect tooHDInsight tooload verileri kullanarak olan Azure Blob depolama alanından - verileri yüklenirken aynıdır. 

### <a name="1-use-polybase-and-t-sql"></a>1. PolyBase ve T-SQL kullanın
Yükleme işlemi özeti:

1. Veri tooHDInsight taşıyın ve metin dosyalarını saklamak ORC veya Parquet biçimi.
2. Dış nesneleri, SQL Data Warehouse toodefine hello konumu ve hello veri biçimini yapılandırın.
3. Bir T-SQL komut tooload hello verileri paralel olarak yeni bir veritabanı tablosuna çalıştırın.

Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (PolyBase) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Öneriler
Ortaklarımızın çoğunun çözümleri yüklenirken vardır. Daha fazla bilgi, toofind listesini görmek bizim [çözüm ortakları][solution partners]. 

Verilerinizi ilişkisel olmayan bir kaynaktan geldiğinden ve içine SQL veri ambarı tooload tootransform gerekir istiyorsanız satırları ve sütunları, yükleme önce içine. Dönüştürülen hello verileri veritabanında depolanan toobe gerek yoktur, metin dosyalarından depolanabilir.

Yeni yüklenen verilere ilişkin istatistikler oluşturun. Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.  Sipariş tooget hello en iyi performans, sorgularından, tüm tabloların hello sonra tüm sütunları toocreate istatistik ilk yükleme veya hello verilerde önemli değişikliklerden önemlidir.  Ayrıntılar için bkz [istatistikleri][Statistics].

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: Merhaba [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
