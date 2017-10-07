---
title: "Azure - Cortana Intelligence çözüm teknik Kılavuzu ile Havacılık aaaPredictive bakım | Microsoft Docs"
description: "Bir teknik Kılavuzu toohello çözüm şablonu Microsoft Cortana Intelligence ile Tahmine dayalı bakım Havacılık, yardımcı programlar ve taşıma için."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Tahmine dayalı bakım Havacılık ve diğer işletmeler için teknik Kılavuzu toohello Cortana Intelligence çözüm şablonu

## <a name="important"></a>**Önemli**
Bu makalede kullanım dışı bırakıldı. Merhaba bilgileri elinizdeki hala ilgili toohello sorun yani Tahmine dayalı bakım Havacılık, ancak hello toodate bilgi yukarı en son makaleyle hello bulunabilir [burada](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Katkıda Bulunanlar**
Bu makalede veri bilimcilerine Yan Zhang Gauher Shaheen, Fidan Boylu Uz ve Microsoft'taki Dan Grecoe yazılım mühendisi tarafından yazılmış.

## <a name="overview"></a>**Genel Bakış**
Çözüm şablonları tasarlanan E2E demo Cortana Intelligence Suite üstünde oluşturmanın tooaccelerate hello işlemi. Dağıtılan bir şablon gerekli Cortana Intelligence bileşenleri aboneliğinizle sağlamak ve aralarında hello ilişkiler oluşturun. Bu ayrıca hello veri ardışık, indirin ve hello çözüm şablonu dağıttıktan sonra yerel makinenize yükleyin veri Oluşturucu uygulamasından oluşturulan örnek verilerle çekirdeğini oluşturur. Merhaba üreticisinden oluşturulan hello veri hello veri ardışık hydrate ve ardından hello Power BI Panosu üzerinde canlandırılabilir machine learning tahminleri oluşturma başlatın. Merhaba dağıtım işlemi, çeşitli adımları tooset çözüm kimlik bilgileri size kılavuzluk yapacaktır. Bu kimlik bilgileri çözüm adı, kullanıcı adı ve parola hello dağıtım sırasında sağladığınız gibi kayıt emin olun.  

Merhaba, bu belgenin tooexplain hello başvuru mimarisi ve aboneliğinizde Bu çözüm şablonu bir parçası olarak sağlanan farklı bileşenleri hedeftir. Merhaba belge ayrıca ettiği hakkında tooreplace toobe mümkün toosee Öngörüler ve kendi verilerden tahminlerin gerçek verilerle örnek verileri. Ayrıca, hello belge hello kendi verilerinizle toocustomize hello çözüm istediyseniz değiştiren toobe gerekir çözüm şablonu bölümlerini açıklanır. Merhaba sonunda nasıl toobuild hello Power BI panosuna Bu çözüm şablonu için yönergeler sağlanmaktadır.

> [!TIP]
> Karşıdan yüklemek ve yazdırma bir [bu belgenin PDF sürümünü](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Büyük resim**
![Tahmine dayalı bakım mimarisi](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Merhaba çözüm dağıtıldığında, çeşitli Azure hizmetlerine Cortana Analytics Suite içinde etkinleştirilir (*örn.* Olay hub'ı, akış analizi, Hdınsight, Data Factory, Machine Learning, *vb.*). Merhaba mimarisi diyagramı yukarıdaki hello Havacılık çözüm şablonu için Tahmine dayalı bakım baştan sona nasıl oluşturulur yüksek bir düzeyde gösterir. Bu hizmetler üzerlerinde hello çözüm hello dağıtım Hdınsight hello özel olarak bu hizmet ile oluşturulan hello çözüm şablonu diyagramında tıklatarak hello azure Portalı'nda hello işlerken isteğe bağlı olarak sağlanan mümkün tooinvestigate olacaktır Ardışık etkinlikler gerekli toorun ve daha sonra silinir.
Karşıdan yükleyebileceğiniz bir [hello diyagramı tam boyutlu sürüm](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Aşağıdaki bölümlerde hello her parça açıklanmaktadır.

## <a name="data-source-and-ingestion"></a>**Veri kaynağı ve alım**
### <a name="synthetic-data-source"></a>Yapay veri kaynağı
Bu şablon hello verileri için kullanılan kaynak indirin ve yerel olarak başarılı dağıtım sonrasında çalıştırmak bir masaüstü uygulaması oluşturulur. Merhaba yönergeleri toodownload bulun ve Tahmine dayalı bakım veri Oluşturucusu hello çözüm şablonu diyagramda adlı hello ilk düğümünü seçtiğinizde hello özellikleri çubuğunda bu uygulamayı yüklemek. Bu uygulama başlangıç akışları [Azure olay hub'ı](#azure-event-hub) hizmeti veri noktaları veya hello çözüm akışının hello kalan kullanılacak olan olayları ile. Bu veri kaynağı oluşur veya genel kullanıma açık verilerden türetilmiş [NASA veri deposu](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) hello kullanarak [Turbofan Engine Bozulması benzetimi veri kümesi](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

yalnızca bilgisayarınızda yürütülürken Merhaba olay oluşturma uygulaması hello Azure olay hub'ı doldurur.

### <a name="azure-event-hub"></a>Azure event hub'ı
Merhaba [Azure olay hub'ı](https://azure.microsoft.com/services/event-hubs/) hello alıcı hello giriş hello yukarıda açıklanan yapay veri kaynağı tarafından sağlanan bir hizmettir.

## <a name="data-preparation-and-analysis"></a>**Veri hazırlama ve çözümleme**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Merhaba [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) hizmetidir hello giriş akışından hello üzerinde gerçek zamanlı analiz yakın kullanılan tooprovide [Azure olay hub'ı](#azure-event-hub) üzerine sonuçlarını yayımlamak ve hizmeti bir [Power BI](https://powerbi.microsoft.com) Pano yanı sıra tüm ham gelen olayları toohello arşivleme [Azure Storage](https://azure.microsoft.com/services/storage/) daha sonra hello tarafından işlenmesi için service [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) hizmet.

### <a name="hd-insights-custom-aggregation"></a>HD Öngörüler özel toplama
Hello Azure HD Insight hizmeti olan kullanılan toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) (Azure Data Factory tarafından düzenlenmiş) komut dosyaları tooprovide toplamalar hello Azure Stream Analytics hizmeti kullanarak arşivlenmiş hello ham olayları.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Merhaba [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (Azure Data Factory tarafından düzenlenmiş) hizmeti kullanılır toomake tahminleri kullanım ömrü (RUL) alınan hello girişleri verilen belirli uçak motorunun kalan hello üzerinde.

## <a name="data-publishing"></a>**Verileri yayımlama**
### <a name="azure-sql-database-service"></a>Azure SQL veritabanı hizmeti
Merhaba [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/) hizmetidir hello hello tüketilen Azure Machine Learning hizmeti tarafından alınan (Azure Data Factory tarafından yönetilen) kullanılan toostore hello tahminleri [Power BI](https://powerbi.microsoft.com) Pano.

## <a name="data-consumption"></a>**Veri tüketim**
### <a name="power-bi"></a>Power BI
Merhaba [Power BI](https://powerbi.microsoft.com) hizmetidir kullanılan tooshow toplamalar ve hello tarafından sağlanan uyarıları içeren bir Pano [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) depolanan RUL tahminleri yanı sıra hizmet [Azure SQL Veritabanı](https://azure.microsoft.com/services/sql-database/) üretilen hello kullanarak [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) hizmet. Nasıl toobuild hello Power BI panosu için bu çözüm şablonu ile ilgili yönergeler için aşağıdaki toohello bölümüne bakın.

## <a name="how-toobring-in-your-own-data"></a>**Nasıl kendi verilerinizi toobring**
Nasıl toobring kendi veri tooAzure ve ne alanları gerektirecek hello veri değişiklikler için bu bölümde açıklanmıştır bu mimariye getirin.

Getir dataset hello tarafından kullanılan hello dataset eşleşir düşüktür [Turbofan Engine Bozulması benzetimi veri kümesi](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) Bu çözüm şablonu için kullanılır. Verilerinizi ve gereksinimleri anlamanız nasıl bu şablonu toowork kendi verilerinizle değiştirmeniz çok önemli olacaktır. Bu, ilk Etkilenme toohello Azure Machine Learning hizmeti ise, hello örnekte kullanarak bir giriş tooit alabilirsiniz [nasıl toocreate ilk denemenizi](machine-learning-create-experiment.md).

Aşağıdaki bölümlerde hello yeni bir veri kümesi eklendiğinde değişiklikler gerektirir hello şablonu hello bölümlerini ele alınacaktır.

### <a name="azure-event-hub"></a>Azure Event hub'ı
Veri toohello hub CSV veya JSON biçiminde gönderilebilir şekilde hello Azure Event Hub hizmetini çok genel. Hiçbir özel işlem Azure olay hub'ı hello ancak içine sat hello verileri anlamak önemlidir gerçekleşir.

Bu belge nasıl tooingest verilerinizi, ancak kolayca olaylarını gönderebilir veya verileri tooan Azure olay hub'ı kullanarak, olay hub'ı API'nin hello açıklanmaz.

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello Azure Stream Analytics hizmeti, veri akışlardan okuma ve veri kaynağı tooany sayısını çıktısı yakın gerçek zamanlı analiz kullanılan tooprovide olur.

Hello Havacılık çözüm şablonu için Tahmine dayalı bakım için dört alt sorgularda, her kaybı olaylarından hello Azure Event Hub hizmetini ve dört farklı konumlara çıkışları sahip Azure akış analizi sorgu oluşur. Bu çıktı, üç Power BI veri kümeleri ve bir Azure depolama konumu oluşur.

Hello Azure akış analizi sorgu tarafından bulunabilir:

* Azure portal Hello günlüğe kaydetme
* Merhaba akış analizi işleri bulma ![Stream Analytics simgesi](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) hello çözüm dağıtıldığında oluşturuldu (*örneğin*, **maintenancesa02asapbi** ve **maintenancesa02asablob** Tahmine dayalı bakım çözümü için)
* Seçme
  
  * ***GİRİŞLERİ*** tooview hello sorgu giriş
  * ***Sorgu*** tooview hello sorgunun kendisini
  * ***ÇIKARIR*** tooview hello farklı çıkışları

Azure Stream Analytics sorgu oluşturma hakkında bilgi hello bulunabilir [Stream Analytics sorgu başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx) konusuna bakın.

Bu çözümde, bu çözüm şablonu bir parçası olarak sağlanan hello gelen veri akışı tooa Power BI Panosu hakkında gerçek zamanlı analiz bilgi yakın üç kümeleriyle hello sorguları çıktı. Merhaba gelen veri biçimi hakkında örtük bilgiye olduğundan, bu sorguları değiştirilmiş toobe gerekir, veri biçimine bağlı.

Merhaba ikinci akış analizi işi Hello sorguda **maintenancesa02asablob** yalnızca tüm çıkarır [olay hub'ı](https://azure.microsoft.com/services/event-hubs/) olayları [Azure Storage](https://azure.microsoft.com/services/storage/) ve bu nedenle hiçbir değişikliğinin gerektirir veri biçimi hello olarak bağımsız olarak tam olay bilgilerini toostorage akışı gerçekleştirilir.

### <a name="azure-data-factory"></a>Azure Data Factory
Merhaba [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) hizmet hello taşıma ve verilerinin işlenmesini düzenler. Tahmine dayalı bakım Havacılık çözüm şablonu hello veriler için Fabrika üç yapılır [ardışık düzen](../data-factory/data-factory-create-pipelines.md) taşımak ve işlem çeşitli teknolojiler kullanılarak hello veri.  Veri fabrikanızın hello hello Data Factory düğümü hello çözüm hello dağıtımı ile oluşturulan hello çözüm şablonu diyagramı hello sonundaki açarak erişebilir. Bu, toohello veri fabrikası Azure portalınızdaki sürecek. Veri kümeleriniz altında hatalar görürseniz, hello veri Oluşturucusu başlatılmasından önce dağıtılan toodata Fabrika oldukları gibi bu yoksayabilirsiniz. Bu hata, veri fabrikası çalışmasını engellemez.

![Data Factory veri kümesi hataları](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Bu bölümde hello gerektiği açıklanmaktadır [ardışık düzen](../data-factory/data-factory-create-pipelines.md) ve [etkinlikleri](../data-factory/data-factory-create-pipelines.md) hello bulunan [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Merhaba diyagram görünümü hello çözümün aşağıdadır.

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

İki hello ardışık düzen Bu Factory içeren [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) kullanılan toopartition ve birleşik hello verileri betikler. Not ettiğiniz zaman hello betikleri hello bulunması [Azure Storage](https://azure.microsoft.com/services/storage/) hesabı Kurulum sırasında oluşturuldu. Konumlarına olacaktır: maintenancesascript\\\\betik\\\\hive\\ \\ (veya https://[Your çözüm name].blob.core.windows.net/maintenancesascript).

Benzer toohello [Azure akış analizi](#azure-stream-analytics-1) sorguları, [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) betikleri hello gelen veri biçimi hakkında örtük bilgiye sahip, bu sorguları değiştirilmiş toobe gerekir, veri biçimi ve bağlı[özellik Mühendisliği](machine-learning-feature-selection-and-engineering.md) gereksinimleri.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Bu [ardışık düzen](../data-factory/data-factory-create-pipelines.md) - tek bir etkinlik içeren bir [Hdınsighthive](../data-factory/data-factory-hive-activity.md) etkinliğini kullanarak bir [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) çalıştıran bir [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) komut dosyası toopartition hello veri koyun [Azure Storage](https://azure.microsoft.com/services/storage/) sırasında [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) işi.

[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) bölümleme bu görev için komut dosyası ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Bu [ardışık düzen](../data-factory/data-factory-create-pipelines.md) çeşitli etkinlikleri ve son sonucu skoru hello tahminleri hello gelen olan içeren [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) Bu çözüm şablonuyla ilişkili deneme.

Bu konuda yer alan hello etkinlikleri şunlardır:

* [Hdınsighthive](../data-factory/data-factory-hive-activity.md) etkinliğini kullanarak bir [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) çalıştıran bir [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform toplamalar komut dosyası ve özellik Mühendisliği Merhaba gerekli [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) deneyin.
  [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) bölümleme bu görev için komut dosyası ***PrepareMLInput.hql***.
* [Kopya](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello sonuçlarından taşır etkinlik [Hdınsighthive](../data-factory/data-factory-hive-activity.md) etkinlik tooa tek [Azure Storage](https://azure.microsoft.com/services/storage/) tarafından erişim olabilir blob [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) etkinlik.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) hello çağırır etkinlik [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) tek bir koyulmuş hello sonuçlarında sonuçları deneme [Azure Storage](https://azure.microsoft.com/services/storage/) blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Bu [ardışık düzen](../data-factory/data-factory-create-pipelines.md) - tek bir etkinlik içeren bir [kopyalama](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello hello sonuçlarını taşır etkinlik [Azure Machine Learning](#azure-machine-learning) gelen denemeler *** MLScoringPipeline*** toohello [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/) çözüm şablonu yüklemesinin bir parçası sağlanan.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Merhaba [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) kullanılan deneme Bu çözüm şablonu sağlar için kalan kullanım ömrü (RUL) uçak motorunun hello. Merhaba deneme belirli toohello veri tüketilen kümesidir ve bu nedenle duruma getirildikten değişiklik ya da değiştirme belirli toohello veri ister.

Hello Azure Machine Learning deneme nasıl oluşturulduğu hakkında daha fazla bilgi için bkz: [Tahmine dayalı Bakım: adım 1 / 3, veri hazırlığı ve özellik Mühendisliği](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**İlerlemeyi izleme**
 Merhaba veri Oluşturucusu başlatıldıktan sonra hello ardışık düzen başlayan hydrated tooget ve hello farklı bileşenleri çözümünüzün Data Factory hello tarafından aşağıdaki hello komutlar eyleme oluşturan başlatın. Merhaba ardışık düzen izleyebilirsiniz iki yolu vardır.

1. Merhaba Stream Analytics işi birini hello ham gelen veri tooblob depolama yazar. Blob Storage bileşen çözümünüzün başlangıç ekranından, başarıyla dağıtılan hello çözüm tıklayın ve hello sağ panelde Aç'ı tıklatın, bu sizi toohello götürür [Yönetim Portalı](https://portal.azure.com/). Bir kez, BLOB'ları üzerinde tıklatın. Merhaba sonraki panelinde kapsayıcıları listesini görürsünüz. Tıklayın **maintenancesadata**. Merhaba sonraki panelinde hello görürsünüz **rawdata** klasör. Hello rawdata klasörün içinde saat gibi adlarla klasörleri göreceksiniz 17 = saat 18 vb. =. Bu klasörler görürseniz, hello ham verileri başarıyla olduğunu gösterir, bilgisayarınızda oluşturulan ve blob depolama alanına depolanır. Sınırlı boyutları bu klasörlerdeki MB olmalıdır csv dosyaları görmeniz gerekir.
2. Merhaba son adımı hello ardışık toowrite (örneğin tahminleri machine learning'in) SQL veritabanına verilerdir. SQL veritabanı'nda en fazla üç saat hello veri tooappear için toowait olabilir. Tek yönlü toomonitor ne kadar veri SQL veritabanınız kullanılabilir aracılığıyladır [azure portal](https://manage.windowsazure.com/). SQL veritabanları Hello sol panelde bulun ![SQL simgesi](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) ve tıklatın. Veritabanınızı bulun **pmaintenancedb** ve tıklayın. Hello sonraki sayfada hello altta, Yönet'i tıklatın
   
    ![Yönet simgesi](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    Burada, yeni bir sorgu ve hello sayıda satırı (örneğin select count(*) PMResult gelen) için sorgu tıklatabilirsiniz. Veritabanınızı büyüdükçe hello hello tablodaki satır sayısını artırmalısınız.

## <a name="power-bi-dashboard"></a>**Power BI Panosu**
### <a name="overview"></a>Genel Bakış
Bu bölümde nasıl tooset Power BI Panosu toovisualize yukarı toplu tahmin yanı sıra Azure akış analizi (etkin yolunuzda) gerçek zamanlı veri oluşur açıklanmaktadır Azure machine learning (yolunuzda).

### <a name="setup-cold-path-dashboard"></a>Kurulum yolunuzda Panosu
Uçuş (döngü) tamamlandığında hello yolunuzda veri ardışık düzeninde hello temel tooget her uçak motorunun Tahmine dayalı RUL (kalan kullanım ömrü) hedeftir. Merhaba tahmin sonucu 3 bir uçuş sırasında hello son 3 saat bitirdikten hello uçak motorları tahmin etmeye yönelik saatte bir güncelleştirilir.

Power BI tahmin sonuçlarını depolandığı, veri kaynağı olarak tooan Azure SQL veritabanına bağlanır. Not: çözümünüzü dağıtma 1) üzerinde gerçek tahmin hello veritabanında 3 saat içinde görünecektir.
Böylece hemen hello Power BI panosu oluşturabilir hello Oluşturucu indirme ile birlikte gelen hello pbıx dosyası bazı çekirdek verileri içerir. 2) toodownload ve yükleme hello ücretsiz yazılımlar Bu adımda hello önkoşuldur [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Merhaba aşağıdaki adımlar, hello çalışmaya verileri içeren çözüm dağıtımı hello aynı anda başlar SQL veritabanı tooconnect hello pbıx nasıl dosya üzerinde yardımcı olur (*örneğin*. Tahmin sonuçlarını) görselleştirme için.

1. Merhaba veritabanı kimlik bilgileri alın.
   
   İhtiyacınız vardır **veritabanı sunucu adı, veritabanı adı, kullanıcı adı ve parola** toonext adımları geçmeden önce. Merhaba adımları tooguide İşte, nasıl toofind bunları.
   
   * Bir kez **'Azure SQL Database'** çözüm şablonunuzda diyagramı yeşil bırakır, tıklatın ve ardından **'Açık'**.
   * Yeni bir tarayıcı sekmesi/hello Azure portal sayfası görüntüleyen pencere görürsünüz. Tıklatın **'Kaynak grubu'** hello Sol paneldeki.
   * Merhaba çözümü dağıtmak için kullandığınız hello aboneliği seçin ve ardından **' YourSolutionName\_ResourceGroup'**.
   * Hello Hello yeni pop içinde paneli çıkışı,'ı tıklatın ![SQL simgesi](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) simgesi tooaccess veritabanınızı. Veritabanı adınız sonraki toohello bu simgedir (*örneğin*, **'pmaintenancedb'**) ve hello **veritabanı sunucusu adı** sunucu adı özelliği hello altında listelenen ve görünmelidir benzer çok**YourSoutionName.database.windows.net**.
   * Veritabanınızı **kullanıcıadı** ve **parola** aynı kullanıcı adı hello hello ve parola daha önce kaydedilen sırasında hello Çözüm dağıtımı.
2. Merhaba yolunuzda rapor dosyasının Hello veri kaynağını Power BI Desktop ile güncelleştirin.
   
   * İndirdiğiniz ve oluşturucu dosya unzipped PC'nizde Hello klasörde çift **Powerbı\\PredictiveMaintenanceAerospace.pbix** dosya. Merhaba dosyayı açtığınızda herhangi bir uyarı iletisi görürseniz, bunları yoksay. Merhaba dosya Hello üstte tıklatın **'Sorguları Düzenle'**.
     
     ![Sorguları düzenleme](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * İki tablo görürsünüz **RemainingUsefulLife** ve **PMResult**. Merhaba ilk tabloyu seçin ve ![sorgu ayarlar simgesine](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) sonraki çok**'Source'** altında **'UYGULANAN adımları'** hello sağ üzerinde **'Sorgu ayarları'**Masası. Görünen herhangi bir uyarı iletisi yoksay.
   * Hello penceresindeki pop, yerini **'Server'** ve **'Database'** kendi sunucu ve veritabanı adları ve ardından ile **'Tamam'**. Sunucu adı için başlangıç bağlantı noktası 1433 belirttiğinizden emin olun (**YourSoutionName.database.windows.net, 1433**). Merhaba veritabanı alanı olarak bırakın **pmaintenancedb**. Merhaba ekranda görüntülenen hello uyarı iletilerini yoksayın.
   * Merhaba sonraki pop içinde penceresini hello sol bölmedeki iki seçenek görürsünüz (**Windows** ve **veritabanı**). Tıklatın **'Database'**, doldurun, **'Username'** ve **'Parola'** (Merhaba kullanıcı adı ve parola ilk hello çözümü dağıtılmış ve oluşturulan girdiğiniz budur bir Azure SQL veritabanı). İçinde ***, bu ayarların tooapply düzey seçin***, veritabanı düzeyi seçeneği işaretleyin. Ardından **'Bağlan'**.
   * Merhaba ikinci tabloda tıklatın **PMResult** ardından ![Gezinti simgesi](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) sonraki çok**'Source'** altında **'UYGULANAN adımları'** hello sağ üzerinde **'Sorgu ayarları'** panelde, hello server ve veritabanı adları hello adımları üstünde olduğu gibi güncelleştirme ve Tamam'ı tıklatın.
   * Destekli geri toohello önceki sayfaya olduğunuzda hello penceresini kapatın. Bir ileti pop out - tıklatın **Uygula**. Son olarak, hello tıklatın **kaydetmek** düğmesini toosave hello değişiklikleri. Power BI dosyanızı şimdi bağlantı toohello sunucusu oluşturmuştur. Görselleştirmeleri boşken hello sağ üst köşesindeki hello göstergeler hello silme simgesini tıklatarak tüm hello veri hello görselleştirmeleri toovisualize hello seçimlere temizlediğinizden emin olun. Merhaba Yenile düğmesini tooreflect yeni verileri hello görselleştirmelerinde kullanın. Başlangıçta, Hello veri fabrikası zamanlanmış toorefresh 3 saatte olduğu gibi görsel öğeleri hello çekirdek verileri yalnızca görürsünüz. 3 saat sonra yeni tahminleri hello verilerini yenilediğinizde, görselleştirmeler yansıtılan görürsünüz.
3. (İsteğe bağlı) Merhaba yolunuzda Pano çok yayımlama[çevrimiçi Power BI](http://www.powerbi.com/). Bu adım bir Power BI hesabı (veya Office 365 hesabı) gerektiğini unutmayın.
   
   * Tıklatın **'Yayımla'** ve birkaç saniye sonra "tooPower BI başarı yayımlama!" görüntüleyen bir pencere görüntülenir Yeşil bir onay işareti ile. "Açık PredictiveMaintenanceAerospace.pbix Power BI'da" Merhaba bağlantıya tıklayın. toofind ayrıntılı yönergeler için bkz: [Power BI masaüstünden Yayımla](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate yeni bir Pano: hello tıklatın  **+**  sonraki toothe oturum **panolar** hello sol bölmedeki bölümü. Bu yeni bir Pano için "Tahmine dayalı bakım Demo" Merhaba ad girin.
   * Merhaba raporu açtığınızda, tıklatın ![sabitleme simgesine](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin tüm görselleştirmeler tooyour Pano. toofind ayrıntılı yönergeler için bkz: [bir raporundan döşeme tooa Power BI panosuna Sabitle](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Toohello Panosu sayfasına gidin ve hello boyutunu ve konumunu, görsel öğe ayarlamak ve bunların başlıklarını düzenleyin. toofind ayrıntılı yönergeler nasıl tooedit kutucuklarınız, bkz. [düzenleme Döşe--yeniden boyutlandırma, taşıma, yeniden adlandırma, PIN, Sil, köprü eklemek](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Burada, bazı yolunuzda sabitlenmiş görselleştirmeleri tooit içeren bir örnek Pano verilmiştir.  Veri Oluşturucusu ne kadar süreyle çalıştırdığınız bağlı olarak numaralarınızı hello görselleştirmeleri üzerinde farklı olabilir.
     <br/>
     ![Son görünümü](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * Merhaba veri tooschedule yenileme üzerine gelin, fare hello **PredictiveMaintenanceAerospace** dataset tıklatın ![elips simgesi](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) ve ardından **Yenileme zamanlaması**.
     <br/>
     **Not:** 'ı tıklatın, bir uyarı massage görürseniz **kimlik bilgilerini Düzenle** ve veritabanı kimlik bilgileri olan hello aynı 1. adımda açıklanan olarak emin olun.
     <br/>
     ![Yenileme zamanlaması](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Merhaba genişletin **Yenileme zamanlaması** bölümü. "Verilerinizi güncel tutmaya" etkinleştirin.
     <br/>
   * Gereksinimlerinize bağlı hello yenileme zamanlayın. toofind daha fazla bilgi için bkz: [veri yenileme Power BI'da](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Kurulum etkin yolunuzda Panosu
Aşağıdaki adımları hello nasıl toovisualize gerçek zamanlı akış analizi hello çözüm dağıtım zamanında oluşturulan işleri çıktı verilerini size yol gösterecektir. A [çevrimiçi Power BI](http://www.powerbi.com/) aşağıdaki adımları gerekli tooperform hello hesabıdır. Bir hesabınız yoksa, şunları yapabilirsiniz [oluşturmak](https://powerbi.microsoft.com/pricing).

1. Power BI çıktı Azure akış analizi (ASA) ekleyin.
   
   * Toofollow hello yönergelerinde gerekir [Azure akış analizi & Power BI: veri akışı gerçek zamanlı görünürlük için gerçek zamanlı analiz Pano](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset hello çıktı Azure akış analizi işinin gücün olarak ayarlama BI Panosu.
   * Merhaba ASA sorgusu var olan üç çıkışları **aircraftmonitor**, **aircraftalert**, ve **flightsbyhour**. Merhaba sorgu, sorgu sekmesinde tıklayarak görüntüleyebilirsiniz. Karşılık gelen tooeach bu tablolar tooadd bir çıktı tooASA gerekir. Merhaba ilk çıkış eklediğinizde (*örneğin* **aircraftmonitor**) emin hello olun **çıkış diğer adları**, **veri kümesi adı** ve  **Tablo adı** olan, hello aynı (**aircraftmonitor**). Yineleme başlangıç adımları tooadd çıkarır **aircraftalert**, ve **flightsbyhour**. Tüm üç çıktı tablolarında ve hello ASA iş başlatıldı ekledikten sonra bir onay iletisi almanız gerekir (*ör*, "Başlangıç Stream Analytics işi başarılı bir şekilde maintenancesa02asapbi").
2. Çok oturum[çevrimiçi Power BI](http://www.powerbi.com)
   
   * Çalışma Alanım'da, sol panelinde veri kümeleri bölüm hello üzerinde ***DATASET*** adları **aircraftmonitor**, **aircraftalert**, ve **flightsbyhour**görünmelidir. Merhaba önceki step.hello kümesinde Azure akış analizi gönderilen veri akış hello budur **flightsbyhour** hello görüntülenmeyebilir diğer iki veri kümesi hello SQL sorgusu toohello doğası nedeniyle hello gibi aynı saat . Ancak, bunu bir saat sonra gösterilmesi gerekir.
   * Merhaba emin olun ***görselleştirmeleri*** bölmesi açılır ve Merhaba ekranında sağ tarafında gösterilir.
3. Power BI'da akan hello veri olduktan sonra veri akış hello görselleştirme başlatabilirsiniz. Bazı etkin yolunuzda görselleştirmeleri içeren bir örnek Pano tooit sabitlenmiş aşağıdadır. Uygun veri kümelerinin bağlı diğer Pano kutucukları oluşturabilirsiniz. Veri Oluşturucusu ne kadar süreyle çalıştırdığınız bağlı olarak numaralarınızı hello görselleştirmeleri üzerinde farklı olabilir.

    ![Pano görünümü](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. İşte bazı adımları toocreate hello döşeme yukarıdaki – birini hello "algılayıcı 11 vs yakıt görünümü. Eşik 48,26" döşeme:
   
   * Veri kümesi tıklatın **aircraftmonitor** Sol paneli veri kümeleri bölüm hello üzerinde.
   * Merhaba tıklatın **çizgi grafiği** simgesi.
   * Tıklatın **işlenen** hello içinde **alanları** olan "Ekseni altında" hello gösterecek şekilde bölmesinde **görselleştirmeleri** bölmesi.
   * "S11"'i tıklatın ve "s11\_uyarı" böylece her ikisi de "Değerler" altında görünür. Merhaba küçük sonraki çok oku**s11** ve **s11\_uyarı**, "Sum" Değiştir "Ortalama" çok.
   * Tıklatın **KAYDETMEK** hello üst ve "aircraftmonitor" Merhaba rapor adı. "Aircraftmonitor" adlı raporu hello gösterilecek **raporları** hello bölümünde **Gezgini** hello sol bölmesinde.
   * Merhaba tıklatın **PIN Visual** hello sağ üst köşesinde bu çizgi grafiği simgesine. Bir "Pin tooDashboard" penceresi sizin için bir panoyu seçin görünebilirler. "Tahmine dayalı bakım Demo" seçip "Pin"'i tıklatın.
   * Merhaba fare hello Panoda bu kutucuğu üzerine gelerek, hello "Düzenle" Merhaba sağ üst köşedeki toochange başlığını çok simgesine "algılayıcı 11, Donanma görünüm vs. Eşik 48,26" ve altyazısı çok"ortalama zaman içinde Donanma arasında".

## <a name="how-toodelete-your-solution"></a>**Nasıl toodelete çözümünüzü**
Lütfen hello veri Oluşturucusu daha yüksek maliyetleri çalıştırmanın gibi hello çözüm aktif olarak kullanırken, hello veri Oluşturucusu Durdur emin olun. Lütfen bu kullanmıyorsanız hello çözüm silin. Çözümünüzü silinmesi hello çözüm dağıtıldığında, aboneliğinizde sağlanan tüm hello bileşenleri silinmesine neden olur. toodelete hello çözüm hello çözüm şablonu hello sol panelinde çözüm adına tıklayın ve üzerinde Sil'i tıklatın.

## <a name="cost-estimation-tools"></a>**Maliyet tahmini araçları**
Merhaba aşağıdaki iki araçları hello Tahmine dayalı bakım Havacılık çözüm şablonu için aboneliğinizde çalışır durumda söz konusu toplam maliyetleri daha iyi anlamak kullanılabilir toohelp şunlardır:

* [Microsoft Azure maliyetini tahmin Aracı (çevrimiçi)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure maliyetini tahmin Aracı (Masaüstü)](http://www.microsoft.com/download/details.aspx?id=43376)

