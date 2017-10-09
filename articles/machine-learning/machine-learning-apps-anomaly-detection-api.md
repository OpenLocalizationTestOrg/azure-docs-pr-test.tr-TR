---
title: "Machine Learning Anomali algılama API'si aaaAzure | Microsoft Docs"
description: "Anomali algılama API zaman serisi veri zamanında hep aralıklı sayısal değerler ile anormallikleri algılar Microsoft Azure Machine Learning ile yerleşik bir örnektir."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>Anomali algılama API makine
## <a name="overview"></a>Genel Bakış
[Anomali algılama API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) zaman serisi veri zamanında hep aralıklı sayısal değerler ile anormallikleri algılar Azure Machine Learning ile oluşturulmuş bir örnek verilmiştir.

Bu API hello şu anormal desenleri zaman serisi veri türlerini saptayabilir:

* **Pozitif ve negatif eğilimleri**: Örneğin, ne zaman yukarı eğilimi bilgi işlem bellek kullanımını izleme ilgi çekici bir bellek sızıntısı göstergesi olabilir olarak olabilir
* **Merhaba dinamik aralık değerleri değişiklikleri**: Örneğin, bir bulut hizmeti tarafından oluşturulan hello özel durumlar izlerken hello dinamik aralık değerleri değişiklikler hello hizmetinin hello durumunun kararsızlığı olduğunu gösteriyor olabilir ve
* **Ani ve Dips**: Örneğin, bir hizmette oturum açma hataları veya kullanıma sayının e-ticaret sitesi hello izlerken, ani veya dıps anormal davranışları olduğunu gösteriyor olabilir.

Bu makine öğrenme algılayıcılar değerleri gibi değişiklikleri anomali puanları olarak değerlerine zaman ve rapor süregiden değişiklikler üzerinden izleyebilirsiniz. Bunlar geçici eşiği ayarlama gerektirmez ve puanlarını kullanılan toocontrol yanlış pozitif oranı olabilir. Merhaba anomali algılama API, KPI'ları zamanla kullanımı izleyerek hizmet izleme gibi çeşitli senaryolarda kullanışlıdır arama, tıklama sayıda sayısı gibi ölçümleri aracılığıyla izleme performans sayaçları bellek, CPU, dosya gibi aracılığıyla izleme okur, zaman içinde vb..

Merhaba Anomali algılama sunan başlattığınız yararlı Araçlar tooget ile birlikte gelir.

