---
title: "aaaIntroduction tooData Fabrika, bir veri tümleştirme hizmeti | Microsoft Docs"
description: "Azure Data Factory’nin ne olduğunu öğrenin: verilerin taşınmasını ve dönüştürülmesini düzenleyen ve otomatikleştiren bir bulut veri tümleştirme hizmetidir."
keywords: "veri tümleştirme, bulut veri tümleştirme, azure data factory nedir"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Giriş tooAzure veri fabrikası 
## <a name="what-is-azure-data-factory"></a>Azure Data Factory nedir?
Büyük veri Hello world nasıl mevcut verileri business yararlanır? Şirket içi veri kaynakları veya diğer farklı veri kaynaklarını başvuru verileri kullanarak, hello bulutta oluşturulan olası tooenrich veri mi? Örneğin, bir oyun şirket hello bulutta oyunlar tarafından üretilen birçok günlükleri toplar. Bu günlükler toogain ınsights'da toocustomer tercihleri, demografisine, kullanım davranışı tooanalyze istediği vb. tooidentify yukarı satış ve çapraz satış fırsatları yeni özellikler toodrive iş büyümesi çekici geliştirmek ve daha iyi bir deneyim sağlar toocustomers. 

Bu günlükler hello şirket tooanalyze toouse hello başvuru verileri müşteri bilgileri, bir şirket içi veri deposunda kampanya bilgileri pazarlama oyun bilgileri gibi gerekir. Bu nedenle, hello şirket hello bulut veri deposu tooingest günlük verilerini ve başvuru verileri hello şirket içi veri deposundan ister. Ardından, işlem hello verileri Hadoop hello kullanarak (Azure Hdınsight) Bulut ve hello sonuç verilerini Azure SQL Data Warehouse veya bir şirket içi veri gibi bir bulut veri ambarında SQL Server gibi depolamak yayımlayın. Bu iş akışı toorun haftada bir kez istediği. 

Gerekenleri Hadoop gibi varolan işlem hizmetlerini kullanarak şirket içi ve bulut veri depolarına veri ve dönüşüm ya da işlem verileri alma ve yayımlama hello sonuçları tooan şirket içi bir iş akışı hello şirket toocreate izin veren bir platformudur veya BI uygulamaları tooconsume için bulut veri deposu. 

