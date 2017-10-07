---
title: "aaaDemand tahmin enerji teknik Kılavuzu | Microsoft Docs"
description: "Bir teknik Kılavuzu toohello çözüm şablonu Microsoft Cortana Intelligence ile isteğe bağlı enerji tahmin için."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>İsteğe bağlı enerji tahmin için teknik Kılavuzu toohello Cortana Intelligence çözüm şablonu
## <a name="overview"></a>**Genel Bakış**
Çözüm şablonları tasarlanan E2E demo Cortana Intelligence Suite üstünde oluşturmanın tooaccelerate hello işlemi. Dağıtılan bir şablon gerekli Cortana Intelligence bileşen aboneliğinizle sağlamak ve hello arasında ilişkiler oluşturun. Bu ayrıca hello veri ardışık örnek verilerle bir veri benzetimi uygulamasından oluşturulan çekirdeğini oluşturur. Merhaba veri simulator sağlanan hello bağlantısından yükleyin ve yerel makinenize yükleyin, hello simulator kullanma yönergesi için toohello readme.txt dosyasına bakın. Merhaba simulator oluşturulan veri hello veri ardışık düzen ve ardından hello Power BI Panosu üzerinde canlandırılabilir machine learning tahmin oluşturma başlangıç hydrate.

Merhaba çözüm şablonu bulunabilir [burada](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

Merhaba dağıtım işlemi, çeşitli adımları tooset çözüm kimlik bilgileri size kılavuzluk yapacaktır. Bu kimlik bilgileri çözüm adı, kullanıcı adı ve parola hello dağıtım sırasında sağladığınız gibi kayıt emin olun.

Merhaba, bu belgenin tooexplain hello başvuru mimarisi ve aboneliğinizde Bu çözüm şablonu bir parçası olarak sağlanan farklı bileşenleri hedeftir. Merhaba belge nasıl tooreplace hello örnek verilerle kendi toobe mümkün toosee Öngörüler/tahminleri veri won sizden gerçek veri hakkında da alınmaktadır. Merhaba belge konuşmaları hello kendi verilerinizle toocustomize hello çözüm istiyorsanız değiştiren toobe gerekir çözüm şablonu hello bölümleri hakkında ek olarak. Merhaba sonunda nasıl toobuild hello Power BI panosuna Bu çözüm şablonu için yönergeler sağlanmaktadır.

## <a name="big-picture"></a>**Büyük resim**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Açıklanan mimarisi
Merhaba çözüm dağıtıldığında, çeşitli Azure hizmetlerine Cortana Analytics Suite içinde etkinleştirilir (*örn.* Olay hub'ı, akış analizi, Hdınsight, Data Factory, Machine Learning, *vb.*). Merhaba mimarisi diyagramı yukarıdaki hello talep tahmin enerji çözüm şablonu için baştan sona nasıl oluşturulur yüksek bir düzeyde gösterir. Çözüm şablonu diyagramı hello çözüm hello dağıtımı ile oluşturulan tıklayarak üzerlerinde bu hizmetleri hello mümkün tooinvestigate olacaktır. Aşağıdaki bölümlerde hello her parça açıklanmaktadır.

## <a name="data-source-and-ingestion"></a>**Veri kaynağı ve alım**
### <a name="synthetic-data-source"></a>Yapay veri kaynağı
Bu şablon hello verileri için kullanılan kaynak indirin ve yerel olarak başarılı dağıtım sonrasında çalıştırmak bir masaüstü uygulaması oluşturulur. Merhaba yönergeleri toodownload bulun ve enerji tahmin veri Simulator hello çözüm şablonu diyagramda adlı hello ilk düğümünü seçtiğinizde hello özellikleri çubuğunda bu uygulamayı yüklemek. Bu uygulama başlangıç akışları [Azure olay hub'ı](#azure-event-hub) hizmeti veri noktaları veya hello çözüm akışının hello kalan kullanılacak olan olayları ile.

yalnızca bilgisayarınızda yürütülürken Merhaba olay oluşturma uygulaması hello Azure olay hub'ı doldurur.

### <a name="azure-event-hub"></a>Azure Event hub'ı
Merhaba [Azure olay hub'ı](https://azure.microsoft.com/services/event-hubs/) hello alıcı hello giriş hello yukarıda açıklanan yapay veri kaynağı tarafından sağlanan bir hizmettir.

## <a name="data-preparation-and-analysis"></a>**Veri hazırlama ve çözümleme**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Merhaba [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) hizmetidir hello giriş akışından hello üzerinde gerçek zamanlı analiz yakın kullanılan tooprovide [Azure olay hub'ı](#azure-event-hub) üzerine sonuçlarını yayımlamak ve hizmeti bir [Power BI](https://powerbi.microsoft.com) Pano yanı sıra tüm ham gelen olayları toohello arşivleme [Azure Storage](https://azure.microsoft.com/services/storage/) daha sonra hello tarafından işlenmesi için service [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) hizmet.

### <a name="hd-insights-custom-aggregation"></a>HD Öngörüler özel toplama
Hello Azure HD Insight hizmeti olan kullanılan toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) (Azure Data Factory tarafından düzenlenmiş) komut dosyaları tooprovide toplamalar hello Azure Stream Analytics hizmeti kullanarak arşivlenmiş hello ham olayları.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Merhaba [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (Azure Data Factory tarafından düzenlenmiş) hizmeti kullanılır alınan hello girişleri verilen belirli bir bölgenin gelecekteki güç tüketiminin tahmin toomake.

## <a name="data-publishing"></a>**Verileri yayımlama**
### <a name="azure-sql-database-service"></a>Azure SQL veritabanı hizmeti
Merhaba [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/) hizmetidir hello hello tüketilen Azure Machine Learning hizmeti tarafından alınan (Azure Data Factory tarafından yönetilen) kullanılan toostore hello tahminleri [Power BI](https://powerbi.microsoft.com) Pano.

## <a name="data-consumption"></a>**Veri tüketim**
### <a name="power-bi"></a>Power BI
Merhaba [Power BI](https://powerbi.microsoft.com) hizmetidir kullanılan tooshow hello tarafından sağlanan toplamalar içeren bir Pano [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) isteğe bağlı yanı sıra hizmet tahmin depolanan sonuçlarına [Azure SQL Veritabanı](https://azure.microsoft.com/services/sql-database/) üretilen hello kullanarak [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) hizmet. Nasıl toobuild hello Power BI panosu için bu çözüm şablonu ile ilgili yönergeler için aşağıdaki toohello bölümüne bakın.

## <a name="how-toobring-in-your-own-data"></a>**Nasıl kendi verilerinizi toobring**
Nasıl toobring kendi veri tooAzure ve ne alanları gerektirecek hello veri değişiklikler için bu bölümde açıklanmıştır bu mimariye getirin.

Bu çözüm şablonu için kullanılan hello veri kümesi, Getir dataset eşleşir düşüktür. Verilerinizi ve gereksinimleri anlamanız nasıl bu şablonu toowork kendi verilerinizle değiştirmeniz çok önemli olacaktır. Bu, ilk Etkilenme toohello Azure Machine Learning hizmeti ise, hello örnekte kullanarak bir giriş tooit alabilirsiniz [nasıl toocreate ilk denemenizi](machine-learning/machine-learning-create-experiment.md).

Aşağıdaki bölümlerde hello yeni bir veri kümesi eklendiğinde değişiklikler gerektirir hello şablonu hello bölümlerini ele alınacaktır.

### <a name="azure-event-hub"></a>Azure Event hub'ı
Merhaba [Azure olay hub'ı](https://azure.microsoft.com/services/event-hubs/) hizmetidir çok genel sağlayacak şekilde veri toohello hub CSV veya JSON biçiminde gönderilebilir. Hiçbir özel işlem hello Azure olay hub'ı oluşur, ancak içine sat hello verileri anlamak önemlidir.

Bu belgede nasıl tooingest verilerinizi, ancak bir kolayca olayları ya da veri tooan Azure olay Hub'ı gönderebilirsiniz açıklanmamaktadır hello kullanarak [olay hub'ı API](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Merhaba [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) hizmetidir yakın gerçek zamanlı analiz kullanılan tooprovide veri akışlardan okuma ve veri kaynağı tooany sayısını çıktısı.

Merhaba talep tahmin enerji çözüm şablonu için her hello Azure Event Hub hizmetini olaylarından girdi olarak kullanma ve çıkışları tootwo ayrı konumlar sahip iki alt sorguları, hello Azure akış analizi sorgu oluşur. Bu çıktı, bir Power BI veri kümesi ve bir Azure depolama konumu oluşur.

Merhaba [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) sorgu tarafından bulunabilir:

* Merhaba oturum [Azure Yönetim Portalı](https://manage.windowsazure.com/)
* Merhaba akış analizi işleri bulma ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) hello çözüm dağıtıldığında oluşturuldu. Bir veri tooblob depolama (örneğin mytest1streaming432822asablob) gönderilmesi için olan ve diğer veri tooPower BI (örneğin mytest1streaming432822asapbi) gönderilmesi için biridir hello.
* Seçme

  * ***GİRİŞLERİ*** tooview hello sorgu giriş
  * ***Sorgu*** tooview hello sorgunun kendisini
  * ***ÇIKARIR*** tooview hello farklı çıkışları

Azure Stream Analytics sorgu oluşturma hakkında bilgi hello bulunabilir [Stream Analytics sorgu başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx) konusuna bakın.

Bu çözümde, Azure Stream Analytics işi, bir veri kümesi ile Merhaba gelen veri akışı tooa Power BI Panosu hakkında gerçek zamanlı analiz bilgi yakın Bu çözüm şablonu bir parçası olarak sağlanan çıkarır hello. Merhaba gelen veri biçimi hakkında örtük bilgiye olduğundan, bu sorguları değiştirilmiş toobe gerekir, veri biçimine bağlı.

Merhaba diğer Azure Stream Analytics işi tüm çıkarır [olay hub'ı](https://azure.microsoft.com/services/event-hubs/) olayları [Azure Storage](https://azure.microsoft.com/services/storage/) ve bu nedenle hello tam olay bilgilerini akışı gibi veri biçimi ne olursa olsun hiçbir değişikliğinin gerektirir toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Merhaba [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) hizmet hello taşıma ve verilerinin işlenmesini düzenler. Merhaba talep tahmin enerji çözüm şablonu hello veriler için Fabrika on iki yapılır [ardışık düzen](data-factory/data-factory-create-pipelines.md) taşımak ve işlem çeşitli teknolojiler kullanılarak hello veri.

  Veri fabrikanızın hello Data Factory düğümü hello çözüm hello dağıtımı ile oluşturulan hello çözüm şablonu diyagramı hello sonundaki açarak erişebilir. Bu, toohello veri fabrikası Azure yönetim portalınızdaki sürecek. Veri kümeleriniz altında hatalar görürseniz, hello veri Oluşturucusu başlatılmasından önce dağıtılan toodata Fabrika oldukları gibi bu yoksayabilirsiniz. Bu hata, veri fabrikası çalışmasını engellemez.

Bu bölümde hello gerektiği açıklanmaktadır [ardışık düzen](data-factory/data-factory-create-pipelines.md) ve [etkinlikleri](data-factory/data-factory-create-pipelines.md) hello bulunan [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Merhaba diyagram görünümü hello çözümün aşağıdadır.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Beş hello ardışık düzen Bu Factory içeren [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) kullanılan toopartition ve birleşik hello verileri betikler. Not ettiğiniz zaman hello betikleri hello bulunması [Azure Storage](https://azure.microsoft.com/services/storage/) hesabı Kurulum sırasında oluşturuldu. Konumlarına olacaktır: demandforecasting\\\\betik\\\\hive\\ \\ (veya https://[Your çözüm name].blob.core.windows.net/demandforecasting).

Benzer toohello [Azure akış analizi](#azure-stream-analytics-1) sorguları, [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) betikleri hello gelen veri biçimi hakkında örtük bilgiye sahip, bu sorguları değiştirilmiş toobe gerekir, veri biçimi ve bağlı[özellik Mühendisliği](machine-learning/machine-learning-feature-selection-and-engineering.md) gereksinimleri.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Bu [ardışık düzen](data-factory/data-factory-create-pipelines.md) ardışık düzen içeren tek bir etkinliğin - bir [Hdınsighthive](data-factory/data-factory-hive-activity.md) etkinliğini kullanarak bir [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) çalıştıran bir [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)betik tooaggregate hello 10 saniyede alt istasyon düzeyi toohourly bölge düzeyi isteğe bağlı veri akışı ve koyun [Azure Storage](https://azure.microsoft.com/services/storage/) hello Azure akış analizi işi.

[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) bölümleme bu görev için komut dosyası ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Bu [ardışık düzen](data-factory/data-factory-create-pipelines.md) iki etkinlik içerir:

* [Hdınsighthive](data-factory/data-factory-hive-activity.md) etkinliğini kullanarak bir [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) çalıştığında bir Hive betiği tooaggregate hello saatlik geçmiş talep verileri alt istasyon düzeyi toohourly bölge düzeyinde ve Azure hello sırasında Azure Depolama'da yerleştirme Akış analizi işi
* [Kopya](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello taşır etkinlik Azure Storage blobu toohello hello çözüm şablonu yüklemesinin bir parçası sağlanan bir Azure SQL veritabanı'ndan verileri toplanır.

Merhaba [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) bu görev için komut dosyası ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Bunlar [ardışık düzen](data-factory/data-factory-create-pipelines.md) çeşitli etkinlikleri içerir ve son sonucu hello tahminleri bu çözüm şablonuyla ilişkili hello Azure Machine Learning deneme gelen puanlanır. Bunlar, bunların her biri yalnızca hello ADF ardışık düzen ve hello hive betiğini her bölge için geçirilen farklı RegionID tarafından yapılır hello farklı bir bölgeye işleme dışında neredeyse aynıdır.  
Bu konuda yer alan hello etkinlikleri şunlardır:

* [Hdınsighthive](data-factory/data-factory-hive-activity.md) etkinliğini kullanarak bir [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) çalıştığında bir Hive betiği tooperform toplamalar ve özellik Mühendisliği hello Azure Machine Learning deneme için gerekli. Merhaba Hive betikler bu görev için ilgili ***PrepareMLInputRegionX.hql***.
* [Kopya](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello hello sonuçları taşır etkinlik [Hdınsighthive](data-factory/data-factory-hive-activity.md) hello erişiminin olabilecek etkinlik tooa tek Azure Storage blobu [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) etkinlik.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) hello sonuçları hello Azure Machine Learning deneme çağırır etkinlik sonuçları içinde tek bir Azure Storage blobu koyulmuş.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Bunlar [ardışık düzen](data-factory/data-factory-create-pipelines.md) tek bir etkinlik - içeren bir [kopya](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello Azure Machine Learning deneme hello sonuçlarını hello ilgili taşır etkinlik ***MLScoringRegionXPipeline *** toohello hello çözüm şablonu yüklemesinin bir parçası sağlanan bir Azure SQL veritabanı.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Bu [ardışık düzen](data-factory/data-factory-create-pipelines.md) tek bir etkinlik - içeren bir [kopya](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello taşır etkinlik toplanan devam eden talep verileri ***LoadHistoryDemandDataPipeline*** toohello Azure Merhaba çözüm şablonu yüklemesinin bir parçası sağlanan SQL veritabanı.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Bunlar [ardışık düzen](data-factory/data-factory-create-pipelines.md) tek bir etkinlik - içeren bir [kopyalama](https://msdn.microsoft.com/library/azure/dn835035.aspx) olan hello başvuru verileri alt istasyon/bölge/Topologygeo taşır etkinlik karşıya tooAzure depolama blobu hello çözümün bir parçası şablon yükleme toohello hello çözüm şablonu yüklemesinin bir parçası sağlanan bir Azure SQL veritabanı.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Merhaba [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) bölgesinin talebin hello tahmin Bu çözüm şablonu sağlar için kullanılan deneyin. Merhaba deneme belirli toohello veri tüketilen kümesidir ve bu nedenle duruma getirildikten değişiklik ya da değiştirme belirli toohello veri ister.

## <a name="monitor-progress"></a>**İlerlemeyi izleme**
Merhaba veri Oluşturucusu başlatıldıktan sonra hello ardışık düzen başlayan hydrated tooget ve hello farklı bileşenleri çözümünüzün Data Factory hello tarafından aşağıdaki hello komutlar eyleme oluşturan başlatın. Merhaba ardışık düzen izleyebilirsiniz iki yolu vardır.

1. Hello verileri Azure Blob depolama biriminden denetleyin.

    Merhaba Stream Analytics işi birini hello ham gelen veri tooblob depolama yazar. Üzerinde tıklatırsanız **Azure Blob Storage** hello çözümünüzden bileşeni başarıyla dağıtıldı hello çözüm ekran ve ardından **açık** hello sağ panelde, sizi toohello götürür[Azure Yönetim Portalı](https://portal.azure.com). Bir kez, tıklayın **BLOB'lar**. Merhaba sonraki panelinde kapsayıcıları listesini görürsünüz. Tıklayın **"energysadata"**. Merhaba sonraki panelinde hello görürsünüz **"demandongoing"** klasör. Hello rawdata klasörün içine tarihi gibi adlarla klasörleri göreceksiniz = 2016-01-28 vs. Bu klasörler görürseniz, hello ham verileri başarıyla olduğunu gösterir, bilgisayarınızda oluşturulan ve blob depolama alanına depolanır. Sınırlı boyutları bu klasörlerdeki MB olmalıdır dosyaların görmelisiniz.
2. Azure SQL veritabanından Hello veri denetleyin.

    Merhaba son adımı hello ardışık toowrite (örneğin tahminleri machine learning'in) SQL veritabanına verilerdir. SQL veritabanı'nda en fazla 2 saat hello veri tooappear için toowait olabilir. Tek yönlü toomonitor ne kadar veri SQL veritabanınız kullanılabilir aracılığıyladır [Azure Yönetim Portalı](https://manage.windowsazure.com/). SQL veritabanları Hello sol panelde bulun![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) ve tıklatın. Ardından, veritabanınızı (yani demo123456db) bulun ve tıklayın. Merhaba bir sonraki sayfada altında **"Bağlan tooyour veritabanı"** 'yi tıklatın **"SQL veritabanınız Çalıştır Transact-SQL sorguları"**.

    Burada, yeni bir sorgu ve hello sayıda satırı (örneğin "select count(*) DemandRealHourly gelen) için sorgu tıklatabilirsiniz" veritabanınızı büyüdükçe hello hello tablodaki satır sayısını artırmalısınız.)
3. Power BI panosuna Hello verilerden denetleyin.

    Power BI sık kullanılan yolu Pano toomonitor hello ham gelen verileri ayarlayabilirsiniz. Lütfen hello "Power BI panosuna" bölümü hello yönergesinde izleyin.

## <a name="power-bi-dashboard"></a>**Power BI Panosu**
### <a name="overview"></a>Genel Bakış
Bu bölümde tooset Power BI Panosu toovisualize Yukarı'nın düzgün olarak tahmin sonuçlarını olarak Azure gerçek zamanlı veri analizi (etkin yolu) nasıl akışı açıklanır Azure machine learning (yolunuzda).

### <a name="setup-hot-path-dashboard"></a>Kurulum etkin yolunuzda Panosu
Aşağıdaki adımları hello nasıl toovisualize gerçek zamanlı akış analizi hello çözüm dağıtım zamanında oluşturulan işleri çıktı verilerini size yol gösterecektir. A [çevrimiçi Power BI](http://www.powerbi.com/) aşağıdaki adımları gerekli tooperform hello hesabıdır. Bir hesabınız yoksa, şunları yapabilirsiniz [oluşturmak](https://powerbi.microsoft.com/pricing).

1. Power BI çıktı Azure akış analizi (ASA) ekleyin.

   * Toofollow hello yönergelerinde gerekir [Azure akış analizi & Power BI: veri akışı gerçek zamanlı görünürlük için gerçek zamanlı analiz Pano](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset hello çıktı Azure akış analizi işinin gücün olarak ayarlama BI Panosu.
   * Merhaba stream analytics işinde bulun, [Azure Yönetim Portalı](https://manage.windowsazure.com). Merhaba işinin Hello adı olmalıdır: YourSolutionName + "streamingjob" + rastgele sayı + "asapbi" (yani demostreamingjob123456asapbi).
   * Powerbı çıktı hello ASA işi için ekleyin. Set hello **çıkış diğer adları** olarak **'PBIoutput'**. Ayarlama, **veri kümesi adı** ve **tablo adı** olarak **'EnergyStreamData'**. Merhaba çıkış ekledikten sonra tıklatın **"Başlat"** hello altındaki hello sayfa toostart hello Stream Analytics işi. Bir onay iletisi almanız gerekir (*ör*, "Başlangıç akış analizi işi başarılı bir şekilde myteststreamingjob12345asablob").
2. Çok oturum[çevrimiçi Power BI](http://www.powerbi.com)

   * Çalışma Alanım'da sol paneli veri kümeleri bölüm hello üzerinde mümkün toosee Power BI, Sol paneldeki hello yeni bir veri kümesi gösteren olmalıdır. Azure Stream Analytics hello önceki adımda gönderilen veri akış hello budur.
   * Merhaba emin olun ***görselleştirmeleri*** bölmesi açılır ve Merhaba ekranında sağ tarafında gösterilir.
3. "İsteğe bağlı olarak zaman damgası" döşeme hello oluşturun:

   * Veri kümesi tıklatın **'EnergyStreamData'** Sol paneli veri kümeleri bölüm hello üzerinde.
   * Tıklatın **"Çizgi grafiği"** simgesi ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * 'EnergyStreamData' tıklayın **alanları** paneli.
   * Tıklatın **"Zaman damgası"** ve "Ekseni altında" gösterdiğinden emin olun. Tıklatın **"Yükle"** ve "Değerler" altında gösterdiğinden emin olun.
   * Tıklatın **KAYDETMEK** hello üst ve hello rapor "EnergyStreamDataReport" olarak adlandırın. "EnergyStreamDataReport" adlı hello raporu, sol taraftaki hello Gezgini bölmesinde raporları bölümünde gösterilir.
   * Tıklatın **"Pin Visual"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) simgesini ekranın sağ üst köşesinde bu çizgi grafiği, bir "Pin tooDashboard" penceresi gösterebilir, toochoose bir Pano. Lütfen "EnergyStreamDataReport" seçip "Pin"'i tıklatın.
   * Merhaba Panoda bu kutucuğu tıklayın "Düzenle" simgesine sağ üst köşedeki toochange başlığını "İsteğe bağlı olarak zaman damgası" olarak hello fare getirin
4. Uygun veri kümelerinin bağlı diğer Pano kutucukları oluşturun. Merhaba son Pano görünümü aşağıda gösterilmiştir.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Kurulum yolunuzda Panosu
Yolunuzda veri ardışık düzeninde hello temel tooget hello isteğe bağlı her bölge tahmin hedeftir. Power BI hello tahmin sonuçlarını depolandığı, veri kaynağı olarak tooan Azure SQL veritabanına bağlanır.

> [!NOTE]
> 1) İşlem birkaç saat toocollect hello Pano için yeterince tahmin sonuçlarını alır. 2-3 saat hello veri Oluşturucusu yemek sonra bu işlemi başlatmak öneririz. 2) toodownload ve yükleme hello ücretsiz yazılımlar Bu adımda hello önkoşuldur [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Merhaba veritabanı kimlik bilgileri alın.

   İhtiyacınız olacak **veritabanı sunucu adı, veritabanı adı, kullanıcı adı ve parola** toonext adımları geçmeden önce. Merhaba adımları tooguide İşte, nasıl toofind bunları.

   * Bir kez **"Azure SQL veritabanı"** çözüm şablonunuzda diyagramı yeşil bırakır, tıklatın ve ardından **"Açık"**. Veritabanı bilgileri sayfası da açılır ve Kılavuzlu tooAzure Yönetim Portalı olacaktır.
   * Merhaba sayfasında "Veritabanı" bölümünde bulabilirsiniz. Oluşturduğunuz hello veritabanını listeler. Veritabanınızın Hello adı olmalıdır **", çözüm adı rastgele sayı + 'db'"** (örneğin, "mytest12345db").
   * Pop paneli çıkışı, veritabanı sunucunuzun adını hello üstte bulabileceğiniz Yeni Merhaba, veritabanınızı'ı tıklatın. Veritabanı sunucusu adı olmalıdır **", çözüm adı rastgele sayı + 'database.windows.net,1433'"** (örneğin, "mytest12345.database.windows.net,1433").
   * Veritabanınızı **kullanıcıadı** ve **parola** aynı kullanıcı adı hello hello ve parola daha önce kaydedilen sırasında hello Çözüm dağıtımı.
2. Güncelleştirme hello hello yolunuzda Power BI dosyası veri kaynağı

   * Merhaba en son sürümünü yüklediğinizden emin olun [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * Merhaba, **"DemandForecastingDataGeneratorv1.0"** indirdiğiniz klasörü, çift tıklayarak hello **'Power BI Template\DemandForecastPowerBI.pbix'** dosya. Merhaba ilk görselleştirmeleri kukla verilere dayanır. **Not:** , massage, lütfen Power BI Desktop hello en son sürümünü yüklediğinizden emin olun bir hata görürsünüz.

     Merhaba dosya hello üstte, açtığınızda, tıklatın **'Sorguları Düzenle'**. Hello penceresindeki pop, çift tıklayarak **'Source'** hello sağ panelde.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * Hello penceresindeki pop, yerini **"Server"** ve **"Veritabanı"** kendi sunucu ve veritabanı adları ve ardından ile **"Tamam"**. Sunucu adı için başlangıç bağlantı noktası 1433 belirttiğinizden emin olun (**YourSolutionName.database.windows.net, 1433**). Merhaba ekranda görüntülenen hello uyarı iletilerini yoksayın.
   * Merhaba sonraki pop içinde penceresini hello sol bölmedeki iki seçenek görürsünüz (**Windows** ve **veritabanı**). Tıklatın **"Veritabanı"**, doldurun, **"Username"** ve **"Parola"** (Merhaba kullanıcı adı ve parola ilk hello çözümü dağıtılmış ve oluşturulan girdiğiniz budur bir Azure SQL veritabanı). İçinde ***, bu ayarların tooapply düzey seçin***, veritabanı düzeyi seçeneği işaretleyin. Ardından **"Bağlan"**.
   * Destekli geri toohello önceki sayfaya olduğunuzda hello penceresini kapatın. Bir ileti pop out - tıklatın **Uygula**. Son olarak, hello tıklatın **kaydetmek** düğmesini toosave hello değişiklikleri. Power BI dosyanızı şimdi bağlantı toohello sunucusu oluşturmuştur. Görselleştirmeleri boşken hello sağ üst köşesindeki hello göstergeler hello silme simgesini tıklatarak tüm hello veri hello görselleştirmeleri toovisualize hello seçimlere temizlediğinizden emin olun. Merhaba Yenile düğmesini tooreflect yeni verileri hello görselleştirmelerinde kullanın. Başlangıçta, Hello veri fabrikası zamanlanmış toorefresh 3 saatte olduğu gibi görsel öğeleri hello çekirdek verileri yalnızca görürsünüz. 3 saat sonra yeni tahminleri hello verilerini yenilediğinizde, görselleştirmeler yansıtılan görürsünüz.
3. (İsteğe bağlı) Merhaba yolunuzda Pano çok yayımlama[çevrimiçi Power BI](http://www.powerbi.com/). Bu adım bir Power BI hesabı (veya Office 365 hesabı) gerektiğini unutmayın.

   * Tıklatın **"Yayımla"** ve birkaç saniye sonra "tooPower BI başarı yayımlama!" görüntüleyen bir pencere görüntülenir Yeşil bir onay işareti ile. "Power bı'da Aç demoprediction.pbix" Merhaba bağlantıya tıklayın. toofind ayrıntılı yönergeler için bkz: [Power BI masaüstünden Yayımla](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate yeni bir Pano: hello tıklatın  **+**  sonraki toothe oturum **panolar** hello sol bölmedeki bölümü. Bu yeni bir Pano için "İsteğe bağlı tahmin Demo" Merhaba ad girin.
   * Merhaba raporu açtığınızda, tıklatın ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin tüm görselleştirmeler tooyour Pano. toofind ayrıntılı yönergeler için bkz: [bir raporundan döşeme tooa Power BI panosuna Sabitle](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Toohello Panosu sayfasına gidin ve hello boyutunu ve konumunu, görsel öğe ayarlamak ve bunların başlıklarını düzenleyin. toofind ayrıntılı yönergeler nasıl tooedit kutucuklarınız, bkz. [düzenleme Döşe--yeniden boyutlandırma, taşıma, yeniden adlandırma, PIN, Sil, köprü eklemek](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Burada, bazı yolunuzda sabitlenmiş görselleştirmeleri tooit içeren bir örnek Pano verilmiştir.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (İsteğe bağlı) Yenileme hello veri kaynağının zamanlayın.

   * Merhaba veri tooschedule yenileme üzerine gelin, fare hello **EnergyBPI son** dataset tıklatın ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) ve ardından **Yenileme zamanlaması**.
     **Not:** 'ı tıklatın, bir uyarı massage görürseniz **kimlik bilgilerini Düzenle** ve veritabanı kimlik bilgileri olan hello aynı 1. adımda açıklanan olarak emin olun.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Merhaba genişletin **Yenileme zamanlaması** bölümü. "Verilerinizi güncel tutmaya" etkinleştirin.
   * Gereksinimlerinize bağlı hello yenileme zamanlayın. toofind daha fazla bilgi için bkz: [veri yenileme Power BI'da](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Nasıl toodelete çözümünüzü**
Lütfen hello veri Oluşturucusu daha yüksek maliyetleri çalıştırmanın gibi hello çözüm aktif olarak kullanırken, hello veri Oluşturucusu Durdur emin olun. Lütfen bu kullanmıyorsanız hello çözüm silin. Çözümünüzü silinmesi hello çözüm dağıtıldığında, aboneliğinizde sağlanan tüm hello bileşenleri silinmesine neden olur. toodelete hello çözüm hello çözüm şablonu hello sol panelinde çözüm adına tıklayın ve üzerinde Sil'i tıklatın.

## <a name="cost-estimation-tools"></a>**Tahmin araçları maliyet**
Merhaba aşağıdaki iki araçları hello talep tahmin enerji çözüm şablonu için aboneliğinizde çalışır durumda söz konusu toplam maliyetleri daha iyi anlamak kullanılabilir toohelp şunlardır:

* [Microsoft Azure maliyetini tahmin Aracı (çevrimiçi)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure maliyetini tahmin Aracı (Masaüstü)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Katkıda Bulunanlar**
Bu makalede veri Bilimcisi Yijing Chen ve yazılım mühendisi Qiu Min Microsoft tarafından yazılmış.
