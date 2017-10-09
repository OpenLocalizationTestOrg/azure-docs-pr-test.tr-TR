---
title: "bir Hadoop aaaExplore veri kümesi ve Azure Machine Learning modellerini oluşturun | Microsoft Docs"
description: "Bir Hdınsight Hadoop kullanan bir uçtan uca senaryo için Hello takım veri bilimi işlemi kullanarak toobuild küme ve genel kullanıma açık bir veri kümesini kullanarak bir modeli dağıtın."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>eylemin Hello takım veri bilimi işlemi: kullanım Azure Hdınsight Hadoop kümeleri
Bu kılavuzda, kullandığımız hello [takım veri bilimi işlem (TDSP)](data-science-process-overview.md) bir uçtan uca senaryoyu kullanarak bir [Azure Hdınsight Hadoop kümesi](https://azure.microsoft.com/services/hdinsight/) toostore, araştırın ve özellik hello mühendislik verileri genel olarak kullanılabilir [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) hello veri örnek veri kümesi ve toodown. Merhaba veri modellerinin Azure Machine Learning toohandle çok sınıflı ve ikili sınıflandırma ve regresyon Tahmine dayalı görevlerle oluşturulur.

Gösteren nasıl toohandle veri işleme için Hdınsight Hadoop kullanarak benzer bir senaryo için daha büyük bir (1 terabayttan küçük) veri kümeleri için bkz [takım veri bilimi işlem - 1 TB veri kümesiüzerindeAzureHdınsightHadoopkümelerikullanarak](machine-learning-data-science-process-hive-criteo-walkthrough.md).

Olası toouse IPython not defteri tooaccomplish hello hello 1 TB veri kümesini kullanarak sunulan hello izlenecek görevler de olabilir. Bu yaklaşım başvurun tootry gibi hello kullanıcılar [Criteo izlenecek bir Hive ODBC bağlantısı kullanarak](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) konu.

## <a name="dataset"></a>NYC ücreti dönüşleri Dataset açıklaması
Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış virgülle ayrılmış değerler (CSV) dosyaları (~ 48 GB sıkıştırılmamış), 173 milyondan fazla kapsayan tek tek dönüşleri ve hello fares her seyahat için ücretli. Her seyahat kayıt hello alma ve teslim konumu ve zaman, anonim korsan (sürücü) lisans numarası ve medallion (ücreti'nın benzersiz kimliği) numarasını içerir. Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:

1. Merhaba 'trip_data' CSV dosyaları yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntıları içerir. Birkaç örnek kayıt şunlardır:
   
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

Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti hello alanlarının oluşur: medallion, korsan\_lisans ve alma\_datetime.

Tüm tooget hello ayrıntıları ilgili tooa belirli seyahat, yeterli toojoin üç anahtarlara sahip olduğu: "medallion" Merhaba "korsan saldırılarına\_lisans" ve "alma\_datetime".

Bunları Hive tablolara kısa süre içinde depolarız zaman biz hello veri bazı ayrıntılar açıklanmaktadır.

## <a name="mltasks"></a>Tahmin görev örnekleri
Veri yaklaşan, kendi analize dayalı toomake istediğiniz tahminleri hello tür belirleme işleminize tooinclude gerekir hello görevleri açıklamak yardımcı olur.
Biz bu kılavuzda, formülasyonu hello üzerinde temel adres tahmin sorunları üç örnekler *İpucu\_tutar*:

1. **İkili sınıflandırma**: bir ipucu bir seyahat, yani ödenmiş olup olmadığına bakılmaksızın tahmin bir *İpucu\_tutar* büyük $0 pozitif bir örnektir küçük, ancak bir *İpucu\_tutar* 0 / negatif bir örnektir.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Çok sınıflı sınıflandırma**: toopredict hello ipucu tutarlar aralığını Ücretli hello seyahat için. Biz hello bölmek *İpucu\_tutar* beş depo veya sınıfları:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Regresyon görev**: seyahat için ödenen hello ucunun toopredict hello tutar.  

## <a name="setup"></a>Bir Hdınsight Hadoop kümesi gelişmiş analizler için ayarlama
> [!NOTE]
> Bu genellikle olur bir **yönetici** görev.
> 
> 

Bir Azure ortamı üç adımda Hdınsight kümesi kullanan gelişmiş analiz için ayarlayabilirsiniz:

1. [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md): verileri Azure Blob Storage'da depolamak için bu depolama hesabı kullanılır. Hdınsight kümelerinde kullanılan hello verileri da buradadır.
2. [Azure Hdınsight Hadoop özelleştirme Advanced Analytics işlemi ve teknoloji kümeleri Merhaba](machine-learning-data-science-customize-hadoop-cluster.md). Bu adım, 64-bit Anaconda Python 2.7 kümeyle tüm düğümlerde yüklü bir Azure Hdınsight Hadoop oluşturur. Hdınsight kümenizi özelleştirilirken iki önemli adımlar tooremember vardır.
   
   * Onu oluştururken Hdınsight kümenize ile 1. adımda oluşturulan toolink hello depolama hesabı unutmayın. Bu depolama hesabını hello küme içinde işlenir kullanılan tooaccess verilerdir.
   * Merhaba Küme oluşturulduktan sonra uzaktan erişim toohello hello küme baş düğümüne etkinleştirin. Toohello gidin **yapılandırma** sekmesinde **etkinleştirmek uzak**. Bu adım, uzak oturum açma için kullanılan hello kullanıcı kimlik bilgilerini belirtir.
3. [Bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md): Bu Azure Machine Learning çalışma alanı kullanılan toobuild machine learning modellerini alanıdır. Bu görev, ilk veri keşfi tamamladıktan sonra ve hello Hdınsight kümesi kullanarak örnekleme aşağı değinilmiştir.

## <a name="getdata"></a>Ortak bir kaynaktan Hello Veri Al
> [!NOTE]
> Bu genellikle olur bir **yönetici** görev.
> 
> 

tooget hello [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) dataset ortak konumundan kullandığınız açıklanan hello yöntemlerden herhangi birini [Azure Blob depolama biriminden verileri Taşı tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello veri tooyour makine.

Burada nasıl kullanım AzCopy tootransfer hello verileri içeren dosyalar açıklanmaktadır. toodownload ve AzCopy yükleme sırasında hello yönergeleri izleyerek [hello AzCopy komut satırı yardımcı programı ile çalışmaya başlama](../storage/common/storage-use-azcopy.md).

1. Bir komut istemi penceresinden aşağıdaki AzCopy komutları, değiştirme hello sorun *< path_to_data_folder >* hello istenen hedefle:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Merhaba kopyalama tamamlandıktan sonra toplam 24 sıkıştırılmış dosya seçilen hello veri klasörü şunlardır. Merhaba indirilen dosyaları toohello sıkıştırmasını yerel makinenizde aynı dizin. Sıkıştırılmamış hello dosyalarının bulunduğu hello klasörü not edin. Bu klasör başvurulan tooas hello olacaktır *< yol\_için\_unzipped_data\_dosyaları\>*  aşağıda değil.

## <a name="upload"></a>Merhaba veri toohello varsayılan kapsayıcı Azure Hdınsight Hadoop kümesi karşıya yükle
> [!NOTE]
> Bu genellikle olur bir **yönetici** görev.
> 
> 

Hello aşağıdaki AzCopy komutları, şu parametreler hello Hadoop kümesi oluştururken belirttiğiniz hello gerçek değerlerle ve hello veri dosyalarını şunu hello yerini alır.

* ***&#60; path_to_data_folder >*** makinenizde sıkıştırması açılmış hello veri dosyalarını içeren hello dizin (birlikte yolu)  
* ***&#60; Hadoop küme depolama hesap adı >*** hello Hdınsight kümenizle ilişkilendirilmiş depolama hesabı
* ***&#60; varsayılan kapsayıcı Hadoop küme >*** , küme tarafından kullanılan hello varsayılan kapsayıcı. Bu hello adını not edin hello varsayılan genellikle aynı adı hello küme olarak kendisi hello kapsayıcıdır. Örneğin, "abc123.azurehdinsight.net" Merhaba küme çağrılırsa, hello varsayılan kapsayıcı abc123 ' dir.
* ***&#60; depolama hesabı anahtarı >*** hello depolama hesabının, küme tarafından kullanılan başlangıç anahtarı

Bir komut istemi veya makinenizde bir Windows PowerShell penceresinde, aşağıdaki iki AzCopy komut hello çalıştırın.

Bu komut hello seyahat veri çok yükler***nyctaxitripraw*** hello Hadoop kümesi hello varsayılan kapsayıcısında dizin.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Bu komut hello ücreti verileri çok yükler***nyctaxifareraw*** hello Hadoop kümesi hello varsayılan kapsayıcısında dizin.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

Hello verileri Azure Blob Storage ve hello Hdınsight küme içinde tüketilen hazır toobe şimdi gerekir.

## <a name="#download-hql-files"></a>Hadoop küme baş düğümüne hello günlüğüne ve ve keşif veri analizi için hazırlama
> [!NOTE]
> Bu genellikle olur bir **yönetici** görev.
> 
> 

Merhaba kümesinin keşif veri analizi için ve hello veri örnekleme aşağı tooaccess hello baş düğümü özetlenen hello yordamı izleyin [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

Bu kılavuzda, öncelikli olarak yazılmış sorguları kullanırız [Hive](https://hive.apache.org/), bir SQL benzeri sorgu dili, tooperform ön veri explorations. Merhaba Hive sorguları .hql dosyalarında depolanır. Biz ardından aşağı içinde Azure Machine Learning modeli oluşturmak için kullanılan bu veri toobe örnek.

tooprepare hello küme keşif veri analizi için biz karşıdan hello ilgili Hive komut dosyalarını içeren hello .hql dosyaları [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) hello baş düğümünde tooa yerel dizin (C:\temp). toodo Bu, açık hello **komut istemi** içinden aşağıdaki iki komutu hello küme ve sorunu hello baş düğümüne hello:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Bu iki komutu bu izlenecek yol toohello yerel dizinde gerekli tüm .hql dosyaları indirir ***C:\temp &#92;*** hello baş düğümünde.

## <a name="#hive-db-tables"></a>Hive veritabanı ve aya göre bölümlenmiş tabloları oluşturma
> [!NOTE]
> Bu genellikle olur bir **yönetici** görev.
> 
> 

Şimdi hazır toocreate Hive tablolarını bizim NYC ücreti veri kümesi için duyuyoruz.
Merhaba Hello baş düğümünde hello Hadoop kümesi, açık ***Hadoop komut satırı*** üzerinde hello Masaüstü hello baş düğümü ve hello komutunu girerek hello Hive dizini girin

    cd %hive_home%\bin

> [!NOTE]
> **Bu kılavuzda Hive depo yukarıda hello tüm Hive komutları çalıştırma / directory istemi. Bu yol sorunları otomatik olarak ilgilenebilmek. "Hive dizin istemi" Merhaba terimleri kullanırız "Hive bin / directory istemi" ve bu kılavuzda birbirinin yerine "Hadoop komut satırı".**
> 
> 

Merhaba Hive dizin isteminden komutu Hadoop komut satırı hello baş düğüm toosubmit hello Hive sorgusu toocreate Hive veritabanı ve tablo aşağıdaki hello girin:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Merhaba Merhaba içeriğine işte ***C:\temp\sample\_hive\_oluşturma\_db\_ve\_tables.hql*** Hive veritabanı oluşturan dosya ***nyctaxidb *** ve tabloları ***seyahat*** ve ***ücreti***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Bu Hive betiğini iki tablo oluşturur:

* Merhaba "seyahat" tablo her kıl (sürücü ayrıntıları, toplama zaman, seyahat uzaklığı ve) seyahat ayrıntılarını içerir
* Merhaba "ücreti" tablosu ücreti ayrıntıları (ücreti tutarı, ipucu tutarı, tolls ve ek talepler) içerir.

Bu yordamları ile ek yardıma gereksinim veya tooinvestigate alternatif olanları istiyorsanız hello bölümüne bakın [gönderme Hive sorguları doğrudan gelen hello Hadoop komut satırı ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Bölümler tarafından veri tooHive tablolar yüklenemiyor
> [!NOTE]
> Bu genellikle olur bir **yönetici** görev.
> 
> 

doğal tooenable daha hızlı işleme ve sorgu süreleri kullanırız aya göre bölümleme Hello NYC ücreti veri kümesi vardır. Aşağıdaki PowerShell komutları hello (Merhaba Hive dizininden hello kullanarak verilen **Hadoop komut satırı**) aya göre bölümlenmiş veri toohello "seyahat" ve "ücreti" Hive tabloları yükleyin.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Merhaba *örnek\_hive\_yük\_veri\_tarafından\_partitions.hql* dosyasını içeren hello aşağıdaki **yük** komutları.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Merhaba araştırması işleminde burada kullandığımız Hive sorguları bir dizi yalnızca tek bir bölüm veya yalnızca birkaç bölümlerinin aramayı içeren unutmayın. Ancak bu sorgular arasında hello tüm verileri çalıştırabilirsiniz.

### <a name="#show-db"></a>Merhaba Hdınsight Hadoop kümesi veritabanları Göster
Hdınsight Hadoop kümesi hello Hadoop komut satırı penceresinde, aşağıdaki komut, Hadoop komut satırı hello çalıştırın içinde oluşturulan tooshow hello veritabanlarını:

    hive -e "show databases;"

### <a name="#show-tables"></a>Merhaba nyctaxidb veritabanında Hello Hive tabloları göster
tooshow hello tablolar hello nyctaxidb veritabanında, aşağıdaki komut, Hadoop komut satırı hello çalıştırın:

    hive -e "show tables in nyctaxidb;"

Merhaba tabloları aşağıdaki hello komutu vererek bölümlenir olduğunu doğrulayabilirsiniz:

    hive -e "show partitions nyctaxidb.trip;"

Merhaba, çıktı aşağıda gösterilen beklenen:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

Benzer şekilde, aşağıdaki hello komutu vererek bu hello ücreti tablonun bölümlenme sağlayabilirsiniz:

    hive -e "show partitions nyctaxidb.fare;"

Merhaba, çıktı aşağıda gösterilen beklenen:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Veri keşfi ve Hive özellik Mühendisliği
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Veri keşfi hello ve Hive sorguları kullanarak veri hello Hive tablolara yüklenen gerçekleştirilebilir hello mühendislik görevlerde özellik. Gibi görevleri biz, bu bölümde size yol olduğunu örnekleri şunlardır:

* Her iki tabloda Hello üst 10 kayıtları görüntüleyin.
* Veri dağıtımları değişen zaman pencereleri birkaç alanların keşfedin.
* Veri Kalitesi hello boylam ve enlem alanlarının araştırın.
* Merhaba üzerinde dayalı çok sınıflı ve ikili sınıflandırma etiketleri oluşturmak **İpucu\_tutar**.
* Özellikler hello doğrudan seyahat uzaklıklar bilgi işlem tarafından oluşturur.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Keşfetme: hello üst 10 kayıt tablo seyahat görüntüleyin.
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

hangi hello verilerin benzer toosee her tablodan 10 kayıt inceleyeceğiz. İki sorguları hello Hive dizin isteminde hello Hadoop komut satırı konsol tooinspect hello kayıtlarında ayrı olarak aşağıdaki hello çalıştırın.

tooget ilk ay Merhaba tablonun "seyahat" Merhaba gelen üst 10 kayıtları hello:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello üst 10 kayıt hello ilk ay öğesinden "ücreti" Merhaba tablosundaki:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

Bu genellikle yararlı toosave hello kayıtları tooa kolay görüntüleme için dosyasıdır. Küçük değişiklik toohello sorgu yukarıda bunu gerçekleştirir:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Keşfetme: Görünümü hello her hello 12 bölüm kayıt sayısı
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Dönüş hello sayısı hello takvim yılı sırasında nasıl değişeceğini hello ilginizi çekecektir. Aya göre gruplandırma sağlayan bize toosee dönüşleri bu dağıtımını benzer.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Bu bize hello çıkış sunar:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

Burada, hello ilk sütun hello ay ve hello ikinci dönüş hello sayısı söz konusu ay.

Biz de hello toplam kayıt sayısı, hello Hive dizin isteminde komutu aşağıdaki hello vererek bizim seyahat veri kümesinde sayabilirsiniz.

    hive -e "select count(*) from nyctaxidb.trip;"

Bu verir:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Merhaba seyahat veri kümesi için gösterilen komutları benzer toothose kullanarak Hive sorguları hello Hive dizin isteminde hello ücreti veri kümesi toovalidate hello kayıt sayısı için verebilir.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Bu bize hello çıkış sunar:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Hello tam aynı dönüş sayısı her ay için her iki veri kümesi verdiğini unutmayın. Bu, verileri doğru şekilde yüklendiğinden bu hello hello ilk doğrulama sağlar.

Merhaba ücreti veri kümesindeki kayıtları toplam sayısı Hello sayım yapılabilir hello Hive dizin isteminden aşağıdaki hello komutunu kullanarak:

    hive -e "select count(*) from nyctaxidb.fare;"

Bu verir:

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

Her iki tablodaki kayıtlarının toplam sayısını Hello olduğunu da hello aynı. Bu, verileri doğru şekilde yüklendiğinden bu hello ikinci doğrulama sağlar.

### <a name="exploration-trip-distribution-by-medallion"></a>Araştırması: Medallion seyahat dağıtım
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Bu örnek, belirli bir süre içinde ile 100'den fazla dönüşleri hello medallion (ücreti sayılar) tanımlar. Hello sorgu avantajları hello gelen bölümlenmiş tabloda erişim hello bölüm değişkeniyle söylediğinizde beri **ay**. Merhaba sorgu sonuçları dilini tooa yerel dosya queryoutput.tsv `C:\temp` hello baş düğüm üzerinde.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Merhaba içeriğine işte *örnek\_hive\_seyahat\_sayısı\_tarafından\_medallion.hql* İnceleme için dosya.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Merhaba medallion hello NYC ücreti veri kümesindeki bir benzersiz cab tanımlar. Hangi cab hangilerinin belirli bir süre içinde birden çok belirli bir sayıda dönüşleri yapılan isteyerek "meşgul" ayırt edebilirsiniz. Merhaba aşağıdaki örnek tanımlar birden fazla yüzlerce dönüşleri hello ilk üç ay yapılan cab dosyaları ve sorgu sonuçları tooa yerel dosya, C:\temp\queryoutput.tsv kaydeder hello.

Merhaba içeriğine işte *örnek\_hive\_seyahat\_sayısı\_tarafından\_medallion.hql* İnceleme için dosya.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Hello dizin istemi, aşağıdaki sorun hello komutu yığını:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Keşfetme: dağıtım medallion ve hack_license tarafından seyahat
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Bir veri kümesi keşfetme, sık tooexamine hello co-örnek değerler gruplarının sayısına istiyoruz. Bu bölüm bir örnek nasıl toodo Bu dolap ve sürücüleri sağlayın.

Merhaba *örnek\_hive\_seyahat\_sayısı\_tarafından\_medallion\_license.hql* dosya grupları "medallion" ve "hack_license" Merhaba ücreti verileri ve her birleşim sayısını döndürür. İçeriğini aşağıda verilmiştir.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Bu sorgu, cab ve dönüş azalan sayısına göre sıralanmış belirli sürücü birleşimleriyle döndürür.

Dizin istemi Hello Hive, çalıştırın:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

Merhaba sorgu sonuçları tooa yerel dosya C:\temp\queryoutput.tsv yazılır.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Araştırması: Geçersiz boylam/enlem kayıtlarını denetleyerek veri kalitesini değerlendirme
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Ortak amacı keşif veri analizi, geçersiz veya hatalı kayıt çıkışı tooweed ' dir. Merhaba bu bölümdeki örnek ya da hello boylam veya enlem alanları kadar hello NYC alanı dışında bir değer içeren olup olmadığını belirler. Bu tür kayıtları bir hatalı boylam enlem değerlere sahip olası olduğundan, bunları toobe olan herhangi bir veri modelleme için kullanılan tooeliminate istiyoruz.

Merhaba içeriğine işte *örnek\_hive\_kalite\_assessment.hql* İnceleme için dosya.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


Dizin istemi Hello Hive, çalıştırın:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Merhaba *-S* Bu komutta yer alan bağımsız değişkeni hello durum ekran hello harita/azaltın Hive işleri çıktısını gizler. Merhaba ekran Yazdır hello Hive sorgusu çıktıyı daha okunabilir hale getirir çünkü bu yararlı olur.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Araştırması: Seyahat ipuçları ikili sınıfı dağıtımları
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Hello özetlenen hello ikili sınıflandırma sorunu için [tahmin görev örnekleri](machine-learning-data-science-process-hive-walkthrough.md#mltasks) bölümüne bir ipucu veya verilen bu yararlı tooknow olup. Bu dağıtımı ipuçları, ikili şöyledir:

* verilen İpucu (sınıf 1, İpucu\_> $0 tutar)  
* İpucu yok (sınıfı 0, İpucu\_tutar = $0).

Merhaba *örnek\_hive\_Eğimli\_frequencies.hql* aşağıda gösterilen dosya yapar.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

Dizin istemi Hello Hive, çalıştırın:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Araştırması: Merhaba çok sınıflı ayarında sınıf dağıtımları
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Hello özetlenen hello çok sınıflı sınıflandırma sorunu için [tahmin görev örnekleri](machine-learning-data-science-process-hive-walkthrough.md#mltasks) bölümünde bu veri kümesi de tooa doğal sınıflandırma burada biz gibi hello ipuçları verilen toopredict hello miktarını kendisini uygundur. Biz depo toodefine ipucu aralıkları hello sorguda kullanabilirsiniz. tooget Merhaba hello için sınıf dağıtımları çeşitli ipucu aralıkları, hello kullanırız *örnek\_hive\_İpucu\_aralığı\_frequencies.hql* dosya. İçeriğini aşağıda verilmiştir.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Hadoop komut satırı konsolundan komutu aşağıdaki hello çalıştırın:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Araştırması: İki boylam enlem konumlar arasında doğrudan uzaklığı işlem
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Merhaba doğrudan uzaklık ölçüsü sağlar bize toofind hello tutarsızlık ve hello arasındaki çıkışı gerçek seyahat uzaklığı. Bu özellik bir yolcu küçük olabilir üzerine gelerek becerisiyle Biz bu hello sürücüsünü şekil, büyük olasılıkla tootip kasıtlı olarak gerçekleştirilecek bunları tarafından kadar uzun yol.

Gerçek seyahat uzaklığı ve hello arasında toosee hello karşılaştırma [Haversine uzaklığı](http://en.wikipedia.org/wiki/Haversine_formula) iki boylam enlem noktaları arasında (Merhaba "mükemmel daire" uzaklığı) hello trigonometrik işlevler Hive içinde bu nedenle kullanırız:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

Sorguda hello yukarıdaki R Merhaba Dünya mil cinsinden hello yarıçapı ve pi dönüştürülmüş tooradians. Merhaba boylam enlem noktaları hello NYC alanı gölgeden uzak olan "filtrelenmiş" tooremove değerleri olduğuna dikkat edin.

Bu durumda, "queryoutputdir" adlı bizim sonuçları tooa dizin yazma. Aşağıda gösterilen komutların Hello dizisi önce bu çıktı dizini oluşturur ve hello Hive komutu çalıştırır.

Dizin istemi Hello Hive, çalıştırın:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Merhaba sorgu sonuçları too9 Azure BLOB'ların yazılır ***queryoutputdir/000000\_0*** çok ***queryoutputdir/000008\_0*** hello varsayılan kapsayıcı hello Hadoop kümesi altında.

Merhaba tek tek bloblar toosee hello boyutu, komut hello Hive dizin isteminden aşağıdaki hello çalıştırın:

    hdfs dfs -ls wasb:///queryoutputdir

belirli bir dosya toosee Merhaba içeriğine söyleyin 000000\_0, Hadoop'ın kullanırız `copyToLocal` komutu, böylece.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal`büyük dosyalar için çok yavaş olabilir ve bunları ile kullanım için önerilmez.  
> 
> 

Biz hello kullanarak Azure Machine Learning içinde hello verileri araştırmak bir Azure blob bulunan verilere erişmenin önemli bir avantajı olan [veri içeri aktarma] [ import-data] modülü.

## <a name="#downsample"></a>Örnek veriler ve yapı modellerinde Azure Machine Learning
> [!NOTE]
> Bu genellikle olur bir **veri Bilimcisi** görev.
> 
> 

Merhaba keşif verileri analiz aşaması sonra artık Azure Machine Learning modellerini oluşturmak için hazır toodown örnek hello veri duyuyoruz. Bu bölümde, nasıl toouse bir Hive sorgusu hello sonra erişilen toodown örnek hello verileri olan gösteriyoruz [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde.

### <a name="down-sampling-hello-data"></a>Merhaba veri örnekleme aşağı
Bu yordamda iki adımı vardır. İlk biz hello katılma **nyctaxidb.trip** ve **nyctaxidb.fare** tüm kayıtları mevcut üç anahtarları tablolarda: "medallion", "korsan saldırılarına\_lisans", ve "alma\_datetime". Biz sonra bir ikili sınıflandırma etiketi oluşturmak **Eğimli** ve birden çok sınıf sınıflandırma etiketini **İpucu\_sınıfı**.

toobe mümkün toouse hello örneklenen verileri doğrudan hello aşağı [veri içeri aktarma] [ import-data] modül Azure Machine Learning ile gerekli toostore hello sorgu tooan iç Hive tablosu yukarıda hello sonuçlarını olduğu. Aşağıda, biz iç bir Hive tablosu oluşturmak ve içeriğini örneklenen verileri aşağı birleştirilmiş hello ile doldurun.

Merhaba sorgusunu uygular standart Hive işlevleri doğrudan toogenerate hello saat, gün, hafta içi (Pazartesi 1 anlamına gelir ve Pazar 7 anlamına gelir) başlangıç hello yılın haftası "toplama\_datetime" alan ve hello alımı ve dropoff arasındaki hello doğrudan uzaklığı konumları. Kullanıcılar çok başvurabilir[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) böyle işlevlerin tam listesi için.

Sorgu hello sonra hello sorgu sonuçları hello Azure Machine Learning Studio sığabilecek böylece örnekleri hello veri aşağı. Yalnızca yaklaşık %1 hello özgün veri kümesinin Studio hello alınır.

Merhaba içeriğine aşağıda verilmiştir *örnek\_hive\_hazırlama\_için\_aml\_full.hql* veri modeli Azure Machine Learning ile derleme hazırlar dosya.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

toorun hello Hive dizininden bu sorguyu iste:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Şimdi bir iç tablosu "Merhaba kullanılarak erişilebilen nyctaxidb.nyctaxi_downsampled_dataset" sahibiz [veri içeri aktarma] [ import-data] Azure Machine Learning modülünden. Bu veri kümesi Machine Learning modeli oluşturmak için Ayrıca, kullanabiliriz.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Azure Machine Learning tooaccess hello örneklenen verileri aşağı Hello veri içeri aktarma modülü kullanın
Merhaba Hive sorguları verme için önkoşul olarak [veri içeri aktarma] [ import-data] modül Azure Machine Learning, ihtiyacımız tooan Azure Machine Learning çalışma alanına erişmek ve hello toohello kimlik bilgilerini erişim Küme ve onun ilişkili depolama hesabı.

Merhaba ilgili bazı Ayrıntılar [veri içeri aktarma] [ import-data] modülü ve hello parametreleri tooinput:

**HCatalog sunucusu URI**: hello küme adı olduğundan abc123 sonra yalnızca budur: https://abc123.azurehdinsight.net

**Hadoop kullanıcı hesabı adı** : hello küme için seçilen hello kullanıcı adı (**değil** hello uzaktan erişim kullanıcı adı)

**Hadoop kullanıcı hesabı parolasını** : hello küme için seçilen hello parola (**değil** hello uzaktan erişim parola)

**Çıktı verilerini konumunu** : Bu toobe Azure seçilir.

**Azure depolama hesabı adı** : hello kümesi ile ilişkili hello varsayılan depolama hesabı adı.

**Azure kapsayıcı adı** : Bu hello varsayılan kapsayıcı hello küme adıdır ve olduğundan genellikle hello aynı hello küme adı olarak. "Abc123" adlı bir küme için yalnızca abc123 budur.

> [!IMPORTANT]
> **Hello kullanarak tooquery istediğimiz herhangi bir tablo [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde bir iç tablosu olması gerekir.** Bir ipucu D.db veritabanındaki bir tablo T bir iç tablosu ise belirlemek için aşağıdaki gibidir.
> 
> 

Hello dizin istemi, sorunu hello komutu yığını:

    hdfs dfs -ls wasb:///D.db/T

Bir iç tablosu Hello tablodur ve onu doldurulur, içeriği burada gösterilecek gerekir. Bir tablo bir iç tablosu olup olmadığını toouse hello Azure Storage Gezgini olan başka bir şekilde toodetermine. Merhaba tablo adına göre filtre uygulamak ve toonavigate toohello varsayılan kapsayıcı hello küme adını kullanın. Merhaba tablo ve içeriği gösterilirse, bu bir iç tablosu olduğunu doğrular.

Merhaba Hive sorgusu ve hello bir anlık görüntüsünü işte [veri içeri aktarma] [ import-data] Modülü:

![Veri içeri aktarma modülü için Hive sorgusu](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Örneklenen verileri hello varsayılan kapsayıcısında yer alıyor bizim aşağı itibaren hello Azure Machine Learning elde edilen Hive sorgusu çok basit bir işlemdir ve yalnızca olduğunu not bir "seçin * nyctaxidb.nyctaxi gelen\_altörnekleme\_veri".

Merhaba veri kümesi, başlangıç noktası Machine Learning model oluşturmaya yönelik hello olarak artık kullanılabilir.

### <a name="mlmodel"></a>Azure Machine Learning modellerini Derleme
Artık mümkün tooproceed toomodel yapı ve model dağıtımda duyuyoruz [Azure Machine Learning](https://studio.azureml.net). Merhaba veri hazır bize için yukarıda tanımlanan hello tahmin sorunları adresleme içinde toouse:

**1. İkili sınıflandırma**: olsun veya olmasın bir ipucu Ücretli bir seyahat için toopredict.

**Kullanılan öğrenen:** iki sınıflı Lojistik regresyon

a. Bu sorun için hedef (veya sınıfı) etiketimizi "Eğimli". Özgün aşağı örneklenen kümemize bu sınıflandırma deneme için hedef sızıntıları olan birkaç sütun içeriyor. Özellikle: İpucu\_sınıfı, İpucu\_miktarı ve toplam\_zaman sınama sırasında kullanılamaz hello hedef etiketi açığa bilgilerini tutar. Biz bu sütunları hello kullanarak dikkate kaldırmak [Select Columns in Dataset sütun] [ select-columns] modülü.

Merhaba anlık aşağıdaki ipucu verilen seyahat için ödeme bizim deneme toopredict gösterir.

![Deneme anlık görüntü](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. Bu deneme için bizim hedef etiket dağıtımların yaklaşık 1:1 yoktu.

Merhaba anlık görüntü aşağıdaki hello ikili sınıflandırma sorunu için ipucu sınıfı etiketleri hello dağılımını gösterir.

![İpucu sınıfı etiketleri dağıtılması](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

Sonuç olarak, size bir AUC 0.987, hello aşağıdaki çizimde gösterildiği gibi edinin.

![AUC değeri](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Çok sınıflı sınıflandırma**: toopredict hello aralık hello kullanarak önceden hello seyahat için ücretli ipucu tutarlarının tanımlanan sınıflar.

**Kullanılan öğrenen:** çok sınıflı Lojistik regresyon

a. Bu sorun için hedef (veya sınıfı) etiketimizi olan "İpucu\_sınıfı" hangi alabilir beş değerlerden (0,1,2,3,4). Merhaba ikili sınıflandırma durumda olduğu gibi bu deneme için hedef sızıntıları olan birkaç sütunlar sahip. Özellikle: eğimli, İpucu\_tutarı, toplam\_zaman sınama sırasında kullanılamaz hello hedef etiketi açığa bilgilerini tutar. Biz hello kullanarak bu sütunları kaldırın [Select Columns in Dataset sütun] [ select-columns] modülü.

Merhaba anlık görüntü gösterilmektedir hangi Kutusu'na ipucu olan büyük olasılıkla toofall bizim deneme toopredict (sınıfı 0: ipucu = $0, 1 sınıfı: ipucu > 0 ve ipucu < = $5, sınıf 2: ipucu > $5 ve ipucu < = $10, sınıf 3: ipucu > $10 ve ipucu < = $20 Sınıf 4: > $20 ipucu)

![Deneme anlık görüntü](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Şimdi bizim gerçek test sınıfı dağıtım nasıl göründüğünü gösterir. Sınıf 0 ve sınıf 1 yaygın olsa da, hello diğer sınıflar nadir olduğunu bakın.

![Test sınıfı dağıtım](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. Bu deneme için bizim tahmin accuracies karışıklığı matris toolook kullanırız. Bu örnek aşağıda gösterilmiştir.

![Karışıklığı Matrisi](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Bizim sınıfı accuracies hello yaygın sınıfları oldukça iyi durumdayken hello modeli Tebrikler "öğrenme" hello nadir sınıflarında yapmaz olduğunu unutmayın.

**3. Regresyon görev**: seyahat için ödenen ucunun toopredict hello tutar.

**Kullanılan öğrenen:** Boosted karar ağacı

a. Bu sorun için hedef (veya sınıfı) etiketimizi olan "İpucu\_tutar". Bizim hedef sızıntıları bu durumda: eğimli, İpucu\_sınıfı, toplam\_tutar; genellikle zaman sınama sırasında kullanılamıyor hello ipucu tutar hakkında bilgi ortaya bu değişkenleri. Biz hello kullanarak bu sütunları kaldırın [Select Columns in Dataset sütun] [ select-columns] modülü.

Başlangıç anlık görüntü belows ipucu verilen hello bizim deneme toopredict hello miktarını gösterir.

![Deneme anlık görüntü](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Regresyon sorunları, biz hello tahminlerin karesi alınmış hello hata bakarak hello accuracies bizim öngörme ölçmek, katsayısı hello ve gibi hello. Bunlar aşağıdaki gösteriyoruz.

![Tahmin istatistikleri](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Merhaba hakkında 0.709, katsayısı olduğunu görmek yaklaşık hello farkı %71 olduğunu belirtmek bizim modeli katsayısını tarafından açıklanmıştır.

> [!IMPORTANT]
> Azure Machine Learning hakkında daha fazla toolearn ve nasıl tooaccess ve kullanmak, lütfen çok bakın[Machine Learning nedir?](machine-learning-what-is-machine-learning.md). Machine Learning denemelerini Azure Machine learning'de bir grup ile çalmak için çok faydalı bir hello kaynaktır [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/). Merhaba galeri denemeler genişliğine kapsayan ve Azure Machine Learning yetenekleri hello aralığı içine kapsamlı bir giriş sağlar.
> 
> 

## <a name="license-information"></a>Lisans bilgileri
Bu örnek gözden geçirme ve eşlik eden betikleri hello MIT lisansı altında Microsoft tarafından paylaşılır. Lütfen hello LICENSE.txt dosyayı daha fazla ayrıntı için GitHub üzerindeki hello örnek kodu hello dizininde iade edin.

## <a name="references"></a>Başvurular
• [Andrés Monroy NYC ücreti dönüşleri indirme sayfası](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC ait ücreti seyahat veri Chris Whong tarafından](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC ücreti ve Limousine devreye sokmak araştırma ve istatistikleri](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
