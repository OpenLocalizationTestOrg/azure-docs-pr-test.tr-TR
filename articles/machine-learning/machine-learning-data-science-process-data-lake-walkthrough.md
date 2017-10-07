---
title: "Azure Data Lake ile ölçeklenebilir veri bilimi: bir uçtan uca kılavuz | Microsoft Docs"
description: "Nasıl bir veri kümesine toouse Azure Data Lake, toodo veri keşfi ve ikili sınıflandırma görevleri."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Azure Data Lake ile ölçeklenebilir veri bilimi: bir uçtan uca gözden geçirme
Bu kılavuz bir ipucu tarafından ücreti ödenen olup olmadığını nasıl toouse Azure Data Lake toodo veri keşfi ve ikili sınıflandırma görevleri hello NYC örneği üzerinde seyahat ve ücreti dataset toopredict ücreti gösterir. Merhaba hello adımlarda size yol gösterir [takım veri bilimi işlemi](http://aka.ms/datascienceprocess), uçtan uca, veri alım toomodel eğitim ve hello modeli yayımlayan bir web hizmeti toohello dağıtımı.

### <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
Merhaba [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) tüm hello özellikleri gerekli toomake sahip Itanium tabanlı sistemler için veri bilimcilerine toostore veri herhangi boyutu, Şekil ve hız ve tooconduct veri analizi ve makine öğrenme modelleme gelişmiş işleme, için kolay, düşük maliyetli bir şekilde yüksek ölçeklenebilirlik ile.   Yalnızca veri gerçekte işlenirken bir iş başına temelinde ücret ödersiniz. Sorgu yetenek Karışımlar bildirim temelli SQL yapısını hello gücüyle C# tooprovide ölçeklenebilir ile Merhaba bir dil dağıtılmış, Azure Data Lake Analytics U-SQL içerir. Tooprocess sağlar üzerinde okuma, şema uygulayarak yapılandırılmamış verileri özel mantık ekleme ve kullanıcı tanımlı işlevler (UDF'ler) ve genişletilebilirlik tooenable ince tanecikli denetime nasıl içerir ölçekte tooexecute. U-SQL, arkasında hello tasarımı felsefesi hakkında daha fazla toolearn bkz [Visual Studio blog gönderisi](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Data Lake Analytics ayrıca Cortana Analytics Suite’in de önemli bir parçasıdır ve Azure SQL Veri Ambarı, Power BI ve Veri Fabrikası ile birlikte çalışır. Bu, tam bulut büyük veri ve Gelişmiş analizi platformu sunar.

Bu kılavuzda hello önkoşulları ve toocomplete hello hello veri bilimi işlemi form Data Lake Analytics ile görevleri ve nasıl kaynakları açıklayarak başlar tooinstall bunları. U-SQL'yi kullanarak hello veri işleme adımlarını özetler ve göstererek sonucuna sonra nasıl toouse Python ve Azure Machine Learning Studio toobuild ile Hive ve hello Tahmine dayalı modelleri dağıtın. 

### <a name="u-sql-and-visual-studio"></a>U-SQL ve Visual Studio
Bu kılavuz, Visual Studio tooedit U-SQL betikleri tooprocess hello dataset kullanılmasını önerir. Merhaba U-SQL betikleri ayrı bir dosyaya sağlanan ve burada açıklanmıştır. Merhaba işlem alma, keşfetme ve hello veri örnekleme içerir. Aynı zamanda, nasıl hello Azure portal işten toorun U-SQL Script gösterir. Hive tablolarını bir ilişkili Hdınsight küme toofacilitate hello yapı ve dağıtım Azure Machine Learning Studio'da bir ikili sınıflandırma modelinin hello veriler için oluşturulur.  

### <a name="python"></a>Python
Bu izlenecek yol da gösteren bir bölüm içeren nasıl toobuild ve Python ile Azure Machine Learning Studio kullanarak Tahmine dayalı bir modeli dağıtın.  Jupyter not defteri hello Python komut dosyalarıyla adımları bu işlem için sunuyoruz. Merhaba dizüstü bazı ek özellik Mühendisliği adımları ve modelleri yapım çok sınıflı sınıflandırma ve ayrıca Burada özetlenen toohello ikili sınıflandırma model modelleme regresyon gibi kodunu içerir. Merhaba regresyon görev toopredict hello diğer ipucu özelliklerini temel alarak hello ipucu miktarıdır. 

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning Studio kullanılan toobuild olan ve hello Tahmine dayalı modelleri dağıtın. Bu yapılır iki yaklaşım kullanarak: ilk Python komut dosyaları ve ardından ile Hive tablolarını Hdınsight (Hadoop) kümesinde.

### <a name="scripts"></a>Betikler
Bu kılavuzda yalnızca hello asıl adımları özetlenmiştir. Merhaba tam indirebilirsiniz **U-SQL betiği** ve **Jupyter not defteri** gelen [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Ön koşullar
Bu konularda başlamadan önce hello şunlara sahip olmanız gerekir:

* Azure aboneliği. Zaten bir yoksa, bkz: [alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Önerilen] Visual Studio 2013 veya üzeri. Zaten yüklü bu sürümlerinden birini yoksa, ücretsiz bir Community sürümü indirebilirsiniz [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> Visual Studio yerine hello Azure Portal toosubmit Azure Data Lake sorguları de kullanabilirsiniz. Nasıl toodo şekilde Visual Studio ile ve hello portal hello bölümünde başlıklı üzerindeki yönergeler size sağlayacaktır **işlem U-SQL verilerle**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Azure Data Lake için veri bilimi ortamını hazırlayın
tooprepare hello veri bilimi ortamı bu yönlendirme için kaynakları aşağıdaki hello oluşturun:

* Azure Data Lake deposu (ADLS) 
* Azure Data Lake Analytics (ADLA)
* Azure Blob storage hesabı
* Azure Machine Learning Studio hesabı
* (Önerilen) Visual Studio için Azure Data Lake araçları

Bu bölümde hakkında yönergeler sağlar toocreate her bu kaynaklar. Hive tablolarını Python, toobuild bir model yerine Azure Machine Learning ile toouse seçerseniz tooprovision Hdınsight (Hadoop) kümesi de gerekir. Bu alternatif yordam hello uygun aşağıdaki bölümde açıklanmıştır.


> [!NOTE]
> Merhaba **Azure Data Lake Store** ya da ayrı olarak oluşturulabilir veya hello oluşturduğunuzda **Azure Data Lake Analytics** hello varsayılan depolama. Her biri ayrı olarak aşağıdaki bu kaynakları oluşturmak için yönergeler başvurulan ancak hello Data Lake storage hesabını ayrı ayrı oluşturmamış.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Bir Azure Data Lake deposu oluşturma


Merhaba bir ADLS oluşturma [Azure Portal](http://portal.azure.com). Ayrıntılar için bkz [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Merhaba hello kümeye özgü AAD kimliği yukarı emin tooset olması **DataSource** hello dikey **isteğe bağlı yapılandırma** dikey açıklanan vardır. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Bir Azure Data Lake Analytics hesabı oluşturma
Merhaba bir ADLA hesabı oluşturma [Azure Portal](http://portal.azure.com). Ayrıntılar için bkz [Öğreticisi: Azure Data Lake Azure Portal kullanarak Analytics ile çalışmaya başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Bir Azure Blob storage hesabı oluşturma
Merhaba bir Azure Blob storage hesabı oluşturma [Azure Portal](http://portal.azure.com). Merhaba oluşturulur bir depolama hesabı bölümüne Ayrıntılar için bkz [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Bir Azure Machine Learning Studio hesap ayarlama
Hello/Azure Machine Learning Studio uygulamasına oturum [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) sayfası. Tıklatın hello üzerinde **hemen kullanmaya başlayın** düğmesine tıklayın ve ardından "Ücretsiz çalışma" veya "Standart çalışma"'i seçin. Bundan sonra Azure ML Studio'da mümkün toocreate denemeler olacaktır.  

### <a name="install-azure-data-lake-tools-recommended"></a>[Önerilen] Azure Data Lake Araçları'nı yükleme
Visual Studio'dan sürümünüz için Azure Data Lake araçları yükleme [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

Merhaba yükleme başarıyla tamamlandıktan sonra Visual Studio'yu açın. Merhaba Data Lake sekmesi hello menüsü hello üstünde görmeniz gerekir. Azure hesabınızda oturum açtığınızda Azure kaynaklarınızı hello sol panelinde görüntülenmesi gerekir.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>Merhaba NYC ücreti dönüşleri veri kümesi
Merhaba veri burada kullandık genel kullanıma açık bir veri kümesi--hello kümesidir [NYC ücreti dönüşleri dataset](http://www.andresmh.com/nyctaxitrips/). Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış CSV dosyalarının (sıkıştırılmamış ~ 48 GB) oluşan, 173 milyondan fazla kaydı tek tek dönüşleri ve hello fares her seyahat için ücretli. Zaman, anonim hale getirilen (sürücü) lisans numarası korsan saldırılarına ve medallion (ücreti'nın benzersiz kimliği) numarası hello ve her seyahat kayıt hello alma ve teslim konumları içerir. Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:

* Merhaba 'trip_data' CSV yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntıları içerir. Birkaç örnek kayıt şunlardır:
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Merhaba 'trip_fare' CSV ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat için ücretli hello ücreti ayrıntılarını içerir. Birkaç örnek kayıt şunlardır:
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti aşağıdaki üç alanı hello oluşur: medallion, korsan\_lisans ve alma\_datetime. Merhaba ham CSV dosyaları ortak Azure storage blobundan erişilebilir. Bu katılımı hello için U-SQL betiği hello [katılma seyahat ve ücreti tabloları](#join) bölümü.

## <a name="process-data-with-u-sql"></a>U-SQL ile verileri işleme
Bu bölümde gösterilen hello veri işleme görevlerini alma, kalite denetimi, keşfetme ve hello veri örnekleme içerir. Ayrıca gösteriyoruz nasıl toojoin seyahat ve ücreti tabloları. Merhaba son bölümü hello Azure portalında bir U-SQL komut dosyası işinden çalışma gösterir. Tooeach alt bağlantılar şunlardır:

* [Veri alımı: ortak blob verileri okuma](#ingest)
* [Veri Kalitesi denetimleri](#quality)
* [Veri keşfi](#explore)
* [Seyahat ve ücreti tabloları birleştirme](#join)
* [Veri örnekleme](#sample)
* [U-SQL işleri çalıştırma](#run)

Merhaba U-SQL betikleri ayrı bir dosyaya sağlanan ve burada açıklanmıştır. Merhaba tam indirebilirsiniz **U-SQL betikleri** gelen [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute U-SQL, açık Visual Studio tıklatın **Dosya--> Yeni Proje-->**, seçin **U-SQL projesi**, ad ve tooa klasörüne kaydedin.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Bu, olası toouse hello Azure Portal tooexecute U-SQL Visual Studio yerine olur. Toohello Azure Data Lake Analytics kaynak hello Portal gidin ve doğrudan olarak aşağıdaki şekilde hello Resimli sorguları göndermek.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Veri alımı: ortak blob verileri okuyun
hello Azure blob hello verilerde Hello konumu olarak başvurulur  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  ve kullanarak ayıklanabilir **Extractors.Csv()**. Kendi kapsayıcı adı ve depolama hesabı adı için aşağıdaki komut yerine container_name@blob_storage_account_name hello wasb adresi. Merhaba dosya adları aynı biçimde olduğundan, biz kullanabilirsiniz **seyahat\_veri_ {\*\}.csv** tüm 12 seyahat dosyalarında tooread. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

Merhaba ilk satırda üstbilgileri olduğundan, biz tooremove hello üstbilgileri gerekir ve uygun parçalara sütun türleri değiştirin. İşlenen hello tooAzure Data Lake Storage kullanarak verileri kaydetme ya da geçebiliriz **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ veya tooAzure Blob Depolama hesabı kullanarak  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

Benzer şekilde biz hello ücreti veri kümelerinde okuyabilir. Azure Data Lake Store sağ tıklatın ve verilerinize toolook seçebilirsiniz **Azure Portal--> Veri Gezgini** veya **dosya Gezgini** Visual Studio içinde. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Veri Kalitesi denetimleri
Seyahat ve ücreti tabloları içinde okunduktan sonra veri kalite denetimleri yolu izleyerek hello yapılabilir. CSV dosyaları kaynaklanan hello çıktı tooAzure Blob storage veya Azure Data Lake Store olabilir. 

Merhaba medallions, benzersiz sayısını ve medallions bulun:

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

100'den fazla dönüşleri vardı bu medallions bulun:

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Geçersiz kayıtların pickup_longitude bakımından bulun:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

Eksik değerleri için bazı değişkenler bulun:

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Veri keşfi
Daha iyi anlamasına yardımcı hello veri bazı veri araştırması tooget yapabiliriz.

Eğimli ve eğimli olmayan dönüşleri Hello dağıtımını bulun:

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

İpucu tutar sonlandırma değerlerle Hello dağıtımını bulun: 0,5,10 ve 20 dolar.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

Seyahat uzaklığı temel istatistiklerinin bulun:

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Seyahat uzaklığı, Hello yüzdebirlik değeri Bul:

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Seyahat ve ücreti tabloları birleştirme
Seyahat ve ücreti tabloları medallion, hack_license ve pickup_time tarafından katılabilir.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Her yolcu sayısı düzeyi için hello sayısı kayıtları, ortalama ipucu tutar, ipucu tutar varyansını, Eğimli dönüşleri yüzdesini hesaplayın.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Veri örnekleme
İlk biz rastgele %0,1 hello veri hello birleştirilmiş tablosundan seçin:

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

Ardından biz stratified örnekleme tarafından ikili değişken tip_class yapın:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>U-SQL işleri çalıştırma
U-SQL betikleri düzenlemeyi tamamladığınızda, Azure Data Lake Analytics hesabınızı kullanarak toohello sunucu gönderebilirsiniz. Tıklatın **Data Lake**, **işi Gönder**seçin, **Analytics hesabı**, seçin **paralellik**, tıklatıp **Gönder**  düğmesi.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Merhaba işi başarıyla derlendiğini, izleme için Visual Studio'da işinizin hello durumu görüntülenir. Hello işi çalışması bittikten sonra hello bulma iş verimliliğinizi adımları tooimprove bottleneck ve hatta yeniden yürütme hello iş yürütme işlemi yapabilirsiniz. TooAzure Portal toocheck hello U-SQL işlerinizin durumunu de gidebilirsiniz.

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Artık Azure Blob storage veya Azure Portalı'nda hello çıktı dosyaları kontrol edebilirsiniz. Bizim modelleme hello sonraki adımda için stratified hello örnek verileri kullanacağız.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Derleme ve Azure Machine Learning modellerini dağıtma
Biz için iki seçenek kullanılabilir toopull verileri Azure Machine Learning toobuild içine göstermek ve 

* Merhaba ilk seçeneğinde tooan Azure Blob yazılmış hello örneklenen verileri kullanın (Merhaba içinde **veri örnekleme** Yukarıdaki adımı) ve Python toobuild kullanabilir ve Azure Machine Learning modelinden dağıtın. 
* Hello ikinci seçenekte, doğrudan bir Hive sorgusu kullanarak Azure Data Lake hello verilerde sorgu. Bu seçenek, yeni bir Hdınsight kümesi oluşturma veya mevcut bir Hdınsight kümesine burada Azure Data Lake Storage noktası toohello NY ücreti verileri hello Hive tabloları kullanın gerektirir.  Biz, hem bu seçenekler aşağıda ele alınmıştır. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Seçenek 1: Kullanım Python toobuild ve makine öğrenimi modellerini dağıtma
toobuild ve Python kullanarak makine öğrenimi modellerini dağıtmak, yerel makinenizde veya Azure Machine Learning Studio'da Jupyter not defteri oluşturun. Merhaba Jupyter not defteri sağlanan [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) içeren tam kod tooexplore Merhaba, verileri, özellik Mühendisliği, model ve dağıtım görselleştirin. Bu makalede, yalnızca hello modelleme ve dağıtım gösterir. 

### <a name="import-python-libraries"></a>Python kitaplıkları içeri aktarma
Jupyter not defteri Sipariş toorun hello örnek veya Python komut dosyası Merhaba, hello aşağıdaki Python paketlerini gereklidir. Merhaba AzureML Not Defteri hizmeti kullanıyorsanız, bu paketleri önceden yüklenmiş olmuştur.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a>Blob hello verileri okuma
* Bağlantı dizesi   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Metin olarak okuyun
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Sütun adları eklemek ve ayrı sütunlar
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Bazı sütunları toonumeric değiştirme
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Machine learning modellerini Derleme
Burada bir seyahat veya eğimli olup olmadığını biz ikili sınıflandırma modeli toopredict oluşturun. Merhaba Jupyter Not Defteri, diğer iki modeli bulabilirsiniz: çok sınıflı sınıflandırma ve regresyon modeli.

* İlk scikit kullanılabilir toocreate kukla değişkenleri ihtiyacımız-modelleri öğrenin
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Merhaba modelleme için veri çerçeve oluşturma
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* Eğitim ve 60-40 bölünmüş test etme
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Eğitim kümesindeki Lojistik regresyon
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Sınama veri kümesi puan
  
        Y_test_pred = logit_fit.predict(X_test)
* Değerlendirme ölçümleri Hesapla
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Web hizmeti API'si derleme ve Python içinde kullanma
Model, oluşturulduktan sonra öğrenme toooperationalize hello makine istiyoruz. Burada hello ikili Lojistik modeli örnek olarak kullanırız. Merhaba scikit emin olun-yerel makinenize sürümünde 0.15.1 olduğunu öğrenin. Azure ML studio hizmeti kullanıyorsanız, bu konuda tooworry yok.

* Çalışma alanı kimlik bilgileriniz Azure ML studio ayarlarından bulun. Azure Machine Learning Studio'da tıklatın **ayarları** --> **adı** --> **yetkilendirme belirteçleri**. 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Web hizmeti oluşturma
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Web hizmeti kimlik bilgileri alma
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Web hizmeti API'sine çağırın. Toowait 5-10 saniye sonra hello önceki adıma sahip.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Seçenek 2: Oluşturma ve Azure Machine Learning modellerini doğrudan dağıtma
Azure Machine Learning Studio verileri doğrudan Azure Data Lake Deposu'ndan veri okuyabilir ve ardından kullanılan toocreate olması ve modelleri dağıtın. Bu yaklaşım hello Azure Data Lake Store işaret eden bir Hive tablosu kullanır. Bu ayrı bir Azure Hdınsight kümesi sağlanması gerekiyorsa, hangi hello Hive tablosu oluşturulur. bölümler Göster nasıl aşağıdaki hello toodo bu. 

### <a name="create-an-hdinsight-linux-cluster"></a>Hdınsight Linux kümesi oluşturma
Hdınsight kümesi (Linux) hello oluşturmak [Azure Portal](http://portal.azure.com). Merhaba Ayrıntılar için bkz **erişim tooAzure Data Lake Store ile bir Hdınsight kümesi oluşturmayı** bölümüne [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Hdınsight'ta Hive tablosu oluşturma
Artık Azure Machine Learning Studio'da hello önceki adımda Azure Data Lake Store'da depolanan hello verileri kullanarak hello Hdınsight kümesinde kullanılan Hive tabloları toobe oluşturun. Yeni oluşturduğunuz Hdınsight kümesi toohello gidin. Tıklatın **ayarları** --> **özellikleri** --> **küme AAD kimlik** --> **ADLS erişimini**, Azure Data Lake Store hesabınızı okuma hello listesinde eklendiğinden emin olun, yazma ve yürütme hakları. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Ardından **Pano** sonraki toohello **ayarları** düğmesi ve bir pencere açılır. Tıklatın **Hive görünümü** hello hello sayfa ve sağ üst köşesindeki hello görürsünüz **sorgu Düzenleyicisi'ni**.

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Hive betikleri toocreate aşağıdaki hello tablo yapıştırın. veri kaynağının Hello konumdur bu şekilde Azure Data Lake Store başvurusu: **adl://data_lake_store_name.azuredatalakestore.net:443/klasör_adı/dosya_adı**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


Merhaba sorgu çalışması sona erdiğinde, hello sonuçlar şöyle görürsünüz:

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Derleme ve Azure Machine Learning Studio'da modelleri dağıtma
Biz hazır toobuild sunulmuştur ve Azure Machine Learning ile bir ipucu Ücretli olsun veya olmasın tahmin modeli dağıtın. Merhaba stratified örnek veri olduğundan bu ikili sınıflandırma kullanılan hazır toobe (veya ipucu) sorun. çok sınıflı sınıflandırma (tip_class) kullanarak Tahmine dayalı modelleri hello ve regresyon (tip_amount) ayrıca oluşturulmuş ve Azure Machine Learning Studio ile dağıtılır, ancak burada yalnızca nasıl toohandle hello örneği kullanarak izin ver hello ikili sınıflandırma modeli gösteriyoruz.

1. Azure hello kullanarak ML Hello Veri Al **veri içeri aktarma** modülü, hello kullanılabilir **veri giriş ve çıkış** bölümü. Daha fazla bilgi için bkz: Merhaba [veri içeri aktarma modülü](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) başvuru sayfası.
2. Seçin **Hive sorgusu** hello olarak **veri kaynağı** hello içinde **özellikleri** paneli.
3. Merhaba Hive betiği aşağıdaki Yapıştır hello **Hive veritabanı sorgusu** Düzenleyicisi
   
        select * from nyc_stratified_sample;
4. Merhaba URI, Hdınsight kümesi (Bu Azure Portalı'nda bulunabilir), Hadoop kimlik bilgileri, çıktı verilerini Azure depolama hesabı anahtarı/ad/kapsayıcı adı ve konumu girin.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

Hive tablodan veri okunurken bir ikili sınıflandırma deneme örneği hello aşağıdaki çizimde gösterilmiştir.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

Merhaba deneme oluşturulduktan sonra tıklatın **Web hizmetinin ayarı** --> **Tahmine dayalı Web hizmeti**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

Tamamlandığında, deneme, Puanlama otomatik olarak oluşturulan çalışma hello tıklatın **Web hizmeti Dağıt**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

Merhaba web hizmeti Pano kısa süre içinde görüntülenir:

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Özet
Bu kılavuzu izleyerek Azure Data Lake içinde ölçeklenebilir uçtan uca çözümler oluşturmak için bir veri bilimi ortamı oluşturdunuz. Bu ortamı kullanılan tooanalyze hello veri bilimi işlemi, veri alım model eğitim üzerinden gelen, hello kurallı adımlarında alma büyük ortak bir dataset, ve ardından hello toohello dağıtımını model bir web hizmeti olarak. U-SQL kullanılan tooprocess oluştu, araştırın ve hello veri örneği. Python ve Hive Azure Machine Learning Studio toobuild ile kullanılan ve Tahmine dayalı modelleri dağıtın.

## <a name="whats-next"></a>Sırada ne var?
öğrenme yolu için hello [takım veri bilimi işlem (TDSP)](http://aka.ms/datascienceprocess) Bağlantılar tootopics her açıklayan adım analytics işlem Gelişmiş hello sağlar. İzlenecek yollar üzerinde hello dökümü bir dizi vardır [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md) bu gösterim nasıl sayfa toouse kaynakları ve çeşitli Tahmine dayalı analiz senaryolarda Hizmetleri:

* [eylemin Hello takım veri bilimi işlemi: SQL Data Warehouse kullanma](machine-learning-data-science-process-sqldw-walkthrough.md)
* [eylemin Hello takım veri bilimi işlemi: Hdınsight Hadoop kümeleri kullanma](machine-learning-data-science-process-hive-walkthrough.md)
* [Merhaba takım veri bilimi işlem: SQL Server kullanma](machine-learning-data-science-process-sql-walkthrough.md)
* [Azure Hdınsight'ta Spark veri bilimi işlemi hello kullanma konusuna genel bakış](machine-learning-data-science-spark-overview.md)