![Data Factory'ye genel bakış](media/data-factory-introduction/what-is-azure-data-factory.png) 

Azure Data Factory, bu tür senaryoların hello platformudur. Bu bir **toocreate veri temelli iş akışlarını yönetme ve veri taşıma ve veri dönüştürme otomatikleştirme hello bulutta sağlayan bulut tabanlı veri tümleştirme hizmeti**. Azure Data Factory kullanarak oluşturun ve farklı veri depolarına verilerden alma ve işlem/hello veri dönüştürme Azure Hdınsight Hadoop, Spark, Azure Data Lake gibi işlem hizmetlerini kullanarak (ardışık olarak adlandırılır) veri temelli iş akışlarını zamanlama Analizler ve Azure Machine Learning ve veri toodata depolar Azure SQL Data Warehouse gibi iş zekası (BI) uygulamaları tooconsume için çıktı yayımlayın.  

Bu, geleneksel bir Ayıklama-Dönüştürme-Yükleme (ETL) platformu yerine daha çok Ayıklama-Dönüştürme (EL) ve sonra Dönüştürme-Yükleme (TL) platformudur. gerçekleştirilen hello dönüşümleri tootransform/işlem verileri işlem hizmetlerini kullanarak yerine çok sayıda satırı, sıralama vb. sayım sütun eklemek için olanları hello gibi tooperform dönüşümleri türetilmiş. 

Şu anda, Azure Data Factory'de tüketilen ve iş akışları tarafından üretilen hello verilerdir **zaman dilimlenebilir veri** (saatlik, günlük, haftalık, vb.). Örneğin, bir işlem hattı günde bir kez giriş verilerini okuyabilir, verileri işleyebilir ve çıktı üretebilir. Bir iş akışını yalnızca bir kez de çalıştırabilirsiniz.  
  

## <a name="how-does-it-work"></a>Nasıl çalışır? 
Azure veri fabrikası'nda Hello ardışık düzen (veri temelli iş akışlarını) genellikle hello aşağıdaki üç adımları gerçekleştirin:

![Azure Data Factory’nin üç aşaması](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Bağlanma ve toplama
Kuruluşların dağınık kaynaklarda yer alan çeşitli türlerde verileri vardır. Merhaba bilgi üretim sistemi oluşturmanın ilk adımı olduğundan veri tooconnect tooall hello gerekli kaynakları ve işleme, SaaS Hizmetleri gibi dosya paylaşımları, FTP, web hizmetleri ve için hello veri merkezi gerektiği tooa konumu sonraki işleniyor.

Veri Fabrikası kuruluşların derleme özel veri taşıma bileşenlerini veya bu veri kaynakları ve işleme özel hizmetler toointegrate yazma gerekir. Pahalı ve sabit toointegrate olduğundan ve bu sistemlere korumak ve izleme ve uyarma hello Kurumsal düzeyde ve tam olarak yönetilen bir hizmet sunabilir hello denetimleri genellikle eksik.

Data Factory ile hem şirket içi veri ardışık düzen toomove veri kopyalama etkinliği hello kullanın ve kaynak veri depoları tooa merkezileşmeyi veri deposunda hello bulut daha fazla çözümleme için bulut. Örneğin, bir Azure Data Lake Analytics işlem hizmetini kullanarak bir Azure Data Lake Store ve dönüştürme hello verilerini daha sonra toplayabilirsiniz. Öte yandan, verileri Azure Blob Depolama Alanı’ndan toplayıp daha sonra Azure HDInsight Hadoop kümesi kullanarak da dönüştürebilirsiniz.

### <a name="transform-and-enrich"></a>Dönüştürme ve zenginleştirme
Veri merkezi veri deposunda hello bulutta mevcut olduğunda, işlenen veya Hdınsight Hadoop, Spark, Data Lake Analytics ve Machine Learning gibi işlem hizmetlerini kullanarak dönüştürülen hello toplanan verileri toobe istiyor. İle güvenilir veri sürdürülebilir ve denetlenen zamanlama toofeed üretim ortamlarında tooreliably dönüştürülmüş üretim verileri istediğiniz. 

### <a name="publish"></a>Yayımlama 
Dönüştürülen veriler tooon içi kaynakları SQL Server gibi hello buluttan teslim ya da içinde bulut depolama kaynakları tüketimi için iş zekası (BI) ve analiz araçları ve diğer uygulamalar tarafından kalmasını sağlamak.

## <a name="key-components"></a>Başlıca bileşenler
Azure aboneliğinin bir veya birden çok Azure Data Factory örneği (veya veri fabrikası) olabilir. Azure Data Factory veri temelli iş akışlarını adımları toomove ve dönüştürme verilerle oluşturan tooprovide hello platform birlikte çalışan dört anahtar bileşenleri kümesinden oluşur. 

### <a name="pipeline"></a>İşlem hattı
Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattı bir grup etkinliktir. Birlikte hello etkinlikleri ardışık düzeninde bir görevi gerçekleştirebilirsiniz. Örneğin, bir işlem hattı bir Azure blob verilerini alır etkinlikleri grubunu içerir ve ardından bir Hive sorgusu bir Hdınsight kümesi toopartition hello veri çalıştırın. Bu Hello avantajı, o hello ardışık düzen toomanage hello etkinliklerin her biri yerine bir küme olarak ayrı ayrı sağlar ' dir. Örneğin, dağıtmak ve hello etkinlikleri yerine hello ardışık düzen bağımsız olarak zamanlayabilirsiniz. 

### <a name="activity"></a>Etkinlik
İşlem hattında bir veya daha fazla etkinlik olabilir. Etkinlikler, verilerinizde hello Eylemler tooperform tanımlayın. Örneğin, bir veri deposu tooanother veri deposundan kopyalama etkinliği toocopy veri kullanabilir. Benzer şekilde, bir Azure Hdınsight küme tootransform üzerinde bir Hive sorgusu çalıştıran bir Hive etkinliği kullanın veya verilerinizi çözümlemek. Data Factory iki tür etkinliği destekler: veri taşıma etkinlikleri ve veri dönüştürme etkinlikleri.

### <a name="data-movement-activities"></a>Veri taşıma etkinlikleri
Data Factory kopyalama etkinliği, bir kaynak veri deposu tooa havuz veri deposundan verileri kopyalar. Data Factory veri depolarına aşağıdaki hello destekler. Herhangi bir kaynaktan veri tooany havuz yazılabilir. Bir veri deposu toolearn nasıl tıklatın toocopy veri tooand o depolama alanından.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Daha fazla bilgi için [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md) makalesine bakın.

### <a name="data-transformation-activities"></a>Veri dönüştürme etkinlikleri
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Daha fazla bilgi için [Veri Dönüştürme Etkinlikleri](data-factory-data-transformation-activities.md) makalesine bakın.

### <a name="custom-net-activities"></a>Özel .NET etkinlikleri
Bir veri deposundan bu kopyalama etkinliği değil desteği veya kendi mantığı kullanarak verileri, Oluştur toomove verilere ihtiyacınız / bir **özel .NET etkinlik**. Özel bir etkinlik oluşturma ve kullanma hakkında ayrıntılı bilgi için bkz. [Azure Data Factory işlem hattında özel etkinlikler kullanma](data-factory-use-custom-activities.md).

### <a name="datasets"></a>Veri kümeleri
Bir etkinlik girdi olarak sıfır veya daha fazla veri kümesi ve çıktı olarak bir ya da daha fazla veri kümesi alır. Veri kümeleri yalnızca noktası veya toouse etkinliklerinizde giriş veya çıkış istediğiniz hello verileri başvuru hello veri depoları içindeki veri yapılarını temsil eder. Örneğin, bir Azure Blob dataset hello Azure Blob hangi hello ardışık düzen hello veri okumalısınız depolama alanına hello blob kapsayıcısı ve klasörü belirtir. Veya hello tablo toowhich hello çıktı verilerini hello etkinliği tarafından yazılmış bir Azure SQL tablosu veri kümesini belirtir. 

### <a name="linked-services"></a>Bağlı hizmetler
Bağlı hizmetler Data Factory tooconnect tooexternal kaynakları için gerekli hello bağlantı bilgilerini tanımlayın bağlantı dizeleri çok gibidir. Bunu bu şekilde düşünün - hello bağlantı toohello veri kaynağı bağlı hizmet tanımlar ve bir veri kümesi hello verilerin hello yapısını temsil eder. Örneğin, bir Azure Storage bağlı hizmeti bağlantı dizesini tooconnect toohello Azure depolama hesabı belirtir. Ve bir Azure Blob dataset hello blob kapsayıcısı ve hello veri içeren hello klasörü belirtir.   

Bağlı hizmetler Data Factory’de iki amaçla kullanılır:

* toorepresent bir **veri deposu** , ancak bunlarla sınırlı olmamak, bir şirket içi SQL Server, Oracle veritabanı, dosya paylaşımı veya bir Azure Blob Storage hesabı dahil olmak üzere. Merhaba bkz [veri taşıma etkinlikleri](#data-movement-activities) desteklenen veri depoları listesi bölümü.
* toorepresent bir **kaynak işlem** etkinlik hello yürütülmesini barındırabilir. Örneğin, bir Hdınsight Hadoop kümesinde hello Hdınsighthive etkinliğini çalıştırır. Desteklenen işlem ortamlarının listesi için [Veri dönüştürme etkinlikleri](#data-transformation-activities) bölümüne bakın.

### <a name="relationship-between-data-factory-entities"></a>Data Factory varlıkları arasındaki ilişki
![Diyagram: Bir bulut veri tümleştirme hizmeti olan Data Factory ile ilgili Temel Kavramlar](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Figure2.** Veri kümesi, Etkinlik, İşlem Hattı ve Bağlı hizmet arasındaki ilişkiler

## <a name="supported-regions"></a>Desteklenen bölgeler
Şu anda veri fabrikaları hello oluşturabilirsiniz **Batı ABD**, **Doğu ABD**, ve **Kuzey Avrupa** bölgeleri. Ancak, veri fabrikası veri depolarına ve diğer Azure bölgeleri toomove verileri veri depoları arasında Hizmetleri'nde işlem veya kullanarak verileri işlemek işlem Hizmetleri.

Azure Data Factory’nin kendisi verileri depolamaz. Veri temelli iş akışlarını arasında veri tooorchestrate hareketini oluşturmanızı sağlar [desteklenen veri depoları](#data-movement-activities) ve verileri kullanarak işleme [işlem Hizmetleri](#data-transformation-activities) başka bölgelerde veya şirket içi ortam. Ayrıca çok tanır[izlemek ve iş akışlarını yönetme](data-factory-monitor-manage-pipelines.md) programlı her ikisini kullanarak kullanıcı Arabirimi mekanizmalarını.

Data Factory yalnızca kullanılabilir olsa bile **Batı ABD**, **Doğu ABD**, ve **Kuzey Avrupa** bölgeler, veri fabrikası'nda hello veri taşımayı destekleyen hello hizmet kullanılabilir [genel](data-factory-data-movement-activities.md#global) birçok bölgede. Bir veri deposu bir güvenlik duvarının arkasında olduğunda sonra bir [veri yönetimi ağ geçidi](data-factory-move-data-between-onprem-and-cloud.md) bunun yerine, şirket içi ortamına taşır hello verilerinizi yüklü.

Örneğin, Azure HDInsight kümesi ve Azure Machine Learning gibi işlem ortamlarınızın Batı Avrupa bölgesinde çalıştığını varsayalım. Oluşturup Kuzey Avrupa'da bir Azure Data Factory örneğini kullanın ve Batı Avrupa'da işlem ortamlarınızda tooschedule işlerini kullanın. Veri Fabrikası tootrigger hello işi birkaç milisaniye işlem ortamınızda alır ancak bilgi işlem ortamınızın hello işin çalıştırılması hello süre değişmez.

## <a name="get-started-with-creating-a-pipeline"></a>İşlem hattı oluşturmaya başlama
Azure Data Factory'de Bu araçlar ve API'ler toocreate veri ardışık birini kullanabilirsiniz: 

- Azure portalına
- Visual Studio
- PowerShell
- .NET API’si
- REST API
- Azure Resource Manager şablonu. 

nasıl toobuild veri fabrikaları verilerle ardışık düzenleri, toolearn öğreticileri aşağıdaki hello içindeki adım adım yönergeleri izleyin:

| Öğretici | Açıklama |
| --- | --- |
| [İki bulut veri deposu arasında veri taşıma](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |Bu öğreticide, data factory işlem hattı ile oluşturduğunuz **verileri taşır** Blob Depolama tooSQL veritabanından. |
| [Hadoop kümesi kullanarak veri dönüştürme](data-factory-build-your-first-pipeline.md) |Bu öğreticide, bir Azure HDInsight (Hadoop) kümesinde Hive betiği çalıştırarak **veri işleyen** bir veri işlem hattı ile ilk Azure veri fabrikanızı oluşturacaksınız. |
| [Veri Yönetimi Ağ Geçidi'ni kullanarak verileri şirket içi veri deposu ile bulut veri deposu arasında taşıma](data-factory-move-data-between-onprem-and-cloud.md) |Bu öğreticide, data factory işlem hattı ile yapı **verileri taşır** gelen bir **şirket içi** SQL Server veritabanı tooan Azure blob. Merhaba izlenecek bir parçası olarak yükleyin ve makinenizde hello veri yönetimi ağ geçidi yapılandırın. |
