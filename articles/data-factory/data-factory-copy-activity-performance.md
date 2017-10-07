---
title: "aaaCopy etkinlik performans ve ayarlama Kılavuzu | Microsoft Docs"
description: "Kopyalama etkinliği kullandığınızda, Azure Data factory'de veri taşımayı hello performansını etkileyen anahtar Etkenler hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Etkinlik performans ve ayarlama Kılavuzu kopyalayın
Azure Data Factory kopyalama etkinliği çözümü bir birinci sınıf güvenli, güvenilir ve yüksek performanslı veri yükleme sunar. Bu bulut zengin çeşitli her gün toocopy onlarca veri terabayt sağlar ve şirket içi veri depolarına. Üstün hızlı veri performans yükleme olan anahtar tooensure odaklanmak hello çekirdek "büyük veri" sorunu: Gelişmiş analiz çözümleri oluşturmak ve tüm bu verilerden ayrıntılı Öngörüler alma.

Azure veri depolama ve veri ambarı çözümleri Kurumsal düzeyde bir dizi sağlar ve yüksek oranda iyileştirilmiş bir veri kolay tooconfigure ve ayarlama deneyimi yükleme kopyalama etkinliği sunar. Yalnızca tek kopyalama etkinliği ile elde edebilirsiniz:

* Verileri yükleme **Azure SQL Data Warehouse** adresindeki **1,2 GB/sn**. Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).
* Verileri yükleme **Azure Blob Depolama** adresindeki **1.0 GB/sn**
* Verileri yükleme **Azure Data Lake Store** adresindeki **1.0 GB/sn**

Bu makalede açıklanır:

