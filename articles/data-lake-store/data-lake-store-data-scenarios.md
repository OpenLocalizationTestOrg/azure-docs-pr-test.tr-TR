---
title: "Data Lake Store içeren aaaData senaryoları | Microsoft Docs"
description: "Farklı senaryolar hello ve hangi verileri kullanarak araçlar için alınan, işlenen, yüklenen ve bir Data Lake Store'da görselleştirilen anlamak"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Azure Data Lake Store için büyük veri gereksinimleri kullanma
Büyük veri işleme, dört anahtar aşamaları şunlardır:

* Bir veri deposuna gerçek zamanlı veya toplu büyük miktarlarda veri alma
* Merhaba veri işleme
* Merhaba veri indirme
* Merhaba veri Görselleştirme

Bu makalede, biz bu aşamalarda saygı tooAzure Data Lake Store toounderstand hello seçenekleri ve araçlar kullanılabilir toomeet ile büyük veri gereksinimlerinizi arayın.

## <a name="ingest-data-into-data-lake-store"></a>Data Lake Store veri alma
Bu bölümde, bu verileri bir Data Lake Store dikkate alınan veri ve hello farklı yöntemle hello farklı kaynakları vurgular.

![Data Lake Store veri alma](./media/data-lake-store-data-scenarios/ingest-data.png "Data Lake Store veri alma")

### <a name="ad-hoc-data"></a>Geçici verileri
Bu, daha küçük veri kümeleri temsil eden bir büyük veri uygulaması için prototipi oluşturulurken kullanılan. Geçici veri alma hello veri kaynağı olarak hello bağlı olarak farklı yolu vardır.

| Veri kaynağı | Kullanarak alma |
| --- | --- |
| Yerel bilgisayar |<ul> <li>[Azure Portal](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Azure platformlar arası CLI 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Visual Studio için Data Lake Araçları'nı kullanarak](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Azure depolama blobunu |<ul> <li>[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[AdlCopy aracı](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Hdınsight küme üzerinde çalışan Distcp'yi](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Akışa
Bu uygulamalar, cihazlar, algılayıcılar, vb. gibi çeşitli kaynaklardan tarafından oluşturulan verileri temsil eder. Bu verileri bir Data Lake Store çeşitli araçları tarafından alınan. Bu araçlar genellikle yakalamak ve işlem hello verileri bir olay olayı olarak gerçek zamanlı ve böylece daha fazla işlenebilir hello olayları toplu olarak Data Lake Store yazın.

Kullanabileceğiniz araçlar şunlardır:

* [Azure Stream Analytics](../stream-analytics/stream-analytics-data-lake-output.md) -Event Hubs'a alınan olayları yazılabilir tooAzure Data Lake Azure Data Lake Store çıkış kullanan.
* [Azure Hdınsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) -tooData Lake deposundan hello doğrudan Storm kümesi veri yazabilirsiniz.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) – olayları olay hub'larından almak ve ardından hello kullanarak tooData Lake Store yazma [Data Lake Store .NET SDK](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>İlişkisel veri
Ayrıca, ilişkisel veritabanlarından veri kaynağı. Bir süre boyunca, büyük miktarlarda verinin büyük veri kanalı yoluyla işlenen anahtar Öngörüler sağlayabilen ilişkisel veritabanları toplayın. Data Lake Store içinde bu tür veriler araçları toomove aşağıdaki hello kullanabilirsiniz.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Web sunucu günlüğü verileri (karşıya yükleme kullanarak özel uygulamalar)
Web sunucu günlüğü verileri analizini yaygın kullanılan bir örnek büyük veri uygulamaları için ve günlük dosyaları toobe büyük miktarda toohello Data Lake Store karşıya gerektirir çünkü bu veri kümesi türü özellikle çağırılır. Kendi komut dosyaları veya uygulamaları tooupload araçları toowrite aşağıdaki hello kullanabilirsiniz Bu tür veriler.

