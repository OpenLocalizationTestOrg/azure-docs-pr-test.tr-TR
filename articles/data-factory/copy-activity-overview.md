---
title: "Kopya etkinliği Azure Data Factory'de | Microsoft Docs"
description: "Verileri bir desteklenen kaynak veri deposundan desteklenen havuz veri deposuna kopyalamak için kullanabileceğiniz Azure Data Factory kopyalama etkinliğinde öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2018
ms.author: jingwang
ms.openlocfilehash: 2095d75ed042ae8be02ae0a1570f8e77d06a3563
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/19/2018
---
# <a name="copy-activity-in-azure-data-factory"></a>Azure Data Factory kopyalama etkinliği

## <a name="overview"></a>Genel Bakış

> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Sürüm 1 - Genel Kullanım](v1/data-factory-data-movement-activities.md)
> * [Sürüm 2 - Önizleme](copy-activity-overview.md)

Azure Data Factory'de veri arasında veri depoları şirket içinde ve bulutta kopyalamak için kopyalama etkinliği kullanabilirsiniz. Verileri kopyaladıktan sonra daha fazla dönüştürülen ve analiz edilebilir. Kopyalama etkinliği, dönüştürme ve iş zekası (BI) ve uygulama tüketimi için çözümleme sonuçlarını yayımlamak için de kullanabilirsiniz.

![Kopyalama etkinliği rolü](media/copy-activity-overview/copy-activity.png)

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Genel olarak kullanılabilir (GA) Data Factory Hizmeti'ne 1 sürümünü kullanıyorsanız bkz [V1 kopyalama etkinliği](v1/data-factory-data-movement-activities.md).

Kopyalama Etkinliği yürütüldüğünde bir [tümleştirmesi çalışma zamanı](concepts-integration-runtime.md). Farklı veri kopyalama senaryosu için Integration zamanının farklı özellik de kullanılabilir:

* Veriler arasında veri kopyalama hem de genel olarak erişilebilir depoladığında kopyalama etkinliği tarafından yetkilendirilmiş **Azure tümleştirmesi çalışma zamanı**, güvenli, güvenilir ve ölçeklenebilir ve [genel olarak kullanılabilir](concepts-integration-runtime.md#integration-runtime-location).
* Bulunan şirket içi veri kopyalama/veri depolarına veya ayarlamak gereken erişim denetimi (örneğin, Azure sanal ağı) içeren bir ağda olduğunda bir **tümleşik çalışma zamanı'kendi kendini barındıran** veri kopyalama güçlendirmeniz.

Tümleştirme çalışma zamanı her kaynak ve havuz veri deposuyla ilişkilendirilmiş olması gerekir. Ayrıntılı bilgi kopyalama etkinliğini [kullanmak için hangi IR belirler](concepts-integration-runtime.md#determining-which-ir-to-use).

Kopya etkinliği bir havuz için bir kaynaktan verileri kopyalamak için aşağıdaki aşamaları geçer. Kopyalama etkinliği'nın temelini oluşturan hizmeti:

1. Veri kaynağına veri deposundan okur.
2. Serileştirme/seri durumdan çıkarma, sıkıştırma/açma, sütun eşlemesi, vb. gerçekleştirir. Girdi veri kümesi, çıktı veri kümesi ve kopyalama etkinliği yapılandırmalarını temel alan bu işlemleri yapar.
3. Havuz/hedef veri deposuna verileri yazar.

![Kopyalama Etkinliği’ne Genel Bakış](media/copy-activity-overview/copy-activity-overview.png)

## <a name="supported-data-stores-and-formats"></a>Desteklenen veri depoları ve biçimler

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores.md)]

### <a name="supported-file-formats"></a>Desteklenen dosya biçimleri

Kopya etkinliği için kullanabileceğiniz **olarak dosyaları kopyalama-olduğu** içinde durum verileri kopyalanır verimli bir şekilde tüm serileştirme/seri durumdan çıkarma iki dosya tabanlı veri depoları arasında.

