---
title: "aaaDeep dalın içine araç durumu tahmin etmek ve alışkanlık - Azure yürüten | Microsoft Docs"
description: "Yürüten alışkanlıklarınıza ve araç sistem durumunu Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler Hello özelliklerini kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Araç telemetri analizi çözüm playbook: hello çözüm derinlemesine bakış
Bu **menü** bu playbook toohello bölümlerine bağlantılar: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Bu bölümde kümede ayrıntısına gider her hello çözüm mimarisi yönergeleri ve özelleştirme işaretçileri gösterilen hello aşamaları. 

## <a name="data-sources"></a>Veri Kaynakları
Merhaba çözüm iki farklı veri kaynakları kullanır:

* **Benzetimli araç sinyalleri ve tanılama veri kümesi** ve 
* **araç Kataloğu**

Bir araç telematik simulator bu çözümün bir parçası olarak dahil edilir. Tanılama bilgisi yayar ve karşılık gelen toohello durumu hello araç ve düzeni, zaman içinde belirli bir anda yürüten toohello işaret eder. Tıklatın [araç telematik Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **araç telematik Simulator Visual Studio çözümü** gereksinimlerinize göre özelleştirmeler. Merhaba araç katalog Toplamıdır toomodel eşleme ile bir başvuru veri kümesi içerir.

![Araç telematik simulator](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Şekil 1 – araç telematik Simulator*

Bu şema aşağıdaki hello içeren bir JSON olarak biçimlendirilmiş bir veri kümesi olur.

| Sütun | Açıklama | Değerler |
| --- | --- | --- |
| TOPLAMIDIR |Rastgele oluşturulan araç kimlik numarası |Bu ana 10.000 rastgele oluşturulmuş araç kimlik numaraları listesinden elde edilir. |
| Dış sıcaklığı |Merhaba hello araç burada yürüten sıcaklık dışında |0-100 arasında rastgele oluşturulmuş bir sayıya |
| Altyapısı sıcaklık |Merhaba altyapısı hello araç sıcaklığını |0-500 arasında rastgele oluşturulmuş sayı |
| Hız |araç hangi hello yürüten hello altyapısı hızı |0-100 arasında rastgele oluşturulmuş bir sayıya |
| Yakıt |Merhaba araç Hello yakıt düzeyi |Rastgele oluşturulmuş bir sayıya 0-100 (yakıt düzeyi yüzdesi gösterir) |
| EngineOil |Merhaba araç Hello altyapısı Petrol düzeyi |Rastgele oluşturulmuş bir sayıya 0-100 (altyapısı Petrol düzeyi yüzdesi gösterir) |
| Lastiği baskısı |Merhaba lastiği baskısı hello araç |Rastgele oluşturulan numarası 0-50'den (lastiği baskısı düzeyi yüzdesi gösterir) |
| Kilometre Sayacı |Merhaba araç Hello Kilometre Sayacı okunması |0-200000 arasında rastgele oluşturulmuş sayı |
| Accelerator_pedal_position |Merhaba Hızlandırıcı pedal konumunu hello araç |Rastgele oluşturulmuş bir sayıya 0-100 (Hızlandırıcı düzeyi yüzdesi gösterir) |
| Parking_brake_status |Merhaba araç veya yerleşmiş durumdayken gösterir |TRUE veya False |
| Headlamp_status |Burada hello ön ışık üzerinde olup olmadığını gösterir |TRUE veya False |
| Brake_pedal_status |Merhaba Fren pedal veya basılı olup olmadığını gösterir |TRUE veya False |
| Transmission_gear_position |Merhaba araç Hello iletim dişli konumu |Durumları: ilk olarak, üçüncü, dördüncü beşinci, altıncı seventh, sekizinci ikinci |
| Ignition_status |Merhaba araç çalışıyor veya durdurulmuştur olup olmadığını gösterir |TRUE veya False |
| Windshield_wiper_status |Merhaba ön wiper veya açık olup olmadığını gösterir |TRUE veya False |
| ABS |ABS veya bağlı olup olmadığını gösterir |TRUE veya False |
| zaman damgası |Merhaba veri noktası oluşturulduğunda hello zaman damgası |Tarih |
| Şehir |Merhaba araç Hello konumu |Bu çözümdeki 4 Şehir: Bellevue, Redmond, Sammamish, Seattle |

Merhaba araç model başvuru dataset Toplamıdır toohello modeli eşleme içerir. 

| TOPLAMIDIR | modeli |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Sedan |
| 8J0U8XCPRGW4Z3NQE |Karma |
| WORG68Z2PLTNZDBI7 |Aile Saloon |
| JTHMYHQTEPP4WBMRN |Sedan |
| W9FTHG27LZN1YWO0Y |Karma |
| MHTP9N792PHK08WJM |Aile Saloon |
| EI4QXI2AXVQQING4I |Sedan |
| 5KKR2VB4WHQH97PF8 |Karma |
| W9NSZ423XZHAONYXB |Aile Saloon |
| 26WJSGHX4MA5ROHNL |Dönüştürülebilir |
| GHLUB6ONKMOSI7E77 |İstasyon Wagon |
| 9C2RHVRVLMEJDBXLP |Küçük otomobil |
| BRNHVMZOUJ6EOCP32 |Küçük SUV |
| VCYVW0WUZNBTM594J |Spor araba |
| HNVCE6YFZSA5M82NY |Orta SUV |
| 4R30FOR7NUOBL05GJ |İstasyon Wagon |
| WYNIIY42VKV6OQS1J |Büyük SUV |
| 8Y5QKG27QET1RBK7I |Büyük SUV |
| DF6OX2WSRA6511BVG |Coupe |
| Z2EOZWZBXAEW3E60T |Sedan |
| M4TV6IEALD5QDS3IR |Karma |
| VHRA1Y2TGTA84F00H |Aile Saloon |
| R0JAUHT1L1R3BIKI0 |Sedan |
| 9230C202Z60XX84AU |Karma |
| T8DNDN5UDCWL7M72H |Aile Saloon |
| 4WPYRUZII5YV7YA42 |Sedan |
| D1ZVY26UV2BFGHZNO |Karma |
| XUF99EW9OIQOMV7Q7 |Aile Saloon |
| 8OMCL3LGI7XNCC21U |Dönüştürülebilir |
| ……. | |

### <a name="references"></a>Başvurular
[Araç telematik Simulator Visual Studio çözümü](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Azure Event hub'ı](https://azure.microsoft.com/services/event-hubs/)

[Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Alım
Azure Event Hubs, Stream Analytics ve Data Factory birleşimleridir çevrelerini tooingest hello araç sinyalleri hello tanılama olayları ve gerçek zamanlı ve toplu analizi. Tüm bu bileşenlerin oluşturulur ve hello çözüm dağıtımının bir parçası yapılandırılmış. 

### <a name="real-time-analysis"></a>Gerçek zamanlı analiz
Merhaba araç telematik Simulator hello tarafından oluşturulan olayları yayımlanan toohello olay hub'ı kullanarak hello olay hub'ı SDK. Merhaba Stream Analytics işi hello olay hub'ı bu olayları alır ve işlemleri gerçek zamanlı tooanalyze hello araç sistem durumu verileri hello. 

![Olay hub'ı Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Şekil 4 - Event Hub Panosu*

![Veriler işlenirken Analytics iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Şekil 5 - Stream Analytics işi veri işleme*

Merhaba Stream Analytics işi;

* Merhaba Event Hub'ndan verileri alır 
* bir birleştirme hello başvuru veri toomap hello araç Toplamıdır toohello karşılık gelen modeli gerçekleştirir 
* bunları zengin toplu analiz için Azure blob depolama alanına devam ettirir. 

Stream Analytics sorgu aşağıdaki hello kullanılan toopersist hello veriler Azure blob depolama alanına bağlıdır. 

![Akış analizi işi sorgu veri alımı için](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Şekil 6 - Stream Analytics işi veri alımı için sorgu*

### <a name="batch-analysis"></a>Toplu iş analiz
Biz de benzetimli araç sinyalleri ve tanılama veri kümesi daha zengin toplu analizi için ek bir birim oluşturduğunu. Gerekli tooensure toplu işlem için iyi temsili veri birimi budur. Bu amaçla hello Azure Data Factory iş akışı toogenerate "PrepareSampleDataPipeline" adlı işlem hattını kullanıyoruz bir yılın tutarında benzetimli araç sinyalleri ve tanılama veri kümesi. Tıklatın [Data Factory özel etkinlik](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory özel DotNet etkinlik özelleştirmeleri için Visual Studio çözümü gereksinimlerinize göre tabanlı. 

![Toplu iş akışı işleme için örnek verileri hazırlama](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Şekil 7 - toplu işleme iş akışı için örnek verileri hazırlama*

Merhaba ardışık düzen oluşur özel bir ADF .net etkinliği, burada göster:

![PrepareSampleDataPipeline etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Şekil 8 - PrepareSampleDataPipeline*

Merhaba ardışık düzen başarıyla yürütür ve "RawCarEventsTable" veri kümesi "Hazır", yıllık değerinde benzetimli araç sinyaller ve tanılama işaretlenmiş sonra veri üretilir. Merhaba aşağıdakilere bakın klasör ve dosya depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan:

![PrepareSampleDataPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Şekil 9 - PrepareSampleDataPipeline çıkış*

### <a name="references"></a>Başvurular
[Akış alımı için Azure olay hub'ı SDK](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Azure Data Factory veri taşıma özellikleri](../data-factory/data-factory-data-movement-activities.md)
[Azure veri fabrikası DotNet etkinliği](../data-factory/data-factory-use-custom-activities.md)

[Örnek verileri hazırlama için azure veri fabrikası DotNet etkinlik visual studio çözümü](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Bölüm hello veri kümesi
Merhaba ham yarı yapılandırılmış araç sinyalleri ve tanılama veri kümesi yıl/ay biçimine hello veri hazırlık adımı bölümlenir. Bu bölümleme daha verimli sorgulama yükseltir ve hataya üzerinden bir blob hesap toohello gelen hello ilk hesap olarak sonraki etkinleştirerek ölçeklenebilir uzun vadeli depolama dolar. 

>[!NOTE] 
>Bu adım hello çözümüne uygulanabilir yalnızca toobatch işleme bağlıdır.

Giriş ve çıkış veri veri yönetimi:

* Merhaba **çıktı verilerini** (etiketli *PartitionedCarEventsTable*) toobe uzun bir süre için veri hello Müşteri'nin "Data Lake" Merhaba temel / "rawest" form olarak tutulur. 
* Merhaba **giriş verileri** toothis ardışık düzen genellikle atılmasını gerektirebilir gibi hello çıktı verileri içeren tam uygunluğunu toohello giriş - yalnızca (sonraki kullanım için daha iyi bölümlenmiş) depolanır.

![Bölüm araba olayları iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Şekil 10 – bölüm araba olayları iş akışı*

Hdınsight Hive etkinliği "PartitionCarEventsPipeline içinde" kullanarak Hello ham verileri bölümlenen. Merhaba örnek verileri bir yıl için 1. adımda oluşturulan yıl/AYA göre bölümlenmiş. Merhaba kullanılan toogenerate araç sinyalleri ve tanılama verilerini her ay yılın (toplam 12 bölümler) bölümlerdir. 

![PartitionCarEventsPipeline etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Şekil 11 - PartitionCarEventsPipeline*

***PartitionConnectedCarEvents Hive betiği***

Merhaba "partitioncarevents.hql" adlı aşağıdaki Hive betiğini bölümleme için kullanılır ve hello "\demo\src\connectedcar\scripts" klasöründe hello indirilen ZIP bulunur. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.

![Bölümlenmiş çıktı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Şekil 12 - bölümlenmiş çıktı*

Merhaba veri artık iyileştirilmiş, daha yönetilebilir ve toogain zengin toplu Öngörüler işlenmesi için hazırdır. 

## <a name="data-analysis"></a>Veri analizi
Bu bölümde, nasıl toocombine Azure akış analizi, Azure Machine Learning, Azure Data Factory ve Azure Hdınsight zengin için Gelişmiş bkz araç sistem durumu ve yürüten alışkanlıklarınıza. Burada üç alt bölümleri şunlardır:

1. **Machine Learning**: Bu alt bölümde Bakım ve toosafety sorunları nedeniyle geri çekme gerektiren taşıtlardan bakım gerektiren bu çözüm toopredict taşıtlardan içinde kullanmış hello anomali algılama deneme ilgili bilgiler içerir.
2. **Gerçek zamanlı analiz**: Bu alt bölümde hello Stream Analytics sorgu dili kullanarak ve hello machine learning faaliyete geçirmeye yönelik ilgili hello gerçek zamanlı analiz denemesini özel bir uygulama kullanarak gerçek zamanlı bilgiler içerir.
3. **Toplu analiz**: Bu alt bölümde dönüştürme ve Azure Hdınsight ve Azure Machine Learning Azure Data Factory tarafından kullanıma hazır hale getirilmiş kullanarak hello toplu veri işleme hello ilgili bilgiler içerir.

### <a name="machine-learning"></a>Machine Learning
Amacımız burada Bakım veya belirli sistem durumu istatistiklerine bağlı geri çağırma gerektiren toopredict hello taşıtlardan ' dir. Varsayımlar aşağıdaki hello vermiyoruz

* Aşağıdaki üç koşul hello biri doğruysa hello taşıtlardan gerektiren **bakım Bakım**:
  
  * Lastiği baskısı düşük
  * Altyapısı Petrol düzeyinin düşük
  * Altyapısı sıcaklık yüksek
* Aşağıdaki koşullar hello biri doğruysa hello taşıtlardan olabilir bir **güvenlik sorunu** ve gerektiren **geri çağırma**:
  
  * Altyapısı sıcaklık yüksek olduğu, ancak dış sıcaklığı düşük
  * Altyapısı sıcaklık düşük olduğu, ancak dış sıcaklığı yüksek

Merhaba önceki gereksinimlerine bağlı olarak, iki ayrı modelleri toodetect anormallikleri, araç bakım algılaması için diğeri için araç geri çağırma algılama oluşturduk. Her iki bu modellerinde hello yerleşik asıl bileşen analiz (PCA) algoritması anomali algılama için kullanılır. 

**Bakım algılama modeli**

Üç göstergeleri - lastiği baskısı, altyapısı Petrol veya altyapısı sıcaklık - birini ilgili koşul uymazsa hello bakım algılama modelini bir anomali bildirir. Sonuç olarak, yalnızca tooconsider hello model oluşturmanın bu üç değişkenleri ihtiyacımız var. Azure Machine learning'de bizim denemesinde önce kullandığımız bir **Select Columns in Dataset sütun** modülü tooextract bu üç değişkenleri. Sonraki hello PCA tabanlı anomali algılama modülü toobuild hello anomali algılama modelini kullanın. 

Asıl bileşen analiz (PCA) uygulanan toofeature seçim, Sınıflandırma ve anomali algılama olabilir machine learning'de kurulmuş bir tekniktir. PCA durum büyük olasılıkla bağıntılı değişkenleri asıl bileşenleri adı verilen değerleri kümesine içeren bir dizi dönüştürür. böylece daha kolay özellikleri ve anormallikleri tanımlanabilir hello anahtar PCA tabanlı model tooproject veri küçük boyutlu bir alanı üzerine olur.

Her yeni giriş çok hello için algılama modelini hello anomali algılayıcısı ilk hello eigenvectors üzerinde kendi projeksiyon hesaplar ve sonra yeniden yapılandırma hata hesaplar hello normalleştirilmiş. Merhaba anomali puanı bu normalleştirilmiş hatasıdır. Merhaba yüksek hello hata hello daha anormal hello örneğidir. 

3 boyutlu boşluk nokta koordinatları lastiği baskısı, altyapısı Petrol ve altyapısı sıcaklık tarafından tanımlanan hello bakım algılama sorun her kayıt kabul edilebilir. toocapture bu anormallikleri biz hello özgün veriler hello 3 boyutlu alanda PCA kullanarak 2 boyutlu boşluk yansıtabilirsiniz. Bu nedenle, PCA toobe 2 hello parametre bileşenleri toouse sayısını ayarlar. Bu parametre, PCA tabanlı anomali algılama uygulama önemli bir rol oynar. PCA kullanarak planlanması verileri sonra Biz bu anormallikleri daha kolay tanımlayabilirsiniz.

**Geri çağırma anomali algılama modelini** hello Select Columns in Dataset ve PCA tabanlı anomali sütun kullanırız hello geri çağırma anomali algılama modelinde, benzer bir şekilde algılama modüller. Özellikle de önce ayıklamanız biz üç değişkenleri - altyapısı sıcaklık, dış sıcaklık ve hızı - hello kullanarak **Select Columns in Dataset sütun** modülü. Ayrıca hello hızı eklediğimiz hello altyapısı sıcaklık genellikle olduğundan değişkeni bağıntılı toohello hızı. Sonraki PCA tabanlı anomali algılama modülü tooproject hello veri 2 boyutlu boşluk üzerine hello 3 boyutlu alanından kullanırız. Hello geri çağırma ölçütlerini karşılamadı ve bu nedenle altyapısı sıcaklık ve dış sıcaklığı yüksek oranda olumsuz bağıntılı zaman hello araç geri çağırma gerektirir. PCA tabanlı anomali algılama algoritması kullanan, biz hello anormallikleri PCA gerçekleştirildikten sonra yakalayabilirsiniz. 

Her iki modeli eğitimindeki Bakım veya geri çağırma hello giriş verisi tootrain hello PCA tabanlı anomali algılama modeli olarak gerektirmez toouse normal veri ihtiyacımız var. Deneme Puanlama hello Hello araç Bakım veya geri çağırma gerektirip gerektirmediğini eğitilmiş hello anomali algılama modelini toodetect kullanırız. 

### <a name="real-time-analysis"></a>Gerçek zamanlı analiz
Stream Analytics SQL sorgusu aşağıdaki hello kullanılan tüm tooget hello ortalama hello araç hızı, yakıt düzeyi, altyapısı sıcaklık, Kilometre Sayacı okuma, lastiği baskısı, altyapısı Petrol düzeyinin ve diğerleri gibi önemli araç parametreleri. Merhaba ortalamalar olan kullanılan toodetect anormallikleri vermek uyarıları ve belirlemek hello belirli bölgede işletilen taşıtlardan genel sistem durumu koşulları ve toodemographics ilişkilendirmek. 

![Stream Analytics sorgu için gerçek zamanlı işleme](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Şekil 13 – Stream Analytics sorgu için gerçek zamanlı işleme*

Tüm hello ortalamalar 3 saniyelik TumblingWindow hesaplanır. Biz çakışmayan ve bitişik zaman aralıkları gerektiren bu yana TubmlingWindow bu durumda kullanıyoruz. 

Azure Stream Analytics, tüm hello "Pencereleme" özellikleri hakkında daha fazla toolearn tıklatın [Pencereleme (Azure akış analizi)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Gerçek zamanlı tahmin**

Bir uygulama gerçek zamanlı hello çözüm toooperationalize hello machine learning modelini bir parçası olarak dahil edilmiştir. "RealTimeDashboardApp" olarak adlandırılan bu uygulama oluşturulur ve hello çözüm dağıtımının bir parçası yapılandırılmış. Merhaba uygulaması hello aşağıdakileri gerçekleştirir:

1. Burada Stream Analytics hello olayları bir modelinde sürekli yayımlama tooan olay hub'ı örneği dinler. ![Yayımlama hello veri akış analizi sorgu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Şekil 14 – yayımlama hello veri tooan Stream Analytics sorgu çıktısını olay hub'ı örneği* 
2. Bu uygulamayı alır her olay için: 
   
   * Machine Learning istek-yanıt Puanlama (RR) uç noktası kullanarak işlemleri hello verileri. Merhaba RRS endpoint hello dağıtımının bir parçası otomatik olarak yayımlanır.
   * Merhaba RRS çıkışı hello itme API'lerini kullanarak yayımlanan tooa Power BI dataset yapılır.

Bu desen de toointegrate bir iş kolu (LoB) uygulaması ile Merhaba gerçek zamanlı analiz akış, uyarılar, bildirimler ve mesajlaşma gibi senaryolar için istediğiniz uygulanabilir tooscenarios olur.

Tıklatın [RealtimeDashboardApp indirme](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello özelleştirmeler RealtimeDashboardApp Visual Studio çözümü. 

**tooexecute hello gerçek zamanlı Pano uygulaması**
1. Ayıklayın ve yerel olarak Kaydet ![RealtimeDashboardApp klasörü](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Şekil 16 – RealtimeDashboardApp klasörü*  
2. Merhaba uygulaması RealtimeDashboardApp.exe yürütme
3. Geçerli Power BI kimlik bilgilerini sağlayın, oturum açın ve Kabul Et'i tıklatın ![Gerçek zamanlı Pano uygulama oturum açma tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Gerçek zamanlı Pano uygulaması son oturum açma BI tooPower](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Şekil 17 – RealtimeDashboardApp: Oturum açma tooPower BI*

>[!NOTE] 
>Tooflush hello Power BI dataset istiyorsanız hello RealtimeDashboardApp hello "flushdata" parametresiyle yürütün: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Toplu iş analiz
Merhaba burada nasıl Contoso Motors tooshow düzeni, kullanım davranışı ve araç durumunu yürüten üzerinde hello Azure işlem özellikleri tooharness büyük veri toogain zengin Öngörüler yararlanan hedeftir. Bu, mümkün kılar:

* Merhaba müşteri deneyimini geliştirmek ve alışkanlık ve yakıt verimli yönlendirmeli davranışları yürüten üzerinde Öngörüler sağlayarak daha ucuzdur yapın
* Proaktif olarak müşteriler ve bunların yönlendirmeli patters toogovern iş kararları hakkında bilgi edinin ve hello en iyi sınıf ürünler ve hizmetler sağlar

Bu çözümde, biz ölçümleri aşağıdaki hello hedeflediğiniz:

1. **Davranış yürüten etkin**: hello eğilimini hello modelleri, konumları, yönlendirmeli koşullar ve agresif yönlendirmeli modeli hello yıl toogain ınsights süresini tanımlar. Contoso Motors bu Öngörüler kişiselleştirilmiş yeni özellikler ve kullanım tabanlı sigorta yürüten pazarlama kampanyaları için kullanabilirsiniz.
2. **Yakıt Al verimli yönlendirmeli davranışı**: hello eğilimini hello modelleri, konumları, yönlendirmeli koşullar ve yakıt verimli yönlendirmeli modeli hello yıl toogain ınsights süresini tanımlar. Contoso Motors bu Öngörüler, pazarlama kampanyalarının için yeni özellikler yürüten kullanabilirsiniz ve etkili ve ortam kolay yönlendirmeli alışkanlıklarınıza için öngörülü raporlama toohello sürücüleri maliyeti. 
3. **Modelleri geri çağırma**: Merhaba anomali algılama machine learning deneme faaliyete geçirmeye yönelik geri çekme gerektiren modelleri tanımlar

Her bir bu ölçümleri hello ayrıntılara göz atalım,

**Agresif yönlendirmeli düzeni**

Merhaba bölümlenmiş araç sinyalleri ve tanılama veri işlenir koşullar ve sergiler diğer parametreleri "kullanarak Hive toodetermine hello modelleri, konum, araç AggresiveDrivingPatternPipeline" adlı hello ardışık düzeninde agresif yürüten Desen yürüten.

![Agresif yönlendirmeli düzeni iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Şekil 18 – agresif yönlendirmeli düzeni iş akışı*


***Agresif yönlendirmeli düzeni Hive sorgusu***

Merhaba "aggresivedriving.hql agresif yönlendirmeli koşul düzeni çözümlemek için kullanılan" adlandırılmış Hive betiğini hello indirilen ZIP "\demo\src\connectedcar\scripts" klasör bulunur. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Bu araç'ın iletim dişli konum, Fren pedal durumu ve hız toodetect reckless/en yüksek hızda düzeni braking dayalı davranışı yürüten agresif hello bileşimini kullanır. 

Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.

![AggressiveDrivingPatternPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Şekil 19 – AggressiveDrivingPatternPipeline çıkış*

**Yakıt verimli yönlendirmeli düzeni**

araç sinyalleri Hello bölümlenmiş ve tanılama veri "FuelEfficientDrivingPatternPipeline" adlı hello ardışık düzeninde işlenir. Hive kullanılan toodetermine hello modelleri, konum, araç, yönlendirmeli koşullar ve yakıt verimli yönlendirmeli düzeni sergilemesine diğer özellikleri ' dir.

![Fuel-Efficient yönlendirmeli düzeni](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Şekil 20 – Fuel-efficient yönlendirmeli düzeni iş akışı*

***Yakıt verimli yönlendirmeli düzeni Hive sorgusu***

Merhaba "fuelefficientdriving.hql agresif yönlendirmeli koşul düzeni çözümlemek için kullanılan" adlandırılmış Hive betiğini hello indirilen ZIP "\demo\src\connectedcar\scripts" klasör bulunur. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Araç'ın iletim dişli konumu, Fren pedal durumu, hız ve verimli yönlendirmeli davranışı braking, hızlandırmasını, temel Hızlandırıcı pedal konumu toodetect yakıt hello bileşimini kullanır ve desenler hızı. 

Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.

![FuelEfficientDrivingPatternPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Şekil 21 – FuelEfficientDrivingPatternPipeline çıkış*

**Tahminleri geri çağırma**

Merhaba makine öğrenimi denemesinin sağlandığında ve hello çözüm dağıtımının bir parçası olarak bir web hizmeti olarak yayımlanır. Merhaba toplu Puanlama uç noktası data factory bağlantılı hizmet olarak kayıtlı ve veri fabrikası toplu iş Puanlama etkinliği kullanarak kullanıma hazır hale getirilmiş bu iş akışında yararlanır.

![Machine Learning uç noktası](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Veri fabrikasında bağlı hizmet olarak Şekil 22 – Machine learning uç noktası kayıtlı*

Merhaba kayıtlı bağlantılı hizmet hello anomali algılama modelini kullanarak hello DetectAnomalyPipeline tooscore hello verilerde kullanılır. 

![Machine Learning toplu veri fabrikasında Puanlama etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Şekil 23 – veri fabrikasında Azure Machine Learning toplu Puanlama etkinliği* 

Web hizmeti Puanlama hello toplu işlemle operationalized böylece bu ardışık düzendeki veri hazırlığı için gerçekleştirilen birkaç adım vardır. 

![Geri çekme gerektiren taşıtlardan tahmin etmeye yönelik DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Şekil 24 – geri çekme gerektiren taşıtlardan tahmin etmeye yönelik DetectAnomalyPipeline* 

***Anomali algılama Hive sorgusu***

Merhaba Puanlama tamamlandığında, bir Hdınsight kullanılan tooprocess ve anormallikleri 0.60 veya daha yüksek olasılık puanı hello modeli tarafından ayrılır toplama hello veri etkinliktir.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.

![DetectAnomalyPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Şekil 25 – DetectAnomalyPipeline çıkış*

## <a name="publish"></a>Yayımlama

### <a name="real-time-analysis"></a>Gerçek zamanlı analiz
Merhaba Stream Analytics işi hello sorgularda birini yayımlar hello olayları tooan çıkış Event Hub örneği. 

![Akış analizi işi yayımlar tooan çıkış olay hub'ı örneği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Şekil 26 – Stream Analytics işi yayımlar tooan çıkış olay hub'ı örneği*

![Stream Analytics sorgu toopublish toohello olay hub'ı örnek çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Şekil 27 – Stream Analytics sorgu toopublish toohello çıktısını olay hub'ı örneği*

Bu akış olayların RealTimeDashboardApp hello çözümdeki hello tarafından kullanılır. Bu uygulamayı gerçek zamanlı Puanlama hello Machine Learning istek-yanıt web hizmetini yararlanır ve hello sonuç veri tooa Power BI dataset tüketimi için yayımlar. 

### <a name="batch-analysis"></a>Toplu iş analiz
Merhaba toplu ve gerçek zamanlı işleme Hello sonuçları tüketimi için yayımlanan toohello Azure SQL veritabanı tabloları ' dir. Hello Azure SQL Server, veritabanı ve hello tablolar hello Kurulum komut dosyasının bir parçası otomatik olarak oluşturulur. 

![Toplu işleme sonuçlarını toodata mart iş akışı kopyalama](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Şekil 28 – toplu sonuçları kopyalama toodata mart iş akışı işleme*

![Akış analizi işi toodata mart yayımlar](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Şekil 29 – Stream Analytics işi toodata mart yayımlar*

![Veri reyonu ayarında Stream Analytics işi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Şekil 30 – Data mart Stream Analytics işinde ayarlama*

## <a name="consume"></a>Tüketme
Power BI Bu çözüm gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano sağlar. 

Merhaba Power BI raporları ve hello Pano ayarlama hakkında ayrıntılı yönergeler için buraya tıklayın. Merhaba son Pano şöyle görünür:

![Power BI Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Şekil 31 - Power BI Panosu*

## <a name="summary"></a>Özet
Bu belgede ayrıntılı ayrıntıya hello araç Telemetri analiz çözümü, içerir. Bu bir lambda mimarisi desenini paylaşan gerçek zamanlı ve toplu analytics Öngörüler ve Eylemler ile. Bu desen (gerçek zamanlı) etkin yolunuzda gerektiren kullanım örnekleri tooa çeşitli uygular ve yolunuzda (toplu) analytics. 

