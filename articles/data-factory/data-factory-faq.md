---
title: "aaaAzure Data Factory - sık sorulan sorular"
description: "Azure Data Factory hakkında sık sorulan sorular."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure Data Factory - sık sorulan sorular
## <a name="general-questions"></a>Genel sorular
### <a name="what-is-azure-data-factory"></a>Azure Data Factory nedir?
Veri Fabrikası olan bulut tabanlı bir veri tümleştirme hizmeti **hello taşınmasını ve dönüştürülmesini veri otomatikleştirir**. Donanım tootake hammaddeleri çalıştıran ve bunları tamamlanmış ürünlere dönüştürmek yalnızca bir fabrikası gibi Data Factory ham verileri toplayan ve kullanıma hazır bilgilere dönüştürür var olan hizmetleri düzenler.

Veri Fabrikası hem şirket içi ve bulut veri depolarına yanı sıra Azure Hdınsight ve Azure Data Lake Analytics gibi işlem hizmetleri kullanarak işlem/dönüştürme verileri arasında toocreate veri temelli iş akışlarını toomove verileri sağlar. Gereksinim duyduğunuz hello eylem gerçekleştiren bir işlem hattını oluşturduktan sonra toorun düzenli aralıklarla (saatlik, günlük, haftalık vb.) zamanlayabilirsiniz.   