* [Azure platformlar arası CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake Store .NET SDK'sı](data-lake-store-get-started-net-sdk.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

Web sunucu günlüğü verileri karşıya yükleme için ve ayrıca verileri (örneğin sosyal düşüncelerin) diğer tür karşıya yükleme için iyi bir verdiğinden bu toowrite kendi özel komut dosyaları/uygulamaları yaklaşımını olan bileşen parçası olarak karşıya yükleme, verilerinizi esneklik tooinclude hello daha büyük büyük veri uygulamanızın. Bazı durumlarda bu kodu bir komut dosyası veya basit komut satırı yardımcı programı hello form alabilir. Diğer durumlarda, hello kod kullanılan toointegrate büyük veri işleme iş uygulaması ya da çözüm olabilir.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Azure Hdınsight kümeleri ile ilgili veriler
Çoğu Hdınsight küme türleri (Hadoop, HBase, Storm) Data Lake Store veri depolama depo olarak destekler. Hdınsight kümeleri, Azure Storage Blobları (WASB) veri erişim. Daha iyi performans için hello kümesi ile ilişkili bir Data Lake Store hesabında WASB hello veri kopyalayabilirsiniz. Aşağıdaki araçlar toocopy hello veri hello kullanabilirsiniz.

* [Apache Distcp'yi](data-lake-store-copy-data-wasb-distcp.md)
* [AdlCopy hizmeti](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Şirket içi veya Iaas Hadoop kümeleri veriler
Büyük miktarlarda verinin yerel olarak HDFS kullanarak makinelerde varolan Hadoop kümeleri depolanabilir. Merhaba Hadoop kümeleri bir şirket içi dağıtımda olabilir veya Azure Iaas kümede içinde olabilir. Bu tür veri tooAzure Data Lake Store tek seferlik bir yaklaşım için veya yinelenen bir şekilde gereksinimleri toocopy olabilir. Bu tooachieve kullanabileceğiniz çeşitli seçenekler vardır. Merhaba dengelemeler ilişkili ve alternatifleri listesi aşağıda verilmiştir.

| Yaklaşım | Ayrıntılar | Avantajları | Dikkat edilmesi gerekenler |
| --- | --- | --- | --- |
| Azure veri fabrikası (ADF) toocopy verileri doğrudan Hadoop kümeleri tooAzure Data Lake Deposu'ndan veri kullanın |[ADF HDFS bir veri kaynağı olarak destekler.](../data-factory/data-factory-hdfs-connector.md) |ADF HDFS ve ilk sınıfı uçtan uca yönetim ve izleme Giden kutusu desteği sağlar |Veri Yönetimi ağ geçidi toobe şirket içi dağıtılan gerektirir veya hello Iaas kümesi |
| Verilerin Hadoop'tan dosyaları olarak dışarı aktarın. Daha sonra uygun mekanizmayı kullanarak hello dosyaları tooAzure Data Lake Store kopyalayın. |Data Lake Store tooAzure dosyalarla kopyalayabilirsiniz: <ul><li>[Windows işletim sistemi için Azure PowerShell](data-lake-store-get-started-powershell.md)</li><li>[Azure platformlar arası CLI 2.0 Windows olmayan işletim için](data-lake-store-get-started-cli-2.0.md)</li><li>Tüm Data Lake Store SDK kullanarak özel uygulama</li></ul> |Hızlı tooget başlatıldı. Özelleştirilmiş yüklemeleri yapabilirsiniz |Birden çok teknoloji içerir çok adımlı işlemi. Yönetim ve izleme toobe bir sınama sağlanan süre özelleştirilmiş hello yapısını hello araçları büyüyecektir |
| Hadoop tooAzure depolama Distcp'yi toocopy verileri kullanın. Ardından verileri Azure depolama tooData Lake uygun mekanizma kullanılarak deposundan kopyalayabilirsiniz. |Azure depolama tooData Lake Store kullanarak veri kopyalayabilirsiniz: <ul><li>[Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)</li><li>[AdlCopy aracı](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Apache Hdınsight kümelerinde çalışan Distcp'yi](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |Açık kaynaklı araçları kullanabilirsiniz. |Birden çok teknoloji içerir çok adımlı işlemi |

### <a name="really-large-datasets"></a>Gerçekten büyük veri kümeleri
Birkaç terabayta aralığı veri kümelerini yüklemek için yukarıda açıklanan hello yöntemlerle bazen yavaş ve pahalı olabilir. Böyle durumlarda, aşağıdaki hello seçeneklerini kullanabilirsiniz.

* **Azure ExpressRoute kullanarak**. Azure ExpressRoute, şirket içinde Azure veri merkezleri ile altyapı arasında özel bağlantılar oluşturmanızı sağlar. Bu, büyük miktarlarda veri aktarmak için güvenilir bir seçenek sağlar. Daha fazla bilgi için bkz: [Azure ExpressRoute belgeleri](../expressroute/expressroute-introduction.md).
* **"Çevrimdışı", verilerin karşıya**. Azure ExpressRoute kullanarak herhangi bir nedenle uygun değilse, kullanabileceğiniz [Azure içeri/dışarı aktarma hizmeti](../storage/common/storage-import-export-service.md) tooship sabit disk sürücüleri, veri tooan Azure veri merkezi. Verilerinizi ilk karşıya yüklenen tooAzure depolama BLOB sayısıdır. Daha sonra [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) veya [AdlCopy aracı](data-lake-store-copy-data-azure-storage-blob.md) toocopy verileri Azure depolama BLOB'lar tooData Lake deposu.

  > [!NOTE]
  > İçeri/dışarı aktarma hizmeti kullanma hello sırada tooAzure veri sevk diskleri merkezi hello hello dosya boyutlarına 195 GB'den büyük olmamalıdır.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Data Lake Store içinde depolanan verileri işleme
Merhaba veri Data Lake Store'da kullanılabilir olduğunda, analiz hello kullanarak verileri büyük veri uygulamaları desteklenen üzerinde çalışabilir. Şu anda, Data Lake Store'da depolanan hello verileri Azure Hdınsight ve Azure Data Lake Analytics toorun veri analizi işleri kullanabilirsiniz.

![Data Lake Store'da verileri çözümlemek](./media/data-lake-store-data-scenarios/analyze-data.png "Data Lake Store'da verileri analiz etme")

Örnek hello bakabilirsiniz.

* [Hdınsight kümesi Data Lake Store ile depolama alanı olarak oluşturun.](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Data Lake Deposu'ndan veri veri indirin
Ayrıca toodownload istediğiniz veya gibi senaryolar için veri Azure Data Lake Deposu'ndan veri taşıma:

* Mevcut veri işlem hatlarınızı ile veri tooother depoları toointerface taşıyın. Örneğin, Data Lake Store tooAzure SQL veritabanı toomove verilerden isteyebilirsiniz veya şirket içi SQL Server.
* Veri tooyour yerel bilgisayarda uygulama prototipleri oluştururken işleme IDE ortamlarda indirin.

![Çıkış Data Lake Store verilerden](./media/data-lake-store-data-scenarios/egress-data.png "çıkış Data Lake Store verileri")

Böyle durumlarda, aşağıdaki seçenekleri şu hello kullanabilirsiniz:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
* [Apache Distcp'yi](data-lake-store-copy-data-wasb-distcp.md)

Kendi komut dosyası/uygulama toodownload verilerinizi Data Lake Deposu'ndan veri yöntemleri toowrite aşağıdaki hello de kullanabilirsiniz.

* [Azure platformlar arası CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake Store .NET SDK'sı](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Data Lake Store'da verileri görselleştirin
Hizmetleri toocreate görsel gösterimi Data Lake Store içinde depolanan verileri bir karışımını kullanabilirsiniz.

![Data Lake Store'da verileri görselleştirin](./media/data-lake-store-data-scenarios/visualize-data.png "Data Lake Store'da verileri görselleştirin")

* Kullanarak başlatabilirsiniz [Azure Data Factory toomove verileri Data Lake Store tooAzure SQL veri ambarı](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Bundan sonra şunları yapabilirsiniz [Power BI ile Azure SQL veri ambarı tümleştirmek](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) hello veri toocreate görsel gösterimi.
