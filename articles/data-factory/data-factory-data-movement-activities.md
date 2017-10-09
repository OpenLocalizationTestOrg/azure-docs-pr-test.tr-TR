---
title: "Kopyalama etkinliği kullanarak aaaMove veri | Microsoft Docs"
description: "Data Factory işlem hatlarını veri taşıma hakkında bilgi edinin: Bulut depoları arasında ve bir şirket içi depolama ve bulut deposu arasındaki veri geçişi. Kopyalama etkinliği kullanın."
keywords: "veriler, veri taşıma, veri geçişi, aktarım veri kopyalama"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Kopyalama etkinliği kullanarak veri taşıma
## <a name="overview"></a>Genel Bakış
Şirket içi ve bulut arasında kopyalama etkinliği toocopy veri kullanabileceğiniz Azure Data Factory'de veri depolar. Merhaba veri kopyalandıktan sonra daha fazla dönüştürülen ve analiz edilebilir. İş Zekası (BI) ve uygulama tüketimi için kopyalama etkinliği toopublish dönüştürme ve çözümleme sonuçlarını de kullanabilirsiniz.

![Kopyalama etkinliği rolü](media/data-factory-data-movement-activities/copy-activity.png)

Kopyalama etkinliği desteklenir güvenli tarafından güvenilir ve ölçeklenebilir ve [genel olarak kullanılabilir hizmet](#global). Bu makalede, veri taşıma veri fabrikası ve kopyalama etkinliği hakkında ayrıntılar sağlar.

İlk olarak, iki bulut veri depoları arasında ve bir şirket içi veri depolama ve bulut veri deposu arasındaki veri geçişinin nasıl gerçekleştirildiğini görelim.

> [!NOTE]
> toolearn etkinlikler hakkında genel olarak, bkz: [anlama işlem hatlarının ve etkinliklerin](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>İki bulut veri depoları arasında veri kopyalama
Kaynak ve havuz veri depolarına hello bulutta olduğunda kopyalama etkinliği aşamaları toocopy veri hello kaynak toohello havuz aşağıdaki hello geçer. Kopyalama etkinliği'nın temelini oluşturan hello hizmeti:

1. Veri hello kaynak veri deposundan okur.
2. Serileştirme/seri durumdan çıkarma, sıkıştırma/açma, sütun eşleme gerçekleştirir ve dönüştürme yazın. Merhaba girdi veri kümesi, çıktı veri kümesi ve kopyalama etkinliği hello yapılandırmalarını temel alan bu işlemleri yapar.
3. Veri toohello hedef veri deposuna yazar.

Merhaba hizmet hello en iyi bölge tooperform hello veri taşıma otomatik olarak seçer. Bu bölge genellikle hello bir yakın toohello havuz veri deposudur.

![Bulut Bulut kopyalama](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Bir şirket içi veri depolama ve bir bulut veri deposu arasında veri kopyalama
bir şirket içi veri depolama ve bir bulut veri deposu arasında toosecurely taşıma veri veri yönetimi ağ geçidi, şirket içi makinenizde yükleyin. Veri Yönetimi ağ geçidi karma veri hareketlerini ve işleme sağlayan bir aracıdır. Kendisini hello verileri saklamak gibi aynı makine hello veya erişim toohello verileri sahip ayrı bir makine yükleyebilirsiniz.

Bu senaryoda, veri yönetimi ağ geçidi hello serileştirme/seri durumdan çıkarma, sıkıştırma/açma, sütun eşleme gerçekleştirir ve dönüştürme yazın. Veri hello Azure Data Factory hizmeti geçmez. Bunun yerine, veri yönetimi ağ geçidi doğrudan hello veri toohello hedef depo yazar.

![Şirket içi-için-bulut kopyalama](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Bkz: [şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) bir giriş ve gözden geçirme. Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) bu aracı hakkında ayrıntılı bilgi için.

Verileri de taşıyabilirsiniz / toosupported verilerini depolayan veri yönetimi ağ geçidi kullanarak Azure Iaas sanal makineleri (VM'ler) üzerinde barındırılır. Bu durumda, veri yönetimi ağ geçidi yükleyebileceğiniz kendisini hello verileri saklamak gibi veya erişim toohello verileri sahip ayrı bir VM'de aynı VM hello.

## <a name="supported-data-stores-and-formats"></a>Desteklenen veri depoları ve biçimler
Data Factory kopyalama etkinliği, bir kaynak veri deposu tooa havuz veri deposundan verileri kopyalar. Data Factory veri depolarına aşağıdaki hello destekler. Herhangi bir kaynaktan veri tooany havuz yazılabilir. Bir veri deposu toolearn nasıl tıklatın toocopy veri tooand o depolama alanından.

> [!NOTE] 
> Kopyalama etkinliği desteklemeyen bir veri deposu/toomove verileri gerekiyorsa kullanın bir **özel etkinlik** veri fabrikasında veri kopyalama/taşıma için kendi mantığı ile. Özel bir etkinlik oluşturma ve kullanma hakkında ayrıntılı bilgi için bkz. [Azure Data Factory işlem hattında özel etkinlikler kullanma](data-factory-use-custom-activities.md).

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Veri depolar ile * şirket içi olabilir veya Azure Iaas ve tooinstall gerektiren [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) , şirket içi/Azure Iaas makinede.

### <a name="supported-file-formats"></a>Desteklenen dosya biçimleri
Kopyalama etkinliği kullanabileceğine**olarak dosyaları kopyalama-olan** iki dosya tabanlı veri depoları arasında hello atlayabilirsiniz [Biçim bölümü](data-factory-create-datasets.md) hem hello giriş ve çıkış veri kümesi tanımları. Merhaba veriler herhangi serileştirme/seri durumdan çıkarma verimli bir şekilde kopyalanır.

Kopyalama etkinliği ayrıca okur ve belirtilen biçimlerde toofiles Yazar: **metin, JSON, Avro, ORC ve Parquet**ve sıkıştırma codec **GZIP, Deflate, Bzıp2 ve ZipDeflate** desteklenir. Bkz: [desteklenen dosya ve sıkıştırma biçimleri](data-factory-supported-file-and-compression-formats.md) ayrıntılarla.

Örneğin, bunu hello aşağıdaki etkinlikleri kopyalayın:

* Şirket içi SQL Server veri kopyalama ve tooAzure Data Lake Store ORC biçiminde yazın.
* Dosyaları metin (CSV) biçiminde şirket içi dosya sisteminden kopyalayıp tooAzure Blob Avro biçiminde yazın.
* Şirket içi dosya sisteminden sıkıştırılmış dosyaları kopyalayın ve sıkıştırmasını sonra tooAzure Data Lake Store güden.
* Verileri Azure Blob'tan GZip sıkıştırılmış metin (CSV) biçiminde kopyalayın ve tooAzure SQL veritabanı yazma.

## <a name="global"></a>Genel olarak kullanılabilir veri taşıma
Azure Data Factory yalnızca hello Batı ABD, Doğu ABD ve Kuzey Avrupa bölgelerde kullanılabilir. Ancak, kopyalama etkinliği'nın temelini oluşturan hello hizmeti genel hello kullanılabilir bölgeler ve coğrafi aşağıdaki. Merhaba genel olarak kullanılabilir topoloji genellikle çapraz bölge atlama önler verimli veri taşıma sağlar. Bkz: [bölgeye göre Hizmetleri](https://azure.microsoft.com/regions/#services) Data Factory ve veri taşıma bir bölgede kullanılabilirliği.

### <a name="copy-data-between-cloud-data-stores"></a>Bulut veri depoları arasında veri kopyalama
Kaynak ve havuz veri depolarına hello bulutta olduğunda, veri fabrikası hizmet dağıtımı hello içinde en yakın toohello havuzunun hello bölgede kullanır. aynı Coğrafya toomove hello verileri. Aşağıdaki tablonun eşlemesi için toohello bakın:

| Coğrafya hello hedef veri depoları | Bölge hello hedef veri deposu | Veri taşıma için kullanılan bölge |
|:--- |:--- |:--- |
| Amerika Birleşik Devletleri | Doğu ABD | Doğu ABD |
| &nbsp; | Doğu ABD 2 | Doğu ABD 2 |
| &nbsp; | Orta ABD | Orta ABD |
| &nbsp; | Orta Kuzey ABD | Orta Kuzey ABD |
| &nbsp; | Orta Güney ABD | Orta Güney ABD |
| &nbsp; | Batı Orta ABD | Batı Orta ABD |
| &nbsp; | Batı ABD | Batı ABD |
| &nbsp; | Batı ABD 2 | Batı ABD |
| Kanada | Doğu Kanada | Orta Kanada |
| &nbsp; | Orta Kanada | Orta Kanada |
| Brezilya | Güney Brezilya | Güney Brezilya |
| Avrupa | Kuzey Avrupa | Kuzey Avrupa |
| &nbsp; | Batı Avrupa | Batı Avrupa |
| Birleşik Krallık | Birleşik Krallık Batı | Birleşik Krallık Güney |
| &nbsp; | Birleşik Krallık Güney | Birleşik Krallık Güney |
| Asya Pasifik | Güneydoğu Asya | Güneydoğu Asya |
| &nbsp; | Doğu Asya | Güneydoğu Asya |
| Avustralya | Avustralya Doğu | Avustralya Doğu |
| &nbsp; | Avustralya Güneydoğu | Avustralya Güneydoğu |
| Japonya | Japonya Doğu | Japonya Doğu |
| &nbsp; | Japonya Batı | Japonya Doğu |
| Hindistan | Orta Hindistan | Orta Hindistan |
| &nbsp; | Batı Hindistan | Orta Hindistan |
| &nbsp; | Güney Hindistan | Orta Hindistan |

Alternatif olarak, açıkça Data Factory hizmeti toobe hello bölgesini belirterek tooperform hello kopyalama kullanılan belirtebilirsiniz `executionLocation` kopyalama etkinliği'nin altındaki özelliğini `typeProperties`. Bu özellik için desteklenen değerler listelenmiştir yukarıda **bölge veri taşıma için kullanılan** sütun. Verilerinizi bu bölge hello kablo üzerinden kopyalama sırasında gider unutmayın. Örneğin, Azure arasında toocopy belirtebilirsiniz Kore içinde depolar `"executionLocation": "Japan East"` tooroute Japonya bölge aracılığıyla (bkz [JSON örnek](#by-using-json-scripts) başvuru olarak).

> [!NOTE]
> Merhaba bölge hello hedef veri deposunun önceki listede değil veya belirlenemeyen, varsayılan olarak kopyalama etkinliği alternatif bir bölge giderek yerine sürece başarısız olursa `executionLocation` belirtilir. desteklenen hello bölge listesi zamanla genişletilir.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Bir şirket içi veri depolama ve bir bulut veri deposu arasında veri kopyalama
Ne zaman veri kopyalanır şirket içi (ya da Azure sanal makineleri/Iaas) arasında ve bulut depoları, [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) bir şirket içi makineye veya sanal makineye veri taşımayı gerçekleştirir. Merhaba veri akan hello bulutta hello hizmeti aracılığıyla hello kullanmadığınız sürece [kopyalama hazırlanan](data-factory-copy-activity-performance.md#staged-copy) yeteneği. Bu durumda, veriler Azure Blob Depolama hello havuz veri deposuna yazılmadan önce hazırlama hello aracılığıyla akar.

## <a name="create-a-pipeline-with-copy-activity"></a>Kopyalama etkinliği ile işlem hattı oluşturma
Çeşitli şekillerde kopyalama etkinliği ile işlem hattı oluşturabilirsiniz:

### <a name="by-using-hello-copy-wizard"></a>Merhaba Kopyalama Sihirbazı'nı kullanarak
Merhaba Data Factory Kopyalama Sihirbazı, toocreate kopyalama etkinliği ile işlem hattı yardımcı olur. Bu ardışık düzen desteklenen kaynakları toodestinations toocopy verileri sağlayan *JSON yazma olmadan* bağlı hizmetler, veri kümeleri ve işlem hatları için tanımlar. Bkz: [Data Factory Kopyalama Sihirbazı](data-factory-copy-wizard.md) hello Sihirbazı hakkında ayrıntılı bilgi için.  

### <a name="by-using-json-scripts"></a>JSON komut dosyalarını kullanarak
Data Factory Düzenleyici'hello Azure portal, Visual Studio veya Azure PowerShell toocreate JSON tanımını ardışık düzeni için (bir kopyalama etkinliği'ı kullanarak) kullanabilirsiniz. Ardından, veri fabrikası'nda toocreate hello ardışık olarak dağıtabilirsiniz. Bkz [Öğreticisi: Azure Data Factory işlem hattı kullanım kopyalama etkinliği](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) bir öğretici hakkında adım adım yönergeler için.    

JSON özellikleri (örneğin, ad, açıklama, giriş ve çıkış tabloları ve ilkeleri) etkinlikleri tüm türleri için kullanılabilir. Hello kullanılabilir özellikler `typeProperties` hello etkinlik bölümünü her etkinlik türü ile değişir.

Kopya etkinliği için hello `typeProperties` bölüm kaynakları hello türlerine bağlı olarak değişir ve şu havuzlar. Bir kaynak/havuz hello tıklatın [desteklenen kaynakları ve havuzlarını](#supported-data-stores-and-formats) bölüm toolearn kopyalama etkinliği için bu veri deposu destekleyen türü özellikleri hakkında.

Bir örnek JSON tanımı aşağıda verilmiştir:

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
hello tanımlanan hello zamanlama çıkış veri kümesi belirler hello etkinlik çalıştığında (örneğin: **günlük**, sıklığı olarak **gün**ve aralığı olarak **1**). Merhaba etkinlik verileri bir giriş veri kümesinden kopyalar (**kaynak**) tooan çıkış veri kümesi (**havuz**).

Birden fazla girdi veri kümesi tooCopy etkinlik belirtebilirsiniz. Merhaba etkinlik çalıştırılmadan önce kullanılan tooverify hello bağımlılıkları oldukları. Ancak, yalnızca hello hello ilk veri kümesini kopyalanan toohello hedef veri kümesi verilerdir. Daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Performans ve ayar
Merhaba bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md), Azure Data factory'de veri taşımayı (kopyalama etkinliği) hello performansını etkileyen önemli faktör açıklar. Ayrıca iç testi sırasında performans gözlenecek hello listeler ve çeşitli yolları toooptimize hello performansını kopyalama etkinliği açıklanır.

## <a name="fault-tolerance"></a>Hataya dayanıklılık
Varsayılan olarak, veri ve return hatası kopyalama kopyalama etkinliği durdurulacak zaman uyumsuz veri kaynağı ve havuz; arasında karşılaşırsanız açıkça tooskip ve günlük hello uyumsuz satırları ve yalnızca kopya yapılandırabilirsiniz ancak bu uyumlu veri toomake hello kopyalama başarılı oldu. Merhaba bkz [kopyalama etkinliği hataya dayanıklılık](data-factory-copy-activity-fault-tolerance.md) üzerinde daha ayrıntılı bilgi.

## <a name="security-considerations"></a>Güvenlikle ilgili dikkat edilmesi gerekenler
Merhaba bkz [güvenlik konuları](data-factory-data-movement-security-considerations.md), Azure Data Factory veri taşıma hizmetleri verilerinizi toosecure kullanan güvenlik altyapısı açıklar.

## <a name="scheduling-and-sequential-copy"></a>Zamanlama ve sıralı kopyalama
Bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) zamanlama ve yürütme şeklini Data Factory hakkında ayrıntılı bilgi. Bu olası toorun birden çok kopyalama işlemleri birbiri ardından sıralı/sıralı bir biçimde değil. Merhaba bkz [sırayla kopyalamak](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) bölümü.

## <a name="type-conversions"></a>Tür dönüştürmeleri
Farklı veri depolarına farklı yerel tür sistemleri sahiptir. Kopyalama etkinliği ile iki aşamalı bir yaklaşım aşağıdaki hello kaynak türleri toosink türlerinden otomatik tür dönüşümleri gerçekleştirir:

1. Yerel kaynak türleri tooa .NET türünden dönüştürün.
2. .NET türü tooa yerel Havuz türü dönüştürün.

bir veri deposu için bir yerel tür sistem tooa .NET türü Hello eşlemesinden hello ilgili veri deposu makalesinde bulabilirsiniz. (Merhaba içinde hello belirli bağlantısını tıklatın [desteklenen veri depoları](#supported-data-stores) tablo). Böylece kopyalama etkinliği hello sağ dönüşümleri gerçekleştirir, tablolarınızı oluşturulurken bu eşlemeleri toodetermine uygun türleri kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* toolearn hello daha kopyalama etkinliği hakkında bkz [Azure Blob Depolama tooAzure SQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* bir şirket içi veri deposu tooa bulut veri deposundan veri taşıma hakkında toolearn bkz [şirket içi toocloud veri depolarına veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).