* Merhaba [web uygulaması](http://anomalydetection-aml.azurewebsites.net/) değerlendirmek ve verileriniz üzerinde anomali algılama API'leri hello sonuçlarını görselleştirmenize yardımcı olur.

> [!NOTE]
> Deneyin **BT Anomali Insights çözümü** tarafından sağlanmıştır [bu API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)
> 
> tooget bu son tooend çözümü dağıtılmış tooyour Azure aboneliği <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **buradan başlayın >**</a>
> 
>

## <a name="api-deployment"></a>API dağıtımı
Sipariş toouse hello API, burada bir Azure Machine Learning web hizmeti olarak barındırılacak Azure aboneliği tooyour dağıtmalısınız.  Hello bunu yapabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  Bu iki AzureML Web Hizmetleri (ve ilgili kaynaklarını) dağıtacağınız tooyour Azure aboneliği - biri mevsimselliğin algılama anomali algılama ve bir mevsimselliğin algılama olmadan.  Merhaba dağıtım tamamlandıktan sonra API'lerden mümkün toomanage olacaktır hello [AzureML web Hizmetleri](https://services.azureml.net/webservices/) sayfası.  Bu sayfadan, mümkün toofind API anahtarları, uç nokta konumlarının olması yanı sıra hello API'sini çağırmak için kodu örnek.  Daha ayrıntılı yönergeler kullanılabilir [burada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>Merhaba API ölçeklendirme
Varsayılan olarak, dağıtımınızı 1.000 işlemleri/ay ve 2 işlem saat/ay içeren boş bir fatura geliştirme ve Test planı sahip olur.  Tooanother planı gereksinimlerinize uygun şekilde yükseltebilirsiniz.  Merhaba farklı planları fiyatlandırma hakkında ayrıntıları [burada](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) "Üretim Web API fiyatlandırma" altında.

## <a name="managing-aml-plans"></a>AML yönetme planları 
Faturalandırma planınıza yönetebilirsiniz [burada](https://services.azureml.net/plans/).  Merhaba plan adı hello API dağıtırken seçtiğiniz hello kaynak grubu adı artı benzersiz tooyour abonelik bir dizeye dayalı olarak belirlenir.  Nasıl tooupgrade planınız kullanılabilir yönergeleri [burada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) hello "faturalandırma planları yönetme" bölümünün altında.

## <a name="api-definition"></a>API tanımı
Merhaba web hizmeti sağlayan REST tabanlı bir API web veya mobil uygulama, R, Python, Excel gibi farklı yollarla tüketilebilir HTTPS üzerinden vb..  Zaman serisi veri toothis hizmetiniz bir REST API çağrısı aracılığıyla göndermek ve aşağıda açıklanan hello anomali üç birlikte çalışır.

## <a name="calling-hello-api"></a>Merhaba API çağırma
Sipariş toocall hello API, tooknow hello uç nokta konumu ve API anahtarı gerekir.  Merhaba API'sini çağırmak için örnek kod ile birlikte bunların her ikisi de hello kullanılabilir [AzureML web Hizmetleri](https://services.azureml.net/webservices/) sayfası.  İstenen toohello API gidin ve hello "Tüket" sekmesini toofind ardından bunları.  Hello API olarak Swagger API'si çağırabilirsiniz unutmayın (yani hello URL parametresi ile `format=swagger`) veya farklı bir harici - Swagger API'si (yani, hello olmadan `format` URL parametresi).  Merhaba örnek kod hello Swagger biçimini kullanır.  Aşağıda bir örnek istek ve yanıt Swagger olmayan biçimindedir.  Bu örnek toohello mevsimselliğin endpoint verilebilir.  Merhaba mevsimselliğin olmayan endpoint benzer.

### <a name="sample-request-body"></a>Örnek istek gövdesi
Merhaba isteği iki nesne içerir: `Inputs` ve `GlobalParameters`.  Diğerleri değildir hello örnek aşağıdaki isteği, bazı parametreler açıkça gönderilen (aşağı kaydırın her bitiş noktasıyla ilgili parametrelerin tam bir listesi için).  Merhaba istekte açıkça gönderilip gönderilmeyeceğini Parametreler aşağıda verilen hello varsayılan değerleri kullanır.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Örnek Yanıtı
Unutmayın sipariş toosee hello `ColumnNames` alan içermelidir `details=true` isteğiniz bir URL parametresi olarak.  Bu alanların her biri arkasında hello anlamı için aşağıdaki Hello tablolara bakın.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>Puan API
Merhaba puan API anomali algılama Mevsimlik olmayan zaman serisi veri üzerinde çalıştırmak için kullanılır. Merhaba API anomali algılayıcılar sayısı hello verileri çalıştırır ve anomali puanlarını döndürür. Aşağıdaki Hello şekilde puan API algılayabilir bu hello anormallikleri örneği gösterilmektedir. Bu zaman serisi 2 ayrı düzeyi değişir ve 3 ani sahiptir. Merhaba kırmızı nokta hello siyah nokta algılanan hello ani gösterirken hangi hello düzey değişikliği, algılandığında hello zamanı gösterir.
![Puan API][1]

### <a name="detectors"></a>Algılayıcılar
Merhaba anomali algılama API algılayıcılar 3 geniş kategorilerde destekler. Belirli giriş parametreleri ve her algılayıcı çıktıların hakkında ayrıntılar aşağıdaki tablonun hello bulunabilir.

| Algılayıcısı kategorisi | Algılayıcısı | Açıklama | Giriş parametreleri | Çıkışları |
| --- | --- | --- | --- | --- |
| Depo algılayıcılar |TSpike algılayıcısı |Ani ve birinci ve üçüncü Dörttebirlikler değerler uzak hello göre dıps Algıla |*tspikedetector.sensitivity:* hello aralığındaki tamsayı değeri 1-10, varsayılan alır: 3; Daha yüksek değerler, böylece daha az hassas yapmadan birden fazla aşırı değeri yakalar |TSpike: ikili değerler – '1' depo/DIP algılanırsa, '0' Aksi takdirde |
| Depo algılayıcılar | ZSpike algılayıcısı |Ani ve üzerinde ne kadar hello datapoints göre dıps ortalamasını saptamak |*zspikedetector.sensitivity:* hello aralığındaki tamsayı değeri 1-10, varsayılan alın: 3; Daha yüksek değerleri daha az hassas kolaylaştırarak birden fazla aşırı değeri yakalar |ZSpike: ikili değerler – '1' depo/DIP algılanırsa, '0' Aksi takdirde | |
| Yavaş eğilimi algılayıcısı |Yavaş eğilimi algılayıcısı |Merhaba kümesi duyarlılık göredir yavaş pozitif eğilimi Algıla |*trenddetector.sensitivity:* algılayıcısı puan eşiğine (varsayılan: 3,25, 3,25 – 5 makul sınırlar tooselect öğesinden; hello yüksek hello daha az duyarlı) |tscore: anomali puan eğilimi üzerinde temsil eden kayan sayısı |
| Düzey değişikliği algılayıcılar | Çift yönlü düzeyi değişiklik algılayıcısı |Hello kümesi duyarlılığına göre yukarı ve aşağı düzey değişikliği algılar |*bileveldetector.sensitivity:* algılayıcısı puan eşiğine (varsayılan: 3,25, 3,25 – 5 makul sınırlar tooselect öğesinden; hello yüksek hello daha az duyarlı) |rpscore: anomali puan yukarı ve aşağı düzey değişiklik gösteren kayan sayı | |

### <a name="parameters"></a>Parametreler
Bu giriş parametreleri hakkında daha ayrıntılı bilgi hello aşağıdaki tabloda listelenmiştir:

| Giriş parametreleri | Açıklama | Varsayılan ayar | Tür | Geçerli aralık | Önerilen aralık |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Anomali puan hesaplama için kullanılan geçmişinde (veri noktası sayısı) |500 |tamsayı |10-2000 |Zaman serisi bağımlı |
| detectors.spikesdips | Olup toodetect yalnızca ani, yalnızca dıps veya her ikisi |Her ikisi |Numaralandırılan |Her ikisi de, ani, Dıps |Her ikisi |
| bileveldetector.sensitivity |Çift yönlü düzeyi duyarlılık algılayıcısı değiştirin. |3.25 |Çift |None |3,25 5 (daha düşük değerler daha hassas anlamına gelir) |
| trenddetector.sensitivity |Pozitif eğilimi algılayıcısı duyarlılık. |3.25 |Çift |None |3,25 5 (daha düşük değerler daha hassas anlamına gelir) |
| tspikedetector.sensitivity |Duyarlılık TSpike algılayıcısı |3 |tamsayı |1-10 |3-5 (daha düşük değerler daha hassas anlamına gelir) |
| zspikedetector.sensitivity |Duyarlılık ZSpike algılayıcısı |3 |tamsayı |1-10 |3-5 (daha düşük değerler daha hassas anlamına gelir) |
| postprocess.tailRows |Hello çıkış sonuçlarında tutulan toobe hello son veri noktaları |0 |tamsayı |(tüm veri noktaları tutun) 0 veya sonuçlarında noktaları tookeep sayısını belirtin |Yok |

### <a name="output"></a>Çıktı
Merhaba API tüm algılayıcılar zaman serisi verileriniz üzerinde çalışır ve anomali puanlarını ve her nokta için ikili depo göstergeleri zamanında döndürür. Merhaba tabloda hello API çıkışlarından listelenir. 

| Çıkışları | Açıklama |
| --- | --- |
| Zaman |Ham verileri veya toplanan (ve/veya) imputed verilerden zaman damgaları, toplama (ve/veya) eksik veri imputation uygulanır |
| Veriler |Değerleri ham verileri veya toplanan (ve/veya) imputed veri varsa toplama (ve/veya) eksik veri imputation uygulanır |
| TSpike |İkili gösterge tooindicate bir ani TSpike algılayıcısı tarafından mı algılandı |
| ZSpike |İkili gösterge tooindicate bir ani ZSpike algılayıcısı tarafından mı algılandı |
| rpscore |Kayan sayı temsil eden anomali puan çift yönlü düzeyi değişiklik |
| rpalert |çift yönlü düzeyi var. gösteren 1/0 değeri hello giriş duyarlılığına göre anomali değiştirme |
| tscore |Kayan sayı temsil eden anomali puan üzerinde pozitif eğilimi |
| talert |var. gösteren 1/0 hello giriş duyarlılığına göre pozitif eğilimi anomali değerdir |

## <a name="scorewithseasonality-api"></a>ScoreWithSeasonality API
Merhaba ScoreWithSeasonality API anormallik algılamayı Mevsimlik düzenlere sahip zaman serisi çalıştırmak için kullanılır. Mevsimlik desenleri yararlı toodetect sapmaları API'dir.  
Merhaba aşağıdaki şekilde bir Mevsimlik zaman serisinin algılanan anormallikleri örneği gösterilmektedir. Merhaba zaman serisi bir depo (Merhaba 1 siyah nokta), iki dıps (Merhaba 2 siyah nokta ve bir hello sonunda) ve tek düzey değişikliği (kırmızı nokta) sahiptir. Her ikisi de hello zaman serisinin hello ortasında DIP hello ve hello düzey değişikliği yalnızca discernable Mevsimlik bileşenleri hello serisinden kaldırıldıktan sonra unutmayın.
![Mevsimselliğin API][2]

### <a name="detectors"></a>Algılayıcılar
Merhaba mevsimselliğin uç noktada Hello algılayıcılar benzer toohello olanları hello mevsimselliğin olmayan uç noktası, ancak biraz farklı parametre adları (aşağıda listelenen) ile var.

### <a name="parameters"></a>Parametreler

Bu giriş parametreleri hakkında daha ayrıntılı bilgi hello aşağıdaki tabloda listelenmiştir:

| Giriş parametreleri | Açıklama | Varsayılan ayar | Tür | Geçerli aralık | Önerilen aralık |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Toplama aralığı toplama için saniye cinsinden zaman serisi giriş |0 (hiçbir toplama gerçekleştirilir) |tamsayı |0: toplama, > 0 aksi atla |Zaman serisi bağımlı olan 5 dakika too1 günü |
| preprocess.aggregationFunc |Merhaba veri toplamak için kullanılan işlev AggregationInterval belirtilen |Ortalama |Numaralandırılan |Ortalama, Topla, uzunluğu |Yok |
| preprocess.replaceMissing |Kullanılan değerleri tooimpute eksik veri |lkv (bilinen son değer) |Numaralandırılan |sıfır, lkv, ortalama |Yok |
| detectors.historyWindow |Anomali puan hesaplama için kullanılan geçmişinde (veri noktası sayısı) |500 |tamsayı |10-2000 |Zaman serisi bağımlı |
| detectors.spikesdips | Olup toodetect yalnızca ani, yalnızca dıps veya her ikisi |Her ikisi |Numaralandırılan |Her ikisi de, ani, Dıps |Her ikisi |
| bileveldetector.sensitivity |Çift yönlü düzeyi duyarlılık algılayıcısı değiştirin. |3.25 |Çift |None |3,25 5 (daha düşük değerler daha hassas anlamına gelir) |
| postrenddetector.sensitivity |Pozitif eğilimi algılayıcısı duyarlılık. |3.25 |Çift |None |3,25 5 (daha düşük değerler daha hassas anlamına gelir) |
| negtrenddetector.sensitivity |Negatif eğilimi algılayıcısı duyarlılık. |3.25 |Çift |None |3,25 5 (daha düşük değerler daha hassas anlamına gelir) |
| tspikedetector.sensitivity |Duyarlılık TSpike algılayıcısı |3 |tamsayı |1-10 |3-5 (daha düşük değerler daha hassas anlamına gelir) |
| zspikedetector.sensitivity |Duyarlılık ZSpike algılayıcısı |3 |tamsayı |1-10 |3-5 (daha düşük değerler daha hassas anlamına gelir) |
| seasonality.Enable |Mevsimselliğin analiz toobe olup olmadığını gerçekleştirilen |TRUE |Boole değeri |TRUE, false |Zaman serisi bağımlı |
| seasonality.numSeasonality |Algılanan düzenli döngüleri toobe maksimum sayısı |1 |tamsayı |1, 2 |1-2 |
| seasonality.Transform |Mevsimlik olup olmadığını (ve) eğilimi bileşenleri anomali algılama uygulamadan önce kaldırılması |deseason |Numaralandırılan |None, deseason, deseasontrend |Yok |
| postprocess.tailRows |Hello çıkış sonuçlarında tutulan toobe hello son veri noktaları |0 |tamsayı |(tüm veri noktaları tutun) 0 veya sonuçlarında noktaları tookeep sayısını belirtin |Yok |

### <a name="output"></a>Çıktı
Merhaba API tüm algılayıcılar zaman serisi verileriniz üzerinde çalışır ve anomali puanlarını ve her nokta için ikili depo göstergeleri zamanında döndürür. Merhaba tabloda hello API çıkışlarından listelenir. 

| Çıkışları | Açıklama |
| --- | --- |
| Zaman |Ham verileri veya toplanan (ve/veya) imputed verilerden zaman damgaları, toplama (ve/veya) eksik veri imputation uygulanır |
| OriginalData |Değerleri ham verileri veya toplanan (ve/veya) imputed veri varsa toplama (ve/veya) eksik veri imputation uygulanır |
| ProcessedData |Merhaba aşağıdakilerden herhangi birini: <ul><li>Önemli mevsimselliğin algılandı ve seçeneğe deseason Mevsimlik değişiklikler zaman serisi ayarlandı;</li><li>Mevsimlik değişiklikler ayarlanmış ve önemli mevsimselliğin algıladıysa zaman serisi ve deseasontrend seçeneği seçili değişimleri giderilmiş</li><li>Aksi takdirde, bu olduğu hello OriginalData aynı</li> |
| TSpike |İkili gösterge tooindicate bir ani TSpike algılayıcısı tarafından mı algılandı |
| ZSpike |İkili gösterge tooindicate bir ani ZSpike algılayıcısı tarafından mı algılandı |
| BiLevelChangeScore |Kayan sayı temsil eden anomali puan düzeyi değişiklik |
| BiLevelChangeAlert |hello giriş duyarlılığına göre bir düzey değişikliği anomali olduğunu gösteren 1/0 değeri var. |
| PosTrendScore |Kayan sayı temsil eden anomali puan üzerinde pozitif eğilimi |
| PosTrendAlert |var. gösteren 1/0 hello giriş duyarlılığına göre pozitif eğilimi anomali değerdir |
| NegTrendScore |Kayan sayı temsil eden anomali puana negatif eğilimi üzerinde |
| NegTrendAlert |var. gösteren 1/0 hello giriş duyarlılığına göre negatif eğilimi anomali değerdir |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

