---
title: "Azure Hdınsight'ta Spark kullanarak veri bilimi aaaOverview | Microsoft Docs"
description: "Merhaba Spark Mllib'i Araç Seti modelleme yetenekleri dağıtılmış toohello Hdınsight ortamı önemli makine öğrenimi getirir."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Azure Hdınsight'ta Spark kullanarak veri bilimi genel bakış
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Bu paketi konuların nasıl toouse Hdınsight Spark toocomplete ortak veri bilimi veri alımı, özellik Mühendisliği, model ve model değerlendirme gibi görevleri gösterir. kullanılan hello verileri, seyahat ve ücreti hello 2013 NYC ücreti dataset örneğidir. Merhaba modellerinin oluşturulması Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları içerir. Merhaba konuları da nasıl toostore Bu modeller Azure blob Göster storage (WASB) ve nasıl tooscore ve Tahmine dayalı kendi performansını değerlendirin. Daha gelişmiş konular ele modelleri nasıl olabilir çapraz doğrulama ve parametre hyper Süpürme kullanılarak eğitilmiş. Bu genel bakış konusunun nasıl tooset yukarı hello sağlanan hello izlenecek toocomplete hello adımları uygulamanız Spark kümesi açıklayan hello konuları da başvurur. 

## <a name="spark-and-mllib"></a>Spark ve Mllib'i
[Spark](http://spark.apache.org/) bellek içi destekleyen bir açık kaynaklı bir paralel işleme altyapısıdır işliyor tooboost hello büyük veri analizi uygulamalarının performansını. Merhaba Spark işleme altyapısı hızı, kullanımı kolay, gelişmiş analizler için yerleşik olarak bulunur. Spark'ın bellek içi dağıtılmış hesaplama özellikleri onu machine learning ve grafik hesaplamalarında kullanılan hello yinelemeli algoritmalar için iyi bir seçimdir haline getirir. [Mllib'i](http://spark.apache.org/mllib/) hello algoritmik getirir Spark'ın ölçeklenebilir machine learning kitaplığı modelleme yetenekleri toothis dağıtılmış ortamı. 

## <a name="hdinsight-spark"></a>Hdınsight Spark
[Hdınsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure açık kaynaklı Spark sunumu barındırılır. İçin destek de içerir **Jupyter PySpark not defterlerini** dönüştürme, filtreleme ve Azure BLOB'ları (WASB) içinde depolanan verileri görselleştirmek için Spark SQL etkileşimli sorguları çalıştırabilirsiniz hello Spark kümesinde. PySpark hello Spark için Python API ' dir. Merhaba çözümleri sağlayan ve burada hello Spark kümeleri üzerinde yüklü Jupyter not defterleri çalıştırmanız hello ilgili çizimleri toovisualize hello verileri göster hello kod parçacıkları. Merhaba modelleme adımları aşağıdaki konulardaki nasıl tootrain, değerlendirmek, kaydetme ve her türde bir model kullanmayı gösteren kod içerir. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Kurulum: Spark kümeleri ve Jupyter Not Defterleri
Kurulum adımlarını ve kod bu kılavuzda bir Hdınsight Spark 1.6 kullanmak için sağlanır. Ancak Jupyter not defterleri Hdınsight Spark 1.6 ve Spark 2.0 kümeleri için sağlanır. Merhaba not defterlerini ve bağlantıları toothem açıklamasını hello sağlanan [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) bunları içeren hello GitHub depo. Ayrıca, hello kod burada ve bağlı hello not defterlerini geneldir ve tüm Spark kümesi üzerinde çalışması gerekir. Hdınsight Spark kullanmıyorsanız hello Küme kurulumu ve Yönetimi adımları ne burada gösterilenden biraz farklı olabilir. Kolaylık olması için Spark 1.6 (toobe hello Jupyter not defteri sunucu, hello pySpark Çekirdeği'nde çalıştırın) ve Spark 2. 0'ı (toobe hello pySpark3 Çekirdeği'nde hello Jupyter not defteri sunucu olarak çalıştır) için toohello Jupyter not defterleri hello bağlantılar şunlardır:

### <a name="spark-16-notebooks"></a>Spark 1.6 dizüstü bilgisayarlar
Bu dizüstü bilgisayarlar Jupyter not defteri sunucusunun hello pySpark Çekirdeği'nde çalıştırmak toobe ' dir.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): ilgili bilgiler verilmektedir modelleme ve birkaç farklı algoritmalarıyla Puanlama tooperform veri keşfi,.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Not Defteri #1 ve hyperparameter ayarlama ve çapraz doğrulama kullanarak modeli geliştirme konuları içerir.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): toooperationalize Python kullanarak kaydedilmiş modeli nasıl kümeleri gösterir.

### <a name="spark-20-notebooks"></a>Spark 2.0 dizüstü bilgisayarlar
Bu dizüstü bilgisayarlar Jupyter not defteri sunucusunun hello pySpark3 Çekirdeği'nde çalıştırmak toobe ' dir.

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Bu dosyayı nasıl tooperform veri keşfi, model oluşturma ve Spark 2. 0'Puanlama hello NYC ücreti seyahat kullanarak kümeleri hakkında bilgi sağlar. ve ücreti verileri-set açıklanan [burada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Bu Not hızlı bir şekilde Spark 2.0 için sağladık hello kod keşfetme için iyi bir başlangıç noktası olabilir. Daha ayrıntılı bir not defteri hello NYC ücreti verileri analiz eder, bu listede hello sonraki not defteri bakın. Bu liste aşağıdaki bu dizüstü bilgisayarlar karşılaştırmak hello notlarına bakın. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): Bu dosyayı nasıl wrangling tooperform verileri (işlem), Spark SQL ve dataframe modelleme ve kullanarak Puanlama araştırması NYC ücreti seyahat ve açıklanan ücreti veri kümesi hello gösterir [ Burada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): Bu dosyayı nasıl wrangling tooperform verileri (işlem), Spark SQL ve dataframe modelleme ve kullanarak Puanlama araştırması, iyi bilinen uçak zamanında ayrılma hello gösterir veri kümesi 2011 ve 2012. Bu hava durumu özellikleri hello modele dahil edilebilir biz hello uçak dataset hello havaalanı hava durumu verileri (örneğin windspeed, sıcaklık, yükseklik vb.) önceki toomodeling ile tümleşik.

<!-- -->

> [!NOTE]
> Merhaba uçak dataset toohello Spark 2.0 not defterlerini eklenen toobetter hello sınıflandırma algoritmalarının kullanımını gösterir. Uçak zamanında ayrılma dataset ve hava durumu veri kümesi hakkında bilgi için bağlantılar aşağıdaki hello bakın:

>- Uçak zamanında ayrılma veri: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Havaalanı hava durumu verileri: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Merhaba NYC ücreti Hello Spark 2.0 not defterlerini ve uçak uçuş gecikme veri kümeleri, 10 dakika veya daha fazla toorun (bağlı olarak, HDI kümesi boyutunu hello) alabilir. Merhaba hello listesinin ilk not defteri gösterir pek çok görünüşünün hello veri keşfi, Görselleştirme ve ML model eğitim aşağı örneklenen NYC veri hangi hello ücreti ve ücreti dosyaları önceden birleştirilmiş kümesi, daha az zaman toorun götüren bir Not: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) bir çok daha kısa süre toofinish (2-3 dakika) bu not alır ve olması iyi bir başlangıç noktası hızla hello kod keşfetme için sahip olduğumuz Spark 2.0 için sağlanır. 

<!-- -->

Merhaba hello operationalization bir Spark 2.0 modeli ve puanlama için model tüketim hakkında yönergeler için bkz [Spark 1.6 belge tüketimi üzerinde](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) gerekli hello adımları anahat oluşturma örneği. toouse bu Spark 2.0 Değiştir hello Python kodu dosyasıyla [bu dosyayı](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Ön koşullar
yordamları izleyerek hello ilgili tooSpark 1.6 ' dir. Merhaba Spark 2.0 sürümü için kullanım hello not defterlerini açıklanan ve toopreviously bağlanır. 

1. bir Azure aboneliğinizin olması gerekir. Zaten bir yoksa, bkz: [alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2., bu kılavuzda Spark 1.6 küme toocomplete gerekir. toocreate, sağlanan hello yönergeleri bkz [Başlarken: Azure Hdınsight'ta Apache Spark oluşturmak](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Merhaba küme türü ve sürümü hello belirtilen **küme türü seçin** menüsü. 

![Küme yapılandırma](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Merhaba nasıl toouse Python yerine Scala toocomplete bir uçtan uca veri bilimi işlemi için görevler gösterir bir konuya bakın [veri bilimi Azure üzerinde Spark Scala kullanarak](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Merhaba NYC 2013 ücreti verileri
Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış virgülle ayrılmış değerler (CSV) dosyaları (~ 48 GB sıkıştırılmamış), 173 milyondan fazla kapsayan tek tek dönüşleri ve hello fares her seyahat için ücretli. Her seyahat kayıt hello çekme yukarı ve teslim konumu ve zaman, anonim korsan (sürücü) lisans numarası ve medallion (ücreti'nın benzersiz kimliği) numarasını içerir. Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:

1. Merhaba 'trip_data' CSV dosyaları yolcu sayısı gibi seyahat ayrıntıları içerir, almak ve dropoff noktalarını süresi ve seyahat uzunluğu seyahat. Birkaç örnek kayıt şunlardır:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Merhaba 'trip_fare' CSV dosyaları için ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat Ücretli hello ücreti ayrıntılarını içerir. Birkaç örnek kayıt şunlardır:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Biz bu dosyaları ve birleştirilmiş hello seyahat % 0,1 örneği önlemlerin\_veri ve seyahat\_masrafları CVS dosyaları bir tek veri kümesi toouse hello girdi veri kümesi bu kılavuz olarak. Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti hello alanlarının oluşur: medallion, korsan\_lisans ve alma\_datetime. Merhaba kümesinin her bir kaydı NYC ücreti seyahati temsil eden öznitelikleri aşağıdaki hello içerir:

| Alan | Kısa açıklama |
| --- | --- |
| medallion |Anonim ücreti medallion (benzersiz ücreti kimliği) |
| hack_license |Anonim Hackney satır lisans numarası |
| vendor_id |Ücreti satıcı kimliği |
| rate_code |Ücreti NYC ücreti oranı |
| store_and_fwd_flag |Depolama ve iletme bayrağı |
| pickup_datetime |Tarih ve saat seçin |
| dropoff_datetime |Dropoff tarih ve saat |
| pickup_hour |Saati seçin |
| pickup_week |Merhaba yılın haftası seçin |
| Haftanın günü |Haftanın günü (aralık 1-7) |
| passenger_count |Ücreti seyahat yolcu sayısı |
| trip_time_in_secs |Seyahat süresini saniye cinsinden |
| trip_distance |Mili seyahat seyahat uzaklığı |
| pickup_longitude |Boylam seçin |
| pickup_latitude |Enlem seçin |
| dropoff_longitude |Dropoff boylam |
| dropoff_latitude |Dropoff enlem |
| direct_distance |Yukarı çekme arasındaki uzaklığı doğrudan ve dropoff konumları |
| payment_type |Ödeme türü (CA'lar, kredi kartı vb.) |
| fare_amount |Ücreti tutar |
| Ek ücret |Ek ücret |
| mta_tax |MTA vergi |
| tip_amount |İpucu tutar |
| tolls_amount |Tolls tutar |
| total_amount |Toplam miktarı |
| Eğimli |Eğimli (0/1 Hayır Evet veya) |
| tip_class |Sınıf İpucu (0: 0, 1: $0-5, 2: $6-10, 3: $11-20, 4: > $20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Merhaba Spark kümesinde Jupyter not defteri gelen kodu yürütme
Merhaba Jupyter not defteri hello Azure Portalı'ndan başlatabilirsiniz. Spark kümenizin Panonuzda bulun ve tooenter Yönetim sayfasında kümeniz için tıklatın. Merhaba Spark kümesi ile ilişkili tooopen hello dizüstü tıklatın **küme panolarında** -> **Jupyter not defteri** .

![Küme panolarında](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

Ayrıca çok gözatabilirsiniz***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello Jupyter not defterleri. Bu URL Hello CLUSTERNAME parçası hello kendi küme adıyla değiştirin. Yönetici hesabı tooaccess hello defterlerinizi için başlangıç parolası gerekir.

![Jupyter not defterleri Gözat](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

PySpark toosee Spark konunun bu paketi için hello kod örnekleri içeren PySpark API.hello not defterlerini kullanılabilir hello kullanan önceden paketlenmiş not defterlerini birkaç örnekleri içeren bir dizin seçin [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Merhaba defterlerinden doğrudan yükleyebilirsiniz [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello Jupyter not defteri Spark kümenizin sunucusunda. Merhaba Hello giriş sayfasında, Jupyter birini tıklatın **karşıya** hello Merhaba ekranında sağ parçası düğmesinde. Dosya Gezgini'ni açar. Merhaba GitHub (Ham içerik) URL'sini hello not defteri ve tıklatın burada yapıştırabilirsiniz **açık**. 

Merhaba dosya adı ile Jupyter dosya listenizdeki gördüğünüz bir **karşıya** yeniden düğmesi. Bu tıklatın **karşıya** düğmesi. Şimdi hello dizüstü aldınız. Bu adımları tooupload hello bu kılavuzda diğer defterlerinden yineleyin.

> [!TIP]
> Tarayıcı ve seçim hello bağlantılar sağ **bağlantıyı Kopyala** tooget hello github Ham içerik URL'si. Merhaba Jupyter karşıya dosya Gezgini iletişim kutusuna bu URL'yi yapıştırabilirsiniz.
> 
> 

Artık şunları yapabilirsiniz:

* Merhaba dizüstü tıklayarak Hello koduna bakın.
* Her bir hücre tuşlarına basarak yürütme **SHIFT-ENTER**.
* Merhaba tüm not tıklayarak çalıştırın **hücre** -> **çalıştırmak**.
* Merhaba otomatik görselleştirme sorgu kullanın.

> [!TIP]
> Merhaba PySpark çekirdeği otomatik olarak (HiveQL) SQL sorguları hello çıktısını visualizes. Hello kullanarak hello seçeneği tooselect görselleştirmeleri (tablo, pasta, çizgi, alan veya çubuğu) birkaç farklı türde arasında verilir **türü** menü düğmelerini hello Not:
> 
> 

![Lojistik regresyon ROC eğrisi genel yaklaşım için](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Sırada ne var?
Hdınsight Spark kümesinde ile ayarlama ve hello Jupyter not defterleri karşıya yüklediğiniz artık toohello üç PySpark not defterlerini karşılık hello konuları aracılığıyla hazır toowork demektir. Bunlar Göster nasıl tooexplore veri ve ardından nasıl toocreate ve modelleri için kullanabilir. Gelişmiş Veri keşfi ve not defteri gösterir nasıl modelleme hello tooinclude çapraz doğrulama, hyper-parametre Süpürme ve model değerlendirme. 

**Veri keşfi ve modelleme ile Spark:** hello dataset keşfetmek ve oluşturmak, Puanlama ve hello makine öğrenimi modellerini hello aracılığıyla çalışma değerlendirme [hello Spark ile veri için ikili sınıflandırma ve regresyon model oluşturma Mllib'i Araç Seti](machine-learning-data-science-spark-data-exploration-modeling.md) konu.

**Model tüketimi:** toolearn tooscore hello sınıflandırma ve regresyon modeli Bu konuda, oluşturulan nasıl bkz [puanı ve Spark yerleşik makine öğrenimi modellerini değerlendirme](machine-learning-data-science-spark-model-consumption.md).

**Çapraz doğrulama ve hyperparameter Süpürme**: bkz [veri keşfi ve modelleme Spark ile Gelişmiş](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) modelleri nasıl olabilir üzerinde çapraz doğrulama ve parametre hyper Süpürme kullanılarak eğitilmiş