Kopyalama etkinliği de destekler okuma ve dosyalara belirtilen biçimlerde yazma: **metin, JSON, Avro, ORC ve Parquet**ve sıkıştırma codec **GZIP, Deflate, Bzıp2 ve ZipDeflate** desteklenir. Bkz: [desteklenen dosya ve sıkıştırma biçimleri](supported-file-formats-and-compression-codecs.md) ayrıntılarla.

Örneğin, aşağıdaki kopyalama etkinliklerin yapabilirsiniz:

* Şirket içi SQL Server veri kopyalama ve Azure Data Lake Store'a ORC biçiminde yazın.
* Dosyaları metin (CSV) biçiminde şirket içi dosya sisteminden kopyalama ve Azure Blob Avro biçiminde yazın.
* Şirket içi dosya sisteminden daraltılmış dosyaları kopyalayın ve Azure Data Lake Store'a kara açın.
* Verileri Azure Blob'tan GZip sıkıştırılmış metin (CSV) biçiminde kopyalayın ve Azure SQL veritabanına yazma.

## <a name="supported-regions"></a>Desteklenen bölgeler

Kopyalama etkinliği'nın temelini oluşturan hizmeti genel bölgelerde kullanılabilir ve farklı coğrafyalara listelenen [Azure tümleştirmesi çalışma zamanı konumları](concepts-integration-runtime.md#integration-runtime-location). Genel olarak kullanılabilir topoloji genellikle çapraz bölge atlama önler verimli veri taşıma sağlar. Bkz: [bölgeye göre Hizmetleri](https://azure.microsoft.com/regions/#services) Data Factory ve veri taşıma bir bölgede kullanılabilirliği.

## <a name="configuration"></a>Yapılandırma

Kopya etkinliği Azure Data Factory içinde kullanmak için aktarmanız gerekir:

1. **Kaynak veri deposu ve havuz veri deposu için bağlı hizmetleri oluşturun.** Nasıl yapılandırılacağı ve desteklenen özellikler bağlayıcı makalenin "bağlantılı hizmet özellikleri" bölümüne bakın. Desteklenen bağlayıcı listesinde bulabilirsiniz [desteklenen veri depoları ve biçimleri](#supported-data-stores-and-formats) bölümü.
2. **Kaynak ve havuz için veri kümesi oluşturun.** Bağlayıcı makaleleri "Veri kümesi özellikleri" bölümündeki nasıl yapılandırılacağı ve desteklenen özellikler havuzu ve kaynağına bakın.
3. **Kopyalama etkinliği ile işlem hattı oluşturacaksınız.** Sonraki bölümde bir örnek sağlar.  

### <a name="syntax"></a>Sözdizimi

Aşağıdaki şablonu kopyalama etkinliği, desteklenen özelliklerin kapsamlı bir liste içerir. Senaryonuza uygun olanları belirtin.

```json
"activities":[
    {
        "name": "CopyActivityTemplate",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<source dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<sink dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>",
                <properties>
            },
            "sink": {
                "type": "<sink type>"
                <properties>
            },
            "translator":
            {
                "type": "TabularTranslator",
                "columnMappings": "<column mapping>"
            },
            "cloudDataMovementUnits": <number>,
            "parallelCopies": <number>,
            "enableStaging": true/false,
            "stagingSettings": {
                <properties>
            },
            "enableSkipIncompatibleRow": true/false,
            "redirectIncompatibleRowSettings": {
                <properties>
            }
        }
    }
]
```

### <a name="syntax-details"></a>Sözdizimi ayrıntıları

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Kopyalama etkinliği tür özelliği ayarlamak: **Kopyala** | Evet |
| Girişleri | Kaynak verileri için hangi noktaları oluşturulan veri kümesi belirtin. Kopyalama etkinliği yalnızca tek bir giriş destekler. | Evet |
| çıkışlar | Hangi havuz veri noktalarına oluşturulan veri kümesi belirtin. Kopyalama etkinliği yalnızca tek bir çıktı destekler. | Evet |
| typeProperties | Kopyalama etkinliği yapılandırmak için özellikler grubu. | Evet |
| kaynak | Kopya kaynak türü ve karşılık gelen özelliklere verileri nasıl belirtin.<br/><br/>Bağlayıcı makalesinde listelenen "etkinlik özellikleri Kopyala" bölümünden daha ayrıntılı bilgi [desteklenen veri depoları ve biçimleri](#supported-data-stores-and-formats). | Evet |
| Havuz | Kopya Havuz türü ve karşılık gelen özelliklere veri yazma nasıl belirtin.<br/><br/>Bağlayıcı makalesinde listelenen "etkinlik özellikleri Kopyala" bölümünden daha ayrıntılı bilgi [desteklenen veri depoları ve biçimleri](#supported-data-stores-and-formats). | Evet |
| translator | Kaynak havuzu için açıkça bir sütun eşlemelerini belirtin. Varsayılan kopyalama davranışını gereksiniminizi gerçekleştirilemiyor uygulanır.<br/><br/>Ayrıntıları öğrenmek [şema ve veri türü eşlemesi](copy-activity-schema-and-type-mapping.md). | Hayır |
| cloudDataMovementUnits | Powerfulness belirtin [Azure tümleştirmesi çalışma zamanı](concepts-integration-runtime.md) veri kopyalama güçlendirmeniz.<br/><br/>Ayrıntıları öğrenmek [bulut veri taşıma birimleri](copy-activity-performance.md). | Hayır |
| parallelCopies | Havuz için veri kaynağı ve veri yazma ait okurken kullanılacak kopyalama etkinliği istediğiniz paralellik belirtin.<br/><br/>Ayrıntıları öğrenmek [paralel kopyalama](copy-activity-performance.md#parallel-copy). | Hayır |
| enableStaging<br/>stagingSettings | Geçici verileri doğrudan kopyalama veri havuzu kaynağından yerine aa blob storage'da hazırlamak bu seçeneği seçin.<br/><br/>Yararlı senaryoları ve yapılandırma ayrıntılarını öğrenmek [kopyalama hazırlanan](copy-activity-performance.md#staged-copy). | Hayır |
| enableSkipIncompatibleRow<br/>redirectIncompatibleRowSettings| Uyumsuz satır veri havuzu kaynağından kopyalarken ne yapılacağını seçin.<br/><br/>Ayrıntıları öğrenmek [hataya dayanıklılık](copy-activity-fault-tolerance.md). | Hayır |

## <a name="monitoring"></a>İzleme

Kopya etkinliği Azure Data Factory "Yazar & İzleyicisi" UI veya program aracılığıyla çalıştırma izleyebilirsiniz. Ardından performans ve senaryonuz için kopyalama etkinliği'nin yapılandırılmasını karşılaştırabilirsiniz [Performans başvurusu](copy-activity-performance.md#performance-reference) şirket içi sınama gelen.

### <a name="monitor-visually"></a>Görsel olarak izleme

Görsel olarak çalıştır Kopyala etkinliğini izlemek için veri fabrikası -> **Yazar & İzleyici** -> **İzleyici sekmesi**, ardışık düzen listesini çalışır bir"Görünümüetkinlikçalışır"bağlantısınabakın **Eylemler** sütun. 

![İşlem hattını izleme çalıştırır](./media/load-data-into-azure-data-lake-store/monitor-pipeline-runs.png)

Bu ardışık düzen çalıştırmada etkinliklerin listesini görmek için tıklatın. İçinde **Eylemler** sütun bağlantılarını kopyalama etkinliği giriş, çıkış, (kopyalama etkinliği çalıştırmak başarısız olursa) hataları ve ayrıntılar bulunur.

![Monitör etkinliği çalıştırır](./media/load-data-into-azure-data-lake-store/monitor-activity-runs.png)

Tıklayın "**ayrıntıları**" altında bağlantı **Eylemler** kopyalama etkinliği'nin yürütme ayrıntıları ve performans özelliklerini görmek için. Dahil olmak üzere birim/satır/dosyaları veri kopyalanan kaynak havuzu, işleme, ile ilgili süre geçtiği ve yapılandırmaları kopyalama senaryonuz için kullanılan adımları bilgiler gösterir.

**Örnek: Azure Data Lake Store için Amazon S3'ten kopyalama**
![İzleyici etkinlik çalışma ayrıntıları](./media/copy-activity-overview/monitor-activity-run-details-adls.png)

**Örnek: Azure SQL Data Warehouse kullanarak Azure SQL veritabanı kopyadan hazırlanan kopyalama**
![İzleyici etkinlik çalışma ayrıntıları](./media/copy-activity-overview/monitor-activity-run-details-sql-dw.png)

### <a name="monitor-programmatically"></a>Program aracılığıyla izleme

Kopya etkinliği yürütme ayrıntıları ve performans özellikleri de döndürülür çalıştırma sonucu kopyalama etkinliğinde çıkış bölümü ->. Kapsamlı bir liste aşağıda verilmiştir; Yalnızca kopya senaryonuza uygun ayarlara görünecektir. Çalıştırma etkinliğini izlemek öğrenin [hızlı başlangıç bölümünde izleme](quickstart-create-data-factory-dot-net.md#monitor-a-pipeline-run).

| Özellik adı  | Açıklama | Birim |
|:--- |:--- |:--- |
| DataRead | Kaynaktan okunan veri boyutu | Int64 değeri **bayt** |
| dataWritten | Havuz için yazılan veri boyutu | Int64 değeri **bayt** |
| filesRead | Dosya depolama biriminden veri kopyalama işlemi sırasında kopyalanan dosyaların sayısıdır. | Int64 değeri (birim) |
| filesWritten | Dosya depolama alanına veri kopyalama işlemi sırasında kopyalanan dosyaların sayısıdır. | Int64 değeri (birim) |
| rowsCopied | (İkili kopyası için geçerli değil) kopyalanmasını satır sayısını belirtir. | Int64 değeri (birim) |
| rowsSkipped | Geçiliyor uyumsuz satır sayısını belirtir. Set "enableSkipIncompatibleRow" true olarak özelliğini açın. | Int64 değeri (birim) |
| Üretilen iş | Aktarılan ve verileri oranı | Kayan noktalı sayıyı **KB/sn** |
| copyDuration | Kopya süresi | Saniye cinsinden Int32 değeri |
| sqlDwPolyBase | PolyBase SQL Data Warehouse'a veri kopyalama işlemi sırasında kullanılıyorsa. | Boole |
| redshiftUnload | UNLOAD Redshift veri kopyalama işlemi sırasında kullanılıyorsa. | Boole |
| hdfsDistcp | Distcp'yi HDFS veri kopyalama işlemi sırasında kullanılıyorsa. | Boole |
| effectiveIntegrationRuntime | Etkinliğin çalışma, biçiminde güçlendirmeniz tümleştirme Runtime(s) kullanılan Göster `<IR name> (<region if it's Azure IR>)`. | Metin (dize) |
| usedCloudDataMovementUnits | Kopyalama sırasında etkili bulut veri taşıma birimleri. | Int32 değeri |
| usedParallelCopies | Kopyalama sırasında etkin parallelCopies. | Int32 değeri|
| redirectRowPath | Blob depolama Atlanan uyumsuz satır günlük yolu "redirectIncompatibleRowSettings" altında yapılandırın. Örneğe bakın. | Metin (dize) |
| executionDetails | Kopyalama etkinliği, geçer aşamaları ve ilgili adımlarda, süre, kullanılan yapılandırmaları, vb. hakkında daha ayrıntılı bilgi. Bu, değişiklik gösterebileceği için bu bölümde ayrıştırmak için önerilmez. | Dizi |

```json
"output": {
    "dataRead": 107280845500,
    "dataWritten": 107280845500,
    "filesRead": 10,
    "filesWritten": 10,
    "copyDuration": 224,
    "throughput": 467707.344,
    "errors": [],
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US 2)",
    "usedCloudDataMovementUnits": 32,
    "usedParallelCopies": 8,
    "executionDetails": [
        {
            "source": {
                "type": "AmazonS3"
            },
            "sink": {
                "type": "AzureDataLakeStore"
            },
            "status": "Succeeded",
            "start": "2018-01-17T15:13:00.3515165Z",
            "duration": 221,
            "usedCloudDataMovementUnits": 32,
            "usedParallelCopies": 8,
            "detailedDurations": {
                "queuingDuration": 2,
                "transferDuration": 219
            }
        }
    ]
}
```

## <a name="schema-and-data-type-mapping"></a>Şema ve veri türü eşlemesi

Bkz: [şema ve veri türü eşlemesi](copy-activity-schema-and-type-mapping.md), kopyalama etkinliği havuz için kaynak verilerinizi nasıl eşlendiğini açıklar.

## <a name="fault-tolerance"></a>Hataya dayanıklılık

Varsayılan olarak, kopyalama etkinliği veri kopyalama durdurur ve kaynak ve havuz arasında uyumsuz veri karşılaştığında hatasını döndürür. Açıkça atlayın ve uyumsuz satırları oturum ve yalnızca kopyalama başarılı olmak için bu uyumlu veri kopyalamak için yapılandırabilirsiniz. Bkz: [kopyalama etkinliği hataya dayanıklılık](copy-activity-fault-tolerance.md) üzerinde daha ayrıntılı bilgi.

## <a name="performance-and-tuning"></a>Performans ve ayar

Bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](copy-activity-performance.md), Azure Data factory'de veri taşımayı (kopyalama etkinliği) performansını etkileyen önemli faktör açıklar. Ayrıca, iç test sırasında gözlemlenen performans listeler ve kopyalama etkinliği performansını iyileştirmek için çeşitli yollar ele alınmaktadır.

## <a name="incremental-copy"></a>Artımlı kopya 
Veri Fabrikası sürüm 2, artımlı olarak delta veri kaynağına veri deposundan hedef veri deposuna kopyalamak için senaryolarını destekler. Bkz: [Öğreticisi: artımlı olarak veri kopyalama](tutorial-incremental-copy-overview.md). 

## <a name="read-and-write-partitioned-data"></a>Bölümlenmiş verilerini okuma ve yazma
Sürüm 1'de, Azure Data Factory veri okunurken veya bölümlenmiş SliceStart/SliceEnd/WindowStart/WindowEnd sistem değişkenleri kullanılarak yazılırken desteklenir. Sürüm 2'de, ardışık düzen parametre ve tetikleyici başlangıç saati ve zamanlanan saat parametresinin değeri kullanarak bu davranışı elde edebilirsiniz. Daha fazla bilgi için bkz: [veri okumak veya yazmak nasıl bölümlenmiş](how-to-read-write-partitioned-data.md).

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki quickstarts, öğreticiler ve örnekleri bakın:

- [Veri bir konumdan aynı Azure Blob Depolama başka bir konuma kopyalayın.](quickstart-create-data-factory-dot-net.md)
- [Verileri Azure Blob depolama alanından Azure SQL veritabanına kopyalamak.](tutorial-copy-data-dot-net.md)
- [Azure için şirket içi SQL Server'dan veri kopyalama](tutorial-hybrid-copy-powershell.md)