Daha fazla bilgi için bkz: [genel bakış & anahtar kavramlar](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Nereden bulabilirim Azure Data Factory için fiyatlandırma ayrıntıları?
Bkz: [veri fabrikası fiyatlandırma ayrıntıları sayfası] [ adf-pricing-details] fiyatlandırma ayrıntıları hello Azure Data Factory için hello için.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>Azure Data Factory ile çalışmaya nasıl?
* Azure Data Factory genel bakış için bkz: [giriş tooAzure Data Factory](data-factory-introduction.md).
* Nasıl bir öğretici için çok**copy/move veri** kopyalama etkinliği'ni kullanarak bkz [Azure Blob Storage tooAzure SQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Nasıl bir öğretici için çok**verileri** Hdınsight Hive etkinliği kullanma. Bkz: [Hadoop kümesindeki Hive betiği çalıştırılarak verileri işlemek](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>Merhaba veri fabrikasının bölge kullanılabilirliği nedir?
Veri Fabrikası sağlanmıştır **BİZE Batı** ve **Kuzey Avrupa**. işlem hello ve depolama hizmetleri veri fabrikaları tarafından kullanılan başka bölgelerde olabilir. Bkz: [desteklenen bölgeler](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Veri fabrikaları/işlem hatları/etkinlikleri/veri kümeleri sayısının hello sınırları nelerdir?
Bkz: **Azure veri fabrikası sınırları** hello bölümünü [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md#data-factory-limits) makalesi.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Azure Data Factory hizmeti ile Merhaba yazma geliştirici deneyimi nedir?
Yazar/data Factory araçları/SDK'ları aşağıdaki hello birini kullanarak oluşturabilirsiniz:

* **Azure portal** zengin bir kullanıcı arabirimi, toocreate veri fabrikaları bağlı ad hizmetleri sağlamak hello Data Factory dikey hello Azure portal'ın. Merhaba **Data Factory düzenleyici**, aynı zamanda hello portal parçası olan, sağlar, tooeasily oluşturma bağlı hizmetler, tablolar, veri kümelerini ve ardışık düzen bu yapılar için JSON tanımları belirterek. Bkz [Azure portalını kullanarak ilk veri işlem hattınızı oluşturma](data-factory-build-your-first-pipeline-using-editor.md) kullanmaya ilişkin bir örnek portal/Düzenleyicisi toocreate hello ve bir veri fabrikası dağıtın.
* **Visual Studio** Visual Studio toocreate bir Azure data factory kullanabilirsiniz. Bkz: [Visual Studio kullanarak ilk veri işlem hattınızı oluşturma](data-factory-build-your-first-pipeline-using-vs.md) Ayrıntılar için.
* **Azure PowerShell** bkz [oluşturma ve İzleyici Azure PowerShell kullanarak Azure Data Factory](data-factory-build-your-first-pipeline-using-powershell.md) bir öğretici/PowerShell kullanarak bir veri fabrikası oluşturmaya yönelik kılavuz. Bkz: [Data Factory Cmdlet başvurusu] [ adf-powershell-reference] Data Factory cmdlet'lerini ilişkin kapsamlı belgeler için MSDN kitaplığında içerik.
* **.NET sınıf kitaplığı** Data Factory .NET SDK kullanarak program aracılığıyla veri fabrikaları oluşturabilirsiniz. Bkz: [oluşturun, izlemek ve .NET SDK kullanarak veri fabrikaları yönetmek](data-factory-create-data-factories-programmatically.md) .NET SDK kullanarak bir veri fabrikası oluşturma kılavuz. Bkz: [Data Factory sınıf kitaplığı başvurusu] [ msdn-class-library-reference] veri fabrikası .NET SDK'sının kapsamlı belgeler.
* **REST API** de hello hello Azure Data Factory hizmeti toocreate tarafından kullanıma sunulan REST API kullanın ve veri fabrikaları dağıtın. Bkz: [Data Factory REST API Başvurusu] [ msdn-rest-api-reference] veri fabrikası REST API kapsamlı belgeler.
* **Azure Resource Manager şablonu** bkz [Öğreticisi: Azure Resource Manager şablonu kullanarak ilk Azure data factory'nizi derleme](data-factory-build-your-first-pipeline-using-arm.md) fo ayrıntıları.

### <a name="can-i-rename-a-data-factory"></a>Veri Fabrikası yeniden adlandırabilir miyim?
Hayır. Diğer Azure kaynaklarına gibi bir Azure data factory hello adı değiştirilemez.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>Bir Azure aboneliği tooanother veri fabrikası taşıyabilir miyim?
Evet. Kullanım hello **taşıma** hello Aşağıdaki diyagramda gösterildiği gibi veri fabrikası dikey penceresinde düğmesi:

![Veri Fabrikası taşıma](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Data Factory ile desteklenen hello bilgi işlem ortamları nelerdir?
Merhaba aşağıdaki tabloda bilgi işlem ortamları üzerlerinde çalıştırabilirsiniz Data Factory ve hello etkinlikler tarafından desteklenen bir listesini sağlar.

| İşlem ortamı | etkinlikler |
| --- | --- |
| [İsteğe bağlı Hdınsight kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) veya [kendi Hdınsight kümenizi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop akış](data-factory-hadoop-streaming-activity.md) |
| [Azure toplu işlem](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Machine Learning etkinlikleri: Toplu Yürütme ve Kaynak Güncelleştirme](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Data Lake Analytics U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL veri ambarı](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Saklı Yordam](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Azure Data Factory SQL Server Integration Services (SSIS) ile nasıl karşılaştırmak? 
Merhaba bkz [Azure Data Factory vs. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) bizim MVP (en değerli uzmanları) birini sunudan: Reza Rad. Veri Fabrikası'nda hello son değişikliklerden bazıları hello slayt paketiyle listelenmeyebilir. Daha fazla özellikleri tooAzure Data Factory sürekli olarak ekliyoruz. Daha fazla özellikleri tooAzure Data Factory sürekli olarak ekliyoruz. Biz bu güncelleştirmeleri Microsoft'tan veri tümleştirme teknolojileri hello karşılaştırması içine süre daha sonra bu yıl dahil.   

## <a name="activities---faq"></a>Etkinlikler - SSS
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Bir Data Factory işlem hattı kullanabilirsiniz etkinliklerin hello farklı türleri nelerdir?
* [Veri taşıma etkinlikleri](data-factory-data-movement-activities.md) toomove veri.
* [Veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) tooprocess/dönüştürme veri.

### <a name="when-does-an-activity-run"></a>Bir etkinlik çalıştırıldığında?
Merhaba **kullanılabilirlik** hello yapılandırma ayarında çıktı veri tablosu hello etkinlik çalıştırıldığında belirler. Giriş veri kümeleri belirtilirse, hello etkinlik tüm hello giriş verisi bağımlılıkların olup olmadığını denetler (diğer bir deyişle, **hazır** durumu) çalıştıran başlatılmadan önce.

## <a name="copy-activity---faq"></a>Kopya etkinliği - SSS
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>Birden çok etkinliği ile işlem hattı veya ayrı bir ardışık düzen her etkinlik için daha iyi toohave mi?
Ardışık Düzen beklenen toobundle ilgili etkinlikler. Bunları bağlamak hello veri kümeleri herhangi bir etkinlik dışında hello ardışık düzen tarafından tüketilen değil, bir ardışık düzeninde hello etkinlikleri tutabilirsiniz. Böylece birbirleri ile Hizala bu şekilde, toochain ardışık düzen etkin nokta ihtiyaç duymaz. Ayrıca, hello ardışık düzeni güncellenirken hello veri bütünlüğü hello tabloları iç toohello ardışık düzeninde daha iyi korunur. Ardışık Düzen güncelleştirme temelde hello ardışık düzen içindeki tüm hello etkinlikleri durdurur, bunları kaldırır ve bunları yeniden oluşturur. Perspektif geliştirme, ilgili hello içindeki verilerin daha kolay toosee hello akış de olabilir bir JSON aktivitelerde hello ardışık düzeni için dosya.

### <a name="what-are-hello-supported-data-stores"></a>Desteklenen veri depoları hello nelerdir?
Data Factory kopyalama etkinliği, bir kaynak veri deposu tooa havuz veri deposundan verileri kopyalar. Data Factory veri depolarına aşağıdaki hello destekler. Herhangi bir kaynaktan veri tooany havuz yazılabilir. Bir veri deposu toolearn nasıl tıklatın toocopy veri tooand o depolama alanından.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Veri depolar ile * şirket içi olabilir veya Azure Iaas ve tooinstall gerektiren [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) , şirket içi/Azure Iaas makinede.

### <a name="what-are-hello-supported-file-formats"></a>Desteklenen dosya biçimleri hello nelerdir?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Merhaba kopyalama işlemi gerçekleştirildiği?
Bkz: [genel olarak kullanılabilir veri taşıma](data-factory-data-movement-activities.md#global) ayrıntıları bölümü. Kısacası, bir şirket içi veri deposu söz konusu olduğunda hello veri yönetimi ağ geçidi, şirket içi ortamınızda hello kopyalama işlemi gerçekleştirilir. Ve hello veri taşıma iki bulut depoları arasında olduğunda hello kopyalama işlemi hello bölgeye en yakın toohello havuz konumda hello gerçekleştirilir aynı coğrafi konum.

## <a name="hdinsight-activity---faq"></a>Hdınsight etkinliği - SSS
### <a name="what-regions-are-supported-by-hdinsight"></a>Hangi bölgeleri Hdınsight tarafından destekleniyor mu?
Bkz: Merhaba aşağıdaki makaleye bakın hello bölümünde coğrafi kullanılabilirlik: veya [Hdınsight fiyatlandırma ayrıntıları][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>Hangi bölge isteğe bağlı Hdınsight kümesi tarafından kullanılır?
Merhaba isteğe bağlı Hdınsight kümesi hello aynı oluşturulan hello kümesi ile kullanılan toobe belirtilen hello depolama bulunduğu bölge.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Nasıl tooyour Hdınsight kümesi tooassociate ek depolama hesapları?
Kendi Hdınsight kümenizi (BYOC - Getir bilgisayarınızı kendi küme) kullanıyorsanız, aşağıdaki konularda hello bakın:

* [Alternatif depolama hesapları ve meta Depolarla Hdınsight kümesi kullanma][hdinsight-alternate-storage]
* [Ek depolama hesapları ile Hdınsight Hive kullanma][hdinsight-alternate-storage-2]

Merhaba Data Factory hizmeti tarafından oluşturulan bir isteğe bağlı küme kullanıyorsanız, böylece hello Data Factory hizmetinin bunları sizin adınıza kaydedebilirsiniz hello Hdınsight için ek depolama hesapları hizmeti bağlı belirtin. Hello hello isteğe bağlı hizmet için JSON tanımı, kullanın **additionalLinkedServiceNames** özelliği toospecify alternatif depolama hesapları hello JSON parçacığı aşağıdaki gösterildiği gibi:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
Merhaba yukarıdaki örnekte, Hdınsight küme gereksinimlerini tooaccess alternatif depolama hesapları hello kimlik bilgileri olan tanımlarını içeren bağlı hizmetler otherLinkedServiceName1 ve otherLinkedServiceName2 temsil eder.

## <a name="slices---faq"></a>Dilimler - SSS
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Neden my girdi dilimi hazır durumda değil misiniz?
Genel bir hata değildir ayarı **dış** özelliği çok**true** üzerinde hello hello giriş girdi veri kümesi (Merhaba veri fabrikası tarafından üretilen değil) dış toohello veri fabrikası olduğu.

Aşağıdaki örneğine hello tooset yeterlidir **dış** üzerinde tootrue **dataset1**.  

**DataFactory1** kanal 1: dataset1 activity1 -> -> dataset2 -> activity2 dataset3 ardışık düzen 2 ->: dataset3 -> activity3 ancak dataset4 ->

Başka bir data factory (2 1 veri fabrikasında ardışık düzen tarafından üretilen) dataset4 alan bir işlem hattı ile varsa, bir farklı veri fabrikası (DataFactory1, değil DataFactory2) hello dataset oluşturduğundan dataset4 dış bir veri kümesi işaretleyin.  

**DataFactory2**    
Ardışık Düzen 1: dataset4 -> activity4 dataset5 ->

Hello dış özelliği doğru olarak ayarlanırsa, hello giriş verisi hello girdi veri kümesi tanımında belirtilen hello konumda var olup olmadığını doğrulayın.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Ne zaman hello dilim üretileceğini günlük gece'den başka bir zaman dilimi toorun?
Kullanım hello **uzaklık** hello dilim toobe istediğiniz özellik toospecify hello zaman üretilen. Bkz: [Dataset kullanılabilirliği](data-factory-create-datasets.md#dataset-availability) bu özellik hakkında ayrıntılı bilgi için bölüm. Kısa bir örnek aşağıda verilmiştir:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Günlük dilimler Başlat **6'da** hello varsayılan gece yerine.     

### <a name="how-can-i-rerun-a-slice"></a>Bir dilim nasıl yeniden çalıştırabilir miyim?
Bir dilim yolları aşağıdaki hello birinde çalıştırabilirsiniz:

* İzleme ve yönetme uygulaması toorerun bir etkinlik penceresini veya dilim kullanın. Bkz: [seçilen yeniden çalıştır etkinliği windows](data-factory-monitor-manage-app.md#perform-batch-actions) yönergeler için.   
* Tıklatın **çalıştırmak** hello hello komut çubuğunda **veri DİLİMİ** hello dilimi hello Azure portal dikey penceresinde.
* Çalıştırma **Set-AzureRmDataFactorySliceStatus** durum cmdlet'iyle ayarlamak çok**bekleyen** hello dilim için.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Bkz: [Set-AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] hello cmdlet hakkında ayrıntılı bilgi için.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>Ne kadar süreyle tooprocess bir dilim sürdü?
İzleme ve yönetme uygulaması tooknow içinde veri dilimi tooprocess sürdü ne kadar süreyle etkinlik penceresini Gezgini'ni kullanın. Bkz: [etkinlik penceresini Explorer](data-factory-monitor-manage-app.md#activity-window-explorer) Ayrıntılar için.

Ayrıca yapabilirsiniz hello Azure portalı aşağıdaki hello:  

1. Tıklatın **veri kümeleri** döşeme hello üzerinde **DATA FACTORY** veri fabrikanızın dikey.
2. Merhaba belirli veri kümesine Hello tıklatın **veri kümeleri** dikey.
3. Hello ilgilendiğiniz select hello dilim **son dilimler** hello listede **tablo** dikey.
4. Hello çalıştırmak hello etkinliği tıklatın **etkinlik çalışması** hello listede **veri DİLİMİ** dikey.
5. Tıklatın **özellikleri** döşeme hello üzerinde **etkinlik çalışma ayrıntıları** dikey.
6. Merhaba görmelisiniz **süresi** alan bir değere sahip. Bu değer, tooprocess hello dilim gerçekleştirilecek hello saattir.   

### <a name="how-toostop-a-running-slice"></a>Nasıl toostop çalışan bir dilim?
Yürütülmesini toostop hello ardışık düzen gerekiyorsa, kullanabileceğiniz [Suspend-AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet'i. Şu anda hello ardışık düzen askıya sürüyor hello dilim yürütmeleri durdurmaz. Merhaba sürüyor yürütmeleri tamamladıktan sonra ek bir dilim çekilir.

Gerçekten toostop tüm hello yürütmeleri hemen isterseniz, hello tek yöntem toodelete hello ardışık olması ve yeniden oluşturun. Toodelete hello ardışık düzen seçerseniz, düzenleme toodelete tabloları ve bağlantılı Hizmetleri hello ardışık düzen tarafından kullanılan gerekmez.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