* [Performans referans numaraları](#performance-reference) ; Proje planınızı desteklenen kaynak ve havuz veri depoları toohelp için
* Artırabilir özellikleri hello kopyalama işleme dahil olmak üzere farklı senaryolarda [bulut veri taşıma birimleri](#cloud-data-movement-units), [paralel kopyalama](#parallel-copy), ve [kopyalama hazırlanan](#staged-copy);
* [Performans ayarlama yönergeleri](#performance-tuning-steps) üzerinde nasıl etkileyebileceğini tootune hello performans ve hello anahtar Etkenler performans kopyalayın.

> [!NOTE]
> Genel kopyalama etkinliği ile bilmiyorsanız, bkz: [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md) bu makaleyi okumadan önce.
>

## <a name="performance-reference"></a>Performans başvurusu

Bir başvuru olarak aşağıdaki tabloyu şirket içi testlere göre kaynak ve havuz çiftleri verilen hello için MB/sn olarak hello kopyalama verimlilik numarasını gösterir. Karşılaştırma için ayrıca farklı ayarlarını gösterir [bulut veri taşıma birimleri](#cloud-data-movement-units) veya [veri yönetimi ağ geçidi ölçeklenebilirlik](data-factory-data-management-gateway-high-availability-scalability.md) (birden çok ağ geçidi düğümler) kopyalama performansına yardımcı olabilir.

![Performans Matrisi](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Noktaları toonote:**
* Üretilen iş formülü aşağıdaki hello kullanılarak hesaplanır: [verilerin boyutu okuma kaynağından] / [kopyalama çalışma süresini etkinliği].
* Merhaba tablosundaki Hello performans başvuru numaraları ölçülen kullanarak [TPC-H](http://www.tpc.org/tpch/) veri kümesi bir tek kopyalama etkinliğinde çalıştırın.
* Azure veri depolarında hello kaynak ve havuz hello olan aynı Azure bölgesi.
* Karma kopyalama şirket içi ve bulut arasında veri depolarına, her ağ geçidi düğümü Itanium tabanlı sistemler için hello şirket içi veri deposu ile belirtimi altındaki ayrı bir makinede çalışıyordu. Tek bir etkinliğin ağ geçidinde çalıştırırken hello kopyalama işlemi yalnızca küçük bir bölümü hello test makinenin CPU, bellek veya ağ bant genişliği tüketilen. ' Dan daha fazla bilgi edinin [göz önünde bulundurarak veri yönetimi ağ geçidi için](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>CPU</td>
        <td>32 2.20 GHz Intel Xeon E5-2660 v2 çekirdek</td>
    </tr>
    <tr>
        <td>Bellek</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>Ağ</td>
        <td>Internet arabirimi: 10 GB/sn; intranet arabiriminde: 40 GB/sn</td>
    </tr>
    </table>


> [!TIP]
> Daha fazla veri taşıma birimden (DMUs) hello yararlanarak daha yüksek verimlilik elde edebileceğiniz maksimum DMUs Bulut Bulut kopyalama etkinliği çalıştırmak için 32 olan varsayılan. Örneğin, 100 DMUs ile Azure Blob kopyalama verileri Azure Data Lake Store içine elde edebilirsiniz **1.0GBps**. Merhaba bkz [bulut veri taşıma birimleri](#cloud-data-movement-units) bölüm bu özellik ve hello hakkında ayrıntılı bilgi için desteklenen senaryo. Kişi [Azure Destek](https://azure.microsoft.com/support/) toorequest daha fazla DMUs.

## <a name="parallel-copy"></a>Paralel kopyalama
Merhaba veri kaynağı veya veri toohello hedef yazma okuyabilirsiniz **çalıştırmak kopyalama etkinliği içinde paralel**. Bu özellik, bir kopyalama işlemi hello verimliliğini artırır ve hello süresini toomove veri azaltır.

Bu ayar hello farklı **eşzamanlılık** hello etkinlik tanımında özelliği. Merhaba **eşzamanlılık** özelliği hello sayısını belirler **eşzamanlı kopyalama etkinliği çalışır** farklı etkinlik windows tooprocess verileri (1 AM too2 'M 2 AM too3 'M, 3 AM too4 'M, vb.). Bu özellik, geçmiş bir yükleme gerçekleştirmek yararlıdır. Merhaba paralel kopyasını yetenek geçerlidir tooa **tek Etkinlik**.

Bir örnek senaryo bakalım. Aşağıdaki örneğine hello işlenen toobe hello geçmiş gelen birden çok dilim gerekir. Data Factory kopyalama etkinliği (etkinlik Çalıştır) bir örneği her dilim için çalışır:

* Merhaba veri dilimi hello ilk etkinliği penceresinden (1 AM too2 'M) == > etkinliği çalıştırmak 1
* Merhaba veri dilimi hello ikinci etkinliği penceresinden (2 AM too3 'M) == > etkinliği çalıştırmak 2
* Merhaba veri dilimi hello ikinci etkinliği penceresinden (3 AM too4 'M) == > etkinliği çalıştırmak 3

Etki alanları bu hiyerarşi sıralamasıyla devam eder.

Bu örnekte, hello zaman **eşzamanlılık** değeri too2, ayarı **etkinliği çalıştırmak 1** ve **etkinliği çalıştırmak 2** iki etkinlik Windows'dan veri kopyalama **eşzamanlı olarak**  tooimprove veri taşıma performans. Birden çok dosya 1 Çalıştır etkinliği ile ilişkiliyse, ancak hello veri taşıma hizmeti dosyaları hello kaynak toohello hedef bir dosyadan birer birer kopyalar.

### <a name="cloud-data-movement-units"></a>Bulut veri taşıma birimleri
A **bulut veri taşıma birimi (DMU)** veri fabrikası'nda tek bir birimi (CPU, bellek ve ağ kaynağı ayırma birleşimi) gücünü hello temsil eden bir ölçüdür. Bir DMU Bulut Bulut kopyalama işlemi, ancak bir karma kopyalama kullanılıyor olabilir.

Varsayılan olarak, veri fabrikası tek bulut DMU tooperform çalıştıran tek bir kopyalama etkinliği kullanır. toooverride bu varsayılan hello için bir değer belirtin **cloudDataMovementUnits** şekilde özelliği. Merhaba, belirli kopya kaynak ve havuz için daha fazla birimi yapılandırırken alabilirsiniz performans kazancı hello düzeyi hakkında bilgi için bkz [Performans başvurusu](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Merhaba **izin verilen değerler** hello için **cloudDataMovementUnits** özelliği olan 1 (varsayılan), 2, 4, 8, 16 ve 32. Merhaba **bulut DMUs gerçek sayısını** hello kopyalama işlemini çalışma zamanında veri deseni bağlı olarak yapılandırılmış hello değeri'den küçük eşit tooor kullanmasıdır.

> [!NOTE]
> Daha fazla bulut DMUs için daha yüksek işleme gerekiyorsa başvurun [Azure Destek](https://azure.microsoft.com/support/). 8 ayarlama ve yukarıdaki şu anda yalnızca çalışır, **Blob Depolama/Data Lake Store/Amazon S3/bulut FTP/bulut SFTP tooBlob depolama/Data Lake Store/Azure'dan birden çok dosya kopyalama SQL veritabanı**.
>

### <a name="parallelcopies"></a>parallelCopies
Merhaba kullanabilirsiniz **parallelCopies** özelliği tooindicate hello paralellik kopyalama etkinliği toouse istiyor. Bu özelliğin hello en fazla kaynağınızdan okumak veya tooyour havuz veri depolarına paralel olarak yazma kopyalama etkinliği içinde iş parçacığı sayısı olarak düşünebilirsiniz.

Her kopya Çalıştır etkinliği için veri fabrikası paralel hello sayısı toouse toocopy veri hello kaynak veri deposu ve toohello hedef veri deposuna kopyalar belirler. Merhaba varsayılan kullandığı paralel kopya sayısını kaynak ve kullandığınız havuz hello türüne bağlıdır.  

| Kaynak ve havuz | Hizmeti tarafından belirlenen varsayılan paralel kopya sayısı |
| --- | --- |
| Dosya tabanlı depolar (Blob storage; arasında veri kopyalama Data Lake Store; Amazon S3; bir şirket içi dosya sistemi; bir şirket içi HDFS) |1 ile 32 arasında. İki bulut veri depoları arasında kullanılan toocopy veri hello dosyaları ve bulut veri taşıma birimleri (DMUs) hello sayıda Hello boyutuna bağlıdır veya hello fiziksel yapılandırmasını hello karma kopyalama (toocopy veri tooor bir şirket içi veri deposu için kullanılan ağ geçidi makinesi ). |
| Veri kopyalamak **tüm kaynak veri deposu tooAzure tablo depolama** |4 |
| Diğer tüm kaynak ve havuz çiftleri |1 |

Genellikle, hello varsayılan davranışı vermelidir hello en iyi verimlilik. Ancak, toocontrol hello veri depolarını veya tootune kopyalama performans bu makinelerde barındıran yükleme, toooverride hello varsayılan değer seçin ve hello için bir değer belirtin **parallelCopies** özelliği. Başlangıç değeri 1 ile 32 (her ikisi de dahil) arasında olmalıdır. Çalışma zamanında hello en iyi performans için kopyalama etkinliği küçük veya ona eşit bir değer kullanır ayarladığınız toohello değeri.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Noktaları toonote:

* Dosya tabanlı depoları arasında veri kopyaladığınızda, hello **parallelCopies** hello paralellik hello dosya düzeyinde belirleyin. tek bir dosyada Hello Öbekleme durum altında otomatik ve şeffaf şekilde ve tasarlanmıştır toouse hello belirtilen kaynak veri deposu için en iyi uygun öbek boyutu paralel ve resme tooparallelCopies tooload veri yazın. Merhaba gerçek hello veri taşıma hizmeti zamanında hello kopyalama işlemi için kullanımdır hello sahip dosyaları sayısından fazla paralel kopya sayısı. Merhaba kopyalama davranışını ise **mergeFile**, kopyalama etkinliği, dosya düzeyinde paralellik avantajlarından alamaz.
* Hello için değer belirttiğinizde **parallelCopies** özelliği, bir karma kopyalama ise, kaynak ve havuz veri depoları ve toogateway hello yük artışı göz önünde bulundurun. Bu özellikle birden çok etkinlikleri veya hello eşzamanlı çalıştırılan olduğunda gerçekleşir karşı çalıştırmak aynı etkinlikleri hello aynı veri deposu. Merhaba veri deposunda veya ağ geçidi hello yük ile doludur fark ederseniz hello azaltmak **parallelCopies** değeri toorelieve hello yük.
* Dosya tabanlı dosya tabanlı toostores olmayan depoları verileri kopyaladığınızda, hello veri taşıma hizmeti hello yoksayar **parallelCopies** özelliği. Paralellik belirtilmiş olsa bile, bu durumda uygulanmıyor.

> [!NOTE]
> Veri Yönetimi ağ geçidi sürümü 1.11 veya üzeri toouse hello kullanmalısınız **parallelCopies** karma kopyalama yaptığınızda özelliği.
>
>

toobetter bu iki özellik ve tooenhance veri taşıma verimlilik, hello bkz [örnek kullanım durumları](#case-study-use-parallel-copy). Tooconfigure gerekmeyen **parallelCopies** hello varsayılan davranışı tootake yararlanabilir. Yapılandırırsanız ve **parallelCopies** birden çok bulut DMUs değil tam olarak kullanılan çok küçük.  

### <a name="billing-impact"></a>Faturalama etkisi
Bunun **önemli** sizden ücret tooremember dayalı hello toplam hello kopyalama işlemi zamanında. Kopyalama işini tootake bir saat bir bulut birimle kullanılan ve şimdi dört bulut birimleri ile 15 dakika sürer, hello genel fatura kalır neredeyse aynı hello. Örneğin, dört bulut birimleri kullanın. Hello ilk bulut birimi 10 dakika harcadığı, hello İkincisi, 10 dakika, 5 dakika, üçüncü bir hello ve dördüncü bir, tüm bir kopyalama etkinliğinde çalıştırın 5 dakika hello. 10 + 10 + 5 + 5 = 30 dakika olan hello toplam copy (veri taşıma) süre için sizden ücret kesilir. Kullanarak **parallelCopies** faturalama etkilemez.

## <a name="staged-copy"></a>Hazırlanan kopyalama
Bir kaynak veri deposu tooa havuz veri deposundan verileri kopyaladığınızda, geçici bir hazırlama deposu olarak toouse Blob Depolama seçebilirsiniz. Hazırlama durumlarda aşağıdaki hello özellikle yararlı olur:

1. **PolyBase aracılığıyla SQL veri ambarında tooingest verileri çeşitli veri depolamaları istediğiniz**. SQL Data Warehouse, SQL veri ambarında yüksek verimlilik mekanizması tooload büyük miktarda veri olarak PolyBase kullanır. Ancak, hello kaynak verileri Blob storage'da olmalıdır ve ek ölçütleri karşılaması gerekir. Dışında bir Blob Depolama veri deposundan veri yüklediğinizde, verileri aracılığıyla geçici hazırlama Blob depolamaya kopyalama etkinleştirebilirsiniz. Bu durumda, veri fabrikası PolyBase hello gereksinimlerini karşılayan gerekli hello veri dönüşümleri tooensure gerçekleştirir. Daha sonra PolyBase tooload verileri SQL Data Warehouse'a kullanır. Daha fazla ayrıntı için bkz: [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).
2. **Bazen biraz uzun sürebilir tooperform bir yavaş ağ bağlantısı üzerinden karma veri taşıma (diğer bir deyişle, bir şirket içi veri depolama ve bulut veri deposu arasındaki toocopy)**. tooimprove performans verileri hello bulutta toomove veri toohello hazırlama veri depolamak daha az zaman alır, böylece şirket içi hello sıkıştırabilirsiniz. Ardından hello hedef veri deposuna yükleme önce deposu hazırlama hello hello verilerde açabilmeleri.
3. **Tooopen bağlantı noktaları dışındaki bağlantı noktası 80 ve kurumsal BT ilkeleri nedeniyle, Güvenlik Duvarı'nda 443 numaralı bağlantı istemediğiniz**. Bir şirket içi veri deposu tooan Azure SQL veritabanı havuzunu veya bir Azure SQL veri ambarı havuzu verilerin kopyaladığınızda, örneğin, tooactivate giden TCP iletişim bağlantı noktası 1433 hello Windows Güvenlik Duvarı ve kurumsal güvenlik ağınızın için gerekir. Bu senaryoda, hello ağ geçidi toofirst kopya veri tooa Blob Depolama hazırlama örneği HTTP veya HTTPS üzerinden bağlantı noktası 443 üzerinde yararlanın. Ardından, hello veri SQL Database veya SQL Data Warehouse Blob Depolama hazırlamadan yükleyin. Bu akışta tooenable bağlantı noktası 1433 gerekmez.

### <a name="how-staged-copy-works"></a>Nasıl hazırlanmış kopyalama çalışır
Özellik hazırlama hello etkinleştirdiğinizde, hello kaynak veri deposu toohello veri deposu hazırlama kopyalanan ilk hello verileri (Getir kendi). Ardından, hello veriler veri deposu toohello havuz veri deposu hazırlama hello kopyalanır. Veri Fabrikası hello iki aşamalı akış sizin için otomatik olarak yönetir. Veri Fabrikası aynı zamanda hello veri taşıma işlemi tamamlandıktan sonra depolama hazırlama hello geçici verileri temizler.

Merhaba bulut kopyalama senaryosunda (Merhaba bulutta depoları olan kaynak ve havuz veriler), ağ geçidi kullanılmaz. Merhaba Data Factory hizmetinin hello kopyalama işlemleri gerçekleştirir.

![Kopya hazırlanan: Bulut senaryosu](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

Merhaba karma kopyalama senaryoda (şirket içi bir kaynaktır ve havuz olduğu hello buluta), hello ağ geçidi taşır hello kaynak verilerinden verileri depolamak tooa veri deposu hazırlama. Veri hazırlama hello verilerden toohello havuz veri deposunu veri fabrikası hizmetine taşır. Bir bulut veri deposu tooan veri kopyalama hazırlama yoluyla veri deposu ayrıca ters hello akış ile desteklenen şirket içi.

![Kopya hazırlanan: karma senaryo](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Hazırlama depolama kullanarak veri taşıma etkinleştirdiğinizde, veri tooan geçici veya veri deposu hazırlama depolamak ve bir geçiş verileri taşımadan önce sıkıştırması hello kaynaktan veri taşımadan önce sıkıştırılmış hello veri toobe isteyip istemediğinizi belirtebilirsiniz veya Hazırlama veri deposu toohello havuz veri deposu.

Şu anda, bir hazırlama deposu kullanarak iki şirket içi veri depoları arasında veri kopyalanamıyor. Bu seçenek toobe kullanılabilir yakında bekliyoruz.

### <a name="configuration"></a>Yapılandırma
Merhaba yapılandırma **enableStaging** bir hedef veri deposuna yükleme önce Blob depolama alanına aşamalı hello veri toobe istediğinizi kopyalama etkinliği toospecify ayarlama. Ayarladığınızda **enableStaging** tooTRUE, hello sonraki tabloda listelenen hello ek özellikleri belirtin. Yoksa, ayrıca toocreate bir Azure depolama gerekir veya depolama paylaşılan erişim imzası bağlantılı hizmeti için hazırlama.

| Özellik | Açıklama | Varsayılan değer | Gerekli |
| --- | --- | --- | --- |
| **enableStaging** |Toocopy veri deposu hazırlama bir geçiş aracılığıyla isteyip istemediğinizi belirtin. |False |Hayır |
| **linkedServiceName** |Merhaba adını belirtin bir [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) bağlı bir geçici hazırlama deposu olarak kullanmak depolama toohello örneğini başvuruyor hizmeti. <br/><br/> PolyBase aracılığıyla SQL veri ambarında ile paylaşılan erişim imzası tooload veri depolama alanı kullanamazsınız. Diğer tüm senaryolarda kullanabilirsiniz. |Yok |Evet, ne zaman **enableStaging** tooTRUE ayarlayın |
| **yol** |Toocontain hazırlanan hello verilerin istediğiniz hello Blob Depolama alanı yolu belirtin. Bir yol belirtmezseniz, hello hizmet kapsayıcı toostore geçici verileri oluşturur. <br/><br/> Yalnızca depolama ile paylaşılan erişim imzası kullanın veya belirli bir konumda geçici verileri toobe gerektiren bir yol belirtin. |Yok |Hayır |
| **Aracılığıyla** |Kopyalanan toohello hedef önce verilerin sıkıştırılmasının gerekli olup olmadığını belirtir. Bu ayar hello aktarılan veri hacmini azaltır. |False |Hayır |

Kopyalama etkinliği tablo önceki hello açıklanan hello özelliklere sahip bir örnek tanımı aşağıda verilmiştir:

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Faturalama etkisi
Temel alınarak iki adımı ücretlendirilen: süresi kopyalama ve kopyalama türü.

* (Bir bulut veri deposu tooanother bulut veri deposundan veri kopyalama) bulut kopyalama sırasında Hazırlama [bulut kopya Birim Fiyat] x [adım 1 ve 2. adım için kopyalama süresi toplamı] hello kullandığınızda ücretlendirilirsiniz.
* Kullandığınızda (bir şirket içi veri deposu tooa bulut veri deposundan veri kopyalama) karma kopyalama sırasında hazırlama, [karma kopyalama süresince] ücretlendirilen x [karma kopya Birim Fiyat] + [bulut kopyalama süre] [bulut kopya Birim Fiyat] x.

## <a name="performance-tuning-steps"></a>Performans ayarlama adımları
Veri Fabrikası hizmetinizin kopyalama etkinliği ile tootune hello performans şu adımları uygulamanız öneririz:

1. **Bir taban çizgisi oluşturma**. Merhaba geliştirme aşamasında, temsili veri örneği karşı kopyalama etkinliği kullanarak hattınızı sınayın. Merhaba Data Factory kullanabilirsiniz [modeli dilimleme](data-factory-scheduling-and-execution.md) toolimit hello miktarda veri ile çalışırsınız.

   Yürütme süresi ve performans özellikleri hello kullanarak toplamak **izleme ve yönetim uygulaması**. Seçin **İzleyici & Yönet** Data Factory giriş sayfası. Merhaba ağaç görünümünde hello seçin **çıkış dataset**. Merhaba, **etkinlik Windows** listesinde, hello kopyalama Çalıştır etkinliği seçin. **Etkinlik pencerelerine** hello kopyalama etkinlik süresi ve hello kopyalanır hello verilerin boyutunu listeler. Merhaba verimlilik listelenir **etkinlik penceresini Explorer**. toolearn hello uygulama hakkında daha fazla bilgi görmek [izleme ve yönetme kullanarak Azure Data Factory işlem hatlarını izleme ve yönetim uygulaması hello](data-factory-monitor-manage-app.md).

   ![Etkinlik çalışma ayrıntıları](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Merhaba makalenin sonraki bölümlerinde, hello performans ve, senaryo tooCopy etkinlik 's yapılandırmasını karşılaştırabilirsiniz [Performans başvurusu](#performance-reference) bizim testlerden.
2. **Tanılama ve performansı en iyi duruma**. Merhaba performans, gözlemlemek beklentilerinizi karşılamıyorsa tooidentify performans sorunları gerekir. Ardından, performans tooremove en iyi duruma getirme veya performans sorunlarını hello etkisini azaltmak. Performans Tanılama tam açıklamasını, bu makalenin kapsamı dışındadır hello olmakla birlikte bazı genel konular şunlardır:

   * Performans özellikleri:
     * [Paralel kopyalama](#parallel-copy)
     * [Bulut veri taşıma birimleri](#cloud-data-movement-units)
     * [Hazırlanan kopyalama](#staged-copy)
     * [Veri Yönetimi ağ geçidi ölçeklenebilirlik](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Veri Yönetimi Ağ Geçidi](#considerations-for-data-management-gateway)
   * [Kaynak](#considerations-for-the-source)
   * [Havuz](#considerations-for-the-sink)
   * [Seri hale getirme ve seri durumdan çıkarma](#considerations-for-serialization-and-deserialization)
   * [Sıkıştırma](#considerations-for-compression)
   * [Sütun eşlemesi](#considerations-for-column-mapping)
   * [Diğer konular](#other-considerations)
3. **Merhaba yapılandırma tooyour tüm veri kümesinin genişletin**. Hello yürütme sonuçları ve performans ile memnun kaldığınızda, hello tanımı'nı genişletin ve tüm veri kümenizi etkin dönem toocover kanalı.

## <a name="considerations-for-data-management-gateway"></a>Veri Yönetimi ağ geçidi için ilgili önemli noktalar
**Ağ geçidi Kurulum**: ayrılmış makine toohost veri yönetimi ağ geçidi kullanmanızı öneririz. Bkz: [veri yönetimi ağ geçidi kullanarak dikkat edilmesi gereken noktalar](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Ağ geçidi izleme ve yukarı/genişleme**: tek bir mantıksal ağ geçidi bir veya daha fazla ağ geçidi düğümleri ile birden çok kopya etkinliği kullanılabileceği hello'de çalışır aynı zaman eşzamanlı olarak. Bir ağ geçidi makinesi hello hello Azure portal sınırı karşı çalışan eşzamanlı iş sayısını görmek olarak iyi kaynak kullanımı (CPU, bellek, network(in/out), vb.) neredeyse gerçek zamanlı görüntüsünü görüntüleyebilirsiniz [hello portalındaİzleyiciağgeçidi](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Karma veri taşıma çok sayıda eş zamanlı kopyalama etkinliği çalışır veya büyük miktarda veri toocopy üzerinde ağır gereksiniminiz varsa çok göz önünde bulundurun[ölçeği veya ağ geçidi ölçeklendirmek](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) toobetter olarak bu nedenle, kaynak kullanan veya Daha fazla kaynak tooempower tooprovision kopyalayın. 

## <a name="considerations-for-hello-source"></a>Merhaba kaynak için ilgili önemli noktalar
### <a name="general"></a>Genel
Veri deposu temel bu hello veya onu karşı çalışan diğer iş yükleri tarafından doludur değil emin olun.

Microsoft veri depoları için bkz: [izleme ve konuları ayarlama](#performance-reference) olan belirli toodata depoları ve veri performans özellikleri depolamak, yanıt sürelerini en aza indirmek ve üretilen işi en üst düzeye anlamanıza yardım.

Blob Depolama tooSQL veri ambarı ' verileri kopyalarsanız kullanmayı **PolyBase** tooboost performans. Bkz: [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) Ayrıntılar için. Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Dosya tabanlı veri depoları
*(Blob Depolama, Data Lake Store, Amazon S3, şirket içi dosya sistemleri ve şirket içi HDFS içerir)*

* **Ortalama dosya boyutu ve dosya sayısı**: kopyalama etkinliği, aynı anda bir veri dosyası aktarır. Aynı miktarda veri toobe taşınmış hello ile Merhaba genel üretilen işi hello veri toohello önyükleme aşaması her bir dosyanın son birkaç büyük dosyalar yerine pek çok küçük dosya oluşuyorsa düşüktür. Bu nedenle, mümkünse, küçük dosyalar daha büyük dosyaları toogain daha yüksek verimlilik birleştirin.
* **Dosya biçimi ve sıkıştırma**: hello daha fazla yol tooimprove performans için bkz: [seri hale getirme ve seri durumundan çıkarma için ilgili önemli noktalar](#considerations-for-serialization-and-deserialization) ve [sıkıştırma için ilgili önemli noktalar](#considerations-for-compression) bölümler.
* Hello için **şirket içi dosya sistemi** senaryosunda, hangi **veri yönetimi ağ geçidi** olan gerekli hello bkz [veri yönetimi ağ geçidi için ilgili önemli noktalar](#considerations-for-data-management-gateway) bölümü.

### <a name="relational-data-stores"></a>İlişkisel veri depoları
*(SQL veritabanı içerir; SQL veri ambarı; Amazon Redshift; SQL Server veritabanları; ve Oracle, MySQL, DB2, Teradata, Sybase ve PostgreSQL veritabanları, vs.)*

* **Veri deseni**: Tablo şemanızı kopyalama verimlilik etkiler. Büyük satır boyutu küçük satır boyutu daha iyi performans sağlar, toocopy hello aynı miktarda veri. Merhaba hello veritabanının daha verimli bir şekilde daha az sayıda satır içeren veri daha az toplu alabilir nedenidir.
* **Sorgu veya saklı yordam**: hello sorgu veya saklı yordam belirttiğiniz hello kopyalama etkinliği kaynak toofetch verileri daha verimli bir şekilde hello mantığını en iyi duruma getirme.
* İçin **içi ilişkisel veritabanları**, SQL Server ve hello kullanılmasını Oracle gibi **veri yönetimi ağ geçidi**, hello bkz [veri yönetimi ağ geçididikkatealınacaknoktalar](#considerations-on-data-management-gateway) bölümü.

## <a name="considerations-for-hello-sink"></a>Merhaba havuz için ilgili önemli noktalar
### <a name="general"></a>Genel
Veri deposu temel bu hello veya onu karşı çalışan diğer iş yükleri tarafından doludur değil emin olun.

Microsoft veri depoları için çok başvuran[izleme ve konuları ayarlama](#performance-reference) belirli toodata depoları olan. Bu konular, veri deposu performans özellikleri ve nasıl toominimize yanıt sürelerinde anlamanıza ve üretilen işi en üst düzeye çıkarmanıza yardımcı olabilir.

Verileri kopyalıyorsanız **Blob storage** çok**SQL Data Warehouse**, kullanmayı **PolyBase** tooboost performans. Bkz: [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) Ayrıntılar için. Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Dosya tabanlı veri depoları
*(Blob Depolama, Data Lake Store, Amazon S3, şirket içi dosya sistemleri ve şirket içi HDFS içerir)*

* **Kopyalama davranışı**: farklı dosya tabanlı veri deposundan verileri kopyalarsanız, kopyalama etkinliği hello aracılığıyla üç seçenek vardır **copyBehavior** özelliği. Hiyerarşi korur, hiyerarşi düzleştirir veya dosyaları birleştirir. Koruma veya hiyerarşi düzleştirme çok az kayıpla veya hiç performans yüküne sahiptir, ancak dosyaları birleştirme performans genel gider tooincrease neden olur.
* **Dosya biçimi ve sıkıştırma**: bkz: Merhaba [seri hale getirme ve seri durumundan çıkarma için ilgili önemli noktalar](#considerations-for-serialization-and-deserialization) ve [sıkıştırma için ilgili önemli noktalar](#considerations-for-compression) bölümlerde daha fazla yol tooimprove performansı .
* **BLOB Depolama**: şu anda, Blob Depolama destekler yalnızca en iyi duruma getirilmiş veri aktarımı ve verimlilik için blok.
* İçin **şirket içi dosya sistemleri** hello kullanımını gerektiren senaryolar **veri yönetimi ağ geçidi**, hello bkz [veri yönetimi ağ geçidi için ilgili önemli noktalar](#considerations-for-data-management-gateway) bölümü.

### <a name="relational-data-stores"></a>İlişkisel veri depoları
*(SQL veritabanı, SQL Data Warehouse, SQL Server veritabanları ve Oracle veritabanları içerir)*

* **Davranış kopyalama**: hello özellikleri için ayarlanmış bağlı olarak **sqlSink**, kopyalama etkinliği farklı yollarla verileri toohello hedef veritabanına yazar.
  * Varsayılan olarak, en iyi performansı hello veri taşıma hizmeti kullanan hello toplu kopyalama API tooinsert verilerde ekleme sağlar modu hello.
  * Saklı yordam hello havuzunda yapılandırırsanız, hello veritabanı hello veri bir satır yerine bir anda bir toplu yükleme olarak uygulanır. Performansı önemli ölçüde bırakır. Veri kümenizi uygulanabilir olduğunda büyükse, toousing hello değiştirmeyi göz önünde bulundurun **sqlWriterCleanupScript** özelliği.
  * Merhaba yapılandırırsanız **sqlWriterCleanupScript** özelliği her kopyalama etkinliği için çalıştırın, hello hizmet Tetikleyicileri hello komut dosyası ve ardından hello toplu kopyalama API tooinsert hello verileri kullanın. Örneğin, hello en son verilerle toooverwrite hello tüm tablo, betik toofirst hello kaynağından toplu yükleme hello yeni veri önce tüm kayıtları silin belirtebilirsiniz.
* **Veri düzeni ve toplu işlem boyutu**:
  * Tablo şemasını kopyalama verimlilik etkiler. toocopy Merhaba aynı veri miktarı, büyük satır boyutu hello veritabanı daha verimli bir şekilde daha az veri toplu yürütme çünkü küçük satır boyutu daha iyi performans sağlar.
  * Kopyalama etkinliği, toplu bir dizi veri ekler. Hello kullanarak bir toplu işlemde hello satır sayısını ayarlayabilirsiniz **writeBatchSize** özelliği. Verilerinizi küçük satırları varsa, hello ayarlayabilirsiniz **writeBatchSize** daha yüksek bir değer toobenefit daha az toplu iş yükü ve daha yüksek verimlilik özelliğiyle. Verilerinizin Hello satır boyutu büyükse, artırmanız dikkatli olun **writeBatchSize**. Yüksek bir değer hello veritabanı aşırı yüklemesi nedeniyle tooa kopyalama hatası neden olabilir.
* İçin **içi ilişkisel veritabanları** SQL Server ve hello kullanılmasını Oracle gibi **veri yönetimi ağ geçidi**, hello bkz [veri yönetimi ağ geçididikkatealınacaknoktalar](#considerations-for-data-management-gateway) bölümü.

### <a name="nosql-stores"></a>NoSQL depoları
*(Tablo depolama ve Azure Cosmos DB içerir)*

* İçin **tablo depolama**:
  * **Bölüm**: veri toointerleaved bölümlerini büyük ölçüde yazma performansı düşürür. Veri kaynağınızı bölüm anahtarı tarafından Sırala Hello veriler verimli bir şekilde bir bölüme sonra başka bir eklenir veya hello mantığı toowrite hello veri tooa tek bölüm ayarlayın.
* İçin **Azure Cosmos DB**:
  * **Yığın boyutu**: Merhaba **writeBatchSize** özelliği toohello Azure Cosmos DB hizmet toocreate belgeleri hello paralel istek sayısını ayarlar. Artırdığınızda, daha iyi performans düşüklüğü görebilir **writeBatchSize** çünkü daha fazla paralel istekler tooAzure Cosmos DB gönderilir. Ancak, tooAzure Cosmos DB yazdığınızda azaltma izleyin (Merhaba hata iletisidir "oranıdır büyük istek"). Çeşitli Etkenler, belge boyutu dahil olmak üzere hello belgelerdeki koşulları hello sayısını azaltma neden ve hedef koleksiyonunun dizin oluşturma ilkesini hello. tooachieve daha yüksek kopyalama verimlilik, daha iyi bir koleksiyon, örneğin, S3 kullanmayı düşünün.

## <a name="considerations-for-serialization-and-deserialization"></a>Serileştirme ve seri durumundan çıkarma için ilgili önemli noktalar
Giriş veri kümesini veya çıkış veri kümesi bir dosyadır seri hale getirme ve seri durumdan çıkarma ortaya çıkabilir. Bkz: [desteklenen dosya ve sıkıştırma biçimleri](data-factory-supported-file-and-compression-formats.md) kopyalama etkinliği tarafından desteklenen dosya biçimleri hakkında ayrıntılarla.

**Davranış kopyalama**:

* Dosya tabanlı veri depoları arasında dosyaları kopyalanıyor:
  * Girdi ve çıktı veri hem de kümeleri zaman hello aynı ya da hiç dosya biçimi ayarları, hello veri taşıma hizmeti ikili kopyasını herhangi bir seri hale getirme veya seri durumdan çıkarma olmadan yürütür. Kaynak ve havuz dosya biçimi ayarları hangi hello birbirinden farklı daha yüksek verimlilik karşılaştırıldığında toohello senaryo, bkz.
  * Ne zaman giriş ve çıkış veri kümeleri hem metin biçimi ve yalnızca hello kodlama olan türü farklı olan, hello veri taşıma hizmeti yalnızca kodlama dönüştürme yapar. Tüm serileştirme yapmaz ve bazı performans yüküne neden olan seri tooa ikili kopyalama karşılaştırılır.
  * Girdi ve çıktı veri kümesinin her iki farklı dosya biçimleri sahip veya veri taşıma hizmeti sınırlayıcıların gibi farklı yapılandırmaları hello olduğunda kaynak veri toostream seri durumdan çıkarır, dönüştürme ve belirttiğiniz hello çıkış biçimine seri hale. Bu işlem sonuçları çok daha önemli performans yükü tooother senaryoları karşılaştırılan.
* Dosyaları (örneğin, bir dosya tabanlı depolama tooa ilişkisel deposundan) dosya tabanlı olmayan bir veri deposu/gruptan kopyaladığınızda, hello seri hale getirme veya seri durumdan çıkarma adım gereklidir. Bu adım, önemli performans ek yükü sonuçlanır.

**Dosya biçimi**: seçtiğiniz hello dosya biçimi, kopyalama performansını etkileyebilir. Örneğin, Avro meta verilerle depolar sıkıştırılmış bir ikili biçimi ' dir. Merhaba Hadoop ekosistemindeki işleme ve sorgulama için geniş bir desteğe sahiptir. Ancak, Avro seri hale getirme ve seri durumdan çıkarma, daha düşük kopyalama işleme hangi sonuçlarında tootext biçimi karşılaştırıldığında daha pahalı olması. Dosya biçimi akış bütünsel işleme hello boyunca seçiminizi yapın. Hangi form hello verileri depolanan ile başlatmak için veri depolarını veya dış sistemlerden ayıklanan toobe kaynak; Merhaba depolama, analitik işleme ve sorgulama için en iyi biçimi; ve hangi biçiminde raporlama ve görselleştirme araçları için data Mart içine hello veri verilmesi. Bazen için uygun olmayan bir dosya biçimi okuma ve performans, iyi bir seçimdir olabilir, hello genel analitik göz önüne aldığınızda yazma işlemi.

## <a name="considerations-for-compression"></a>Sıkıştırma için ilgili önemli noktalar
Giriş veya çıkış Veri kümenizi bir dosyası olduğunda, veri toohello hedef yazar gibi kopyalama etkinliği tooperform sıkıştırma veya açma işlemi ayarlayabilirsiniz. Sıkıştırma seçtiğinizde, giriş/çıkış (g/ç) arasında bir kolaylığını yapmak ve CPU. Merhaba verileri sıkıştırma işlem kaynaklarını maliyetleri de ek. Ancak buna karşılık, ağ g/ç ve depolama azaltır. Verilerinizi bağlı olarak artırma genel kopyalama üretilen işi de görebilirsiniz.

**Codec**: GZIP, bzıp2 ve Deflate sıkıştırma türleri kopyalama etkinliği destekler. Azure Hdınsight, tüm üç tür işleme için kullanabilir. Her bir sıkıştırma codec avantajları vardır. Örneğin, bzıp2 hello düşük kopyalama üretilen işi olan, ancak işleme için bölme için hello en iyi Hive sorgu performansı bzıp2 ile alırsınız. Gzip en dengeli hello seçenektir ve kullanıldığı çoğunlukla hello. Uçtan uca senaryonuza uygun hello codec seçin.

**Düzey**: her bir sıkıştırma codec için iki seçenek arasından seçim yapabilirsiniz: hızlı sıkıştırılmış ve verimli sıkıştırılmış. Merhaba elde edilen dosyası en iyi şekilde sıkıştırılmaz olsa bile hello hızlı sıkıştırılmış seçeneği hello veri mümkün olan en kısa sürede sıkıştırır. Merhaba en iyi şekilde sıkıştırılmış seçenek sıkıştırmayı daha fazla zaman harcayan ve en az miktarda veri ortaya çıkarır. Çalışmanızın daha iyi genel performans sağlayan iki seçenekleri toosee test edebilirsiniz.

**Önemli bir unsur**: toocopy büyük miktarda bir şirket içi depolama ve hello bulut arasında veri sıkıştırma ile Ara blob depolama kullanmayı düşünün. Geçici depolama kullanarak şirket ağınıza ve Azure hizmetlerinizi hello bant genişliği hello sınırlayıcı faktördür ve veri kümesi hello girdi ve çıktı verilerini her iki toobe sıkıştırılmamış formunda istediğinizde yararlıdır. Daha açık belirtmek gerekirse, iki kopyalama etkinliklerine tek kopyalama etkinliği bozulabilir. Merhaba ilk kopyalama etkinliği kopyalarından hello kaynak tooan geçici veya sıkıştırılmış biçimde hazırlama blob. Merhaba ikinci kopyalama etkinliği hazırlamadan sıkıştırılmış hello verileri kopyalar ve toohello havuz yazarken sonra açar.

## <a name="considerations-for-column-mapping"></a>Sütun eşlemesi için ilgili önemli noktalar
Merhaba ayarlayabilirsiniz **columnMappings** kopyalama etkinliği toomap tüm veya bir alt kümesini hello özelliği giriş sütunları toohello çıkış sütunları. Merhaba veri taşıma hizmeti hello veri hello kaynağından okuduktan sonra hello veri toohello havuzunu yazmaya başlamadan önce tooperform sütun eşlemesi hello verileri gerekir. Bu ek işleme kopyalama performansını düşürür.

Kaynak veri deposu sorgulanabilir ise, örneğin, SQL Database veya SQL Server gibi ilişkisel bir mağaza ise ya da bir NoSQL deposu Table storage veya Azure Cosmos DB gibi ise mantığı toohello yeniden sıralama ve sütun hello filtreleme Ftp'den göz önünde bulundurun **sorgu**  sütun eşlemesi kullanmak yerine özelliği. Merhaba veri taşıma hizmeti çok daha verimli olduğu hello kaynak verileri verileri depolamak okurken bu şekilde hello projeksiyon oluşur.

## <a name="other-considerations"></a>Diğer konular
Merhaba, boyut toocopy büyük, ayarlayabileceğiniz istediğiniz verileri kullanarak, iş mantığı toofurther bölüm hello verilerinizi veri fabrikasında mekanizması dilimleme hello. Ardından, kopyalama etkinliği toorun tooreduce hello veri boyutu her kopyalama etkinliği çalıştırmak daha sık zamanlayın.

Olması hello sayısı veri kümeleri ve Data Factory tooconnector toohello gerektiren kopyalama etkinlikleri hakkında dikkatli aynı veri hello aynı depolama süresi. Çok sayıda eş zamanlı kopyası işleri bir veri deposu azaltma ve sağlama toodegraded performans, iş iç yeniden deneme, Kopyala ve bazı durumlarda, yürütme hatası.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Örnek senaryo: bir şirket içi SQL Server tooBlob depolama biriminden kopyalama
**Senaryo**: bir ardışık düzen CSV biçiminde bir şirket içi SQL Server tooBlob depolama toocopy verilerden oluşturulur. toomake kopyalama işini daha hızlı Merhaba, hello CSV dosyaları bzıp2 biçime sıkıştırılmış.

**Test ve analiz**: kopyalama etkinliği hello verimini olduğu değerinden 2 MB/sn, hangi hello performans Kıyaslama yavaştır.

**Performans Analizi ve ayarlama**: tootroubleshoot Merhaba performans sorunu, nasıl hello veri işlenen taşınır ve konumundaki bakalım.

1. **Veri Okuma**: ağ geçidi bağlantı tooSQL sunucu açar ve hello sorgusu gönderir. SQL Server hello veri akışı tooGateway hello intranet üzerinden göndererek yanıt verir.
2. **Seri hale getirmek ve verileri sıkıştırmak**: ağ geçidi hello veri akışı tooCSV biçimi serileştirir ve sıkıştırır hello veri tooa bzıp2 akışı.
3. **Veri yazma**: ağ geçidi hello bzıp2 akış tooBlob depolama hello Internet aracılığıyla yükler.

Gördüğünüz gibi hello veri okunduğunu işlenir ve bir akış sıralı şekilde taşındı: SQL Server > LAN > ağ geçidi > WAN > Blob Depolama. **Merhaba genel performansı hello en düşük işleme tarafından hello ardışık düzeni işlenir**.

![Veri akışı](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Bir veya daha fazla Etkenler aşağıdaki hello hello performans düşüklüğü neden olabilir:

* **Kaynak**: SQL Server kendisini nedeniyle ağır yük düşük işleme sahiptir.
* **Veri Yönetimi ağ geçidi**:
  * **LAN**: ağ geçidi hello SQL Server makinesinde gölgeden uzak bulunur ve düşük bant genişlikli bağlantısı vardır.
  * **Ağ geçidi**: ağ geçidi operations aşağıdaki kendi yükü sınırlamaları tooperform hello ulaştı:
    * **Seri hale getirme**: hello veri akışı tooCSV seri hale getirme biçimi yavaş işleme sahiptir.
    * **Sıkıştırma**: yavaş sıkıştırma codec (2.8 MB/sn Çekirdek i7 ile olan Örneğin, bzıp2,) seçtiniz.
  * **WAN**: Azure hizmetlerinizi hello şirket ağı arasında hello bant azaldığını (örneğin, T1 1,544 kbps; = T2 6,312 kbps =).
* **Havuz**: Blob depolama alanına sahip düşük işleme. (Bu senaryoda en az 60 MB/sn SLA'sını güvence altına alır çünkü düşüktür.)

Bu durumda, bzıp2 veri sıkıştırma hello tüm ardışık düzen yavaşlamasının. Tooa gzip sıkıştırma codec geçiş bu performans sorunu kolaylaştırır.

## <a name="sample-scenarios-use-parallel-copy"></a>Örnek senaryo: paralel kopyasını kullanın
**Senaryo I:** hello şirket içi dosya sistemi tooBlob depolama biriminden 1.000 1 MB'lık dosyaları kopyalayın.

**Çözümleme ve performans ayarlama**: dört çekirdekli makine üzerinde ağ geçidi yüklediyseniz, bir örnek için veri fabrikası 16 paralel toomove dosyalarını kopyalar hello dosya sistemi tooBlob depolama biriminden eşzamanlı olarak kullanır. Bu paralel yürütme yüksek performans neden olur. Merhaba paralel kopya sayısı da açıkça belirtebilirsiniz. Çok sayıda küçük dosya kopyaladığınızda, paralel kopyaları önemli ölçüde işleme kaynakları daha verimli şekilde kullanarak yardımcı olur.

![Senaryo 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**Senaryo II**: Blob Depolama Lake deposu Analytics tooData 500 MB'lık 20 BLOB'lar kopyalayın ve performansı ayarlamak.

**Çözümleme ve performans ayarlama**: Bu senaryoda, veri fabrikası hello verileri Blob Depolama tooData Lake deposundan tek kopya kullanarak kopyalar (**parallelCopies** ayarlamak too1) ve tek bulut veri taşıma birimleri. Merhaba verimlilik, hello açıklanan Kapat toothat olması gözlemlemek [performans başvuru bölümünde](#performance-reference).   

![Senaryo 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**Senaryo III**: tek tek dosya boyutu MB düzinelerce büyük ve toplam birim büyük değil.

**Çözümleme ve performans dönüş**: artırma **parallelCopies** hello kaynak sınırlamaları tek bulut DMU nedeniyle kopyalama daha iyi performans elde edemezseniz. Bunun yerine, daha fazla bulut DMUs tooget daha fazla kaynak tooperform hello veri taşıma belirtmeniz gerekir. Hello için bir değer belirtmezseniz **parallelCopies** özelliği. Veri Fabrikası hello paralellik işler. Bu durumda, ayarlarsanız **cloudDataMovementUnits** too4, dört kez hakkında verimliliğinden oluşur.

![Senaryo 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>Başvuru
Performans izleme ve bazı hello desteklenen veri depoları için başvuru ayarlama şunlardır:

* Azure Storage (Blob Depolama ve tablo depolama dahil): [Azure Storage ölçeklenebilirlik hedefleri](../storage/common/storage-scalability-targets.md) ve [Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage/common/storage-performance-checklist.md)
* Azure SQL Database: Yapabilecekleriniz [hello performansı izleyerek](../sql-database/sql-database-single-database-monitor.md) ve hello veritabanı işlem birimi (DTU) yüzde denetleyin
* Azure SQL Data Warehouse: Veri ambarı birimlerini (Dwu'lar); kendi yeteneği ölçülür bkz: [Yönet işlem güç Azure SQL Data warehouse'da (genel bakış)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB: [Azure Cosmos veritabanı performans düzeyleri](../documentdb/documentdb-performance-levels.md)
* Şirket içi SQL Server: [İzleyici ve performans ayarlama](https://msdn.microsoft.com/library/ms189081.aspx)
* Şirket içi dosya sunucusu: [dosya sunucuları için performans ayarlama](https://msdn.microsoft.com/library/dn567661.aspx)
