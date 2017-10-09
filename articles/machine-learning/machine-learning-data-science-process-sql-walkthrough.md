---
title: "aaaBuild ve bir Azure VM üzerinde SQL Server kullanarak bir makine öğrenimi modeline dağıtma | Microsoft Docs"
description: "Gelişmiş analizler işlemi ve eylem teknoloji"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>eylemin Hello takım veri bilimi işlemi: SQL Server kullanma
Bu öğreticide, oluşturma ve makine öğrenimi modeline dağıtma hello işleminde size kılavuzluk SQL Server ve genel kullanıma açık bir veri kümesi--hello kullanarak [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) veri kümesi. Merhaba yordamdan sonraki standart veri bilimi akışı: alma ve hello verileri araştırmak, mühendislik özellikleri toofacilitate öğrenme, sonra yapı ve model dağıtma.

## <a name="dataset"></a>NYC ücreti veri kümesi tanımı dönüşleri
Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış CSV dosyaları (~ 48 GB sıkıştırılmamış), 173 milyondan fazla kapsayan tek tek dönüşleri ve hello fares her seyahat için ücretli. Her seyahat kayıt hello alma ve teslim konumu ve zaman, anonim korsan (sürücü) lisans numarası ve medallion (ücreti'nın benzersiz kimliği) numarasını içerir. Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:

1. Merhaba 'trip_data' CSV yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntıları içerir. Birkaç örnek kayıt şunlardır:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Merhaba 'trip_fare' CSV ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat için ücretli hello ücreti ayrıntılarını içerir. Birkaç örnek kayıt şunlardır:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti hello alanlarının oluşur: medallion, korsan\_lisans ve alma\_datetime.

## <a name="mltasks"></a>Tahmin görev örnekleri
Merhaba üzerinde temel üç tahmin sorunları formüle *İpucu\_tutar*, yani:

1. İkili sınıflandırma: bir ipucu bir seyahat, yani ödenmiş olup olmadığına bakılmaksızın tahmin bir *İpucu\_tutar* büyük $0 pozitif bir örnektir küçük, ancak bir *İpucu\_tutar* 0 / negatif bir örnektir.
2. Çok sınıflı sınıflandırma: ipucu toopredict hello aralığı Ücretli hello seyahat için. Biz hello bölmek *İpucu\_tutar* beş depo veya sınıfları:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Regresyon görevi: seyahat için ödenen ucunun toopredict hello tutar.  

## <a name="setup"></a>Kurulum hello Azure veri bilimi ortamı Gelişmiş analiz için
Hello gördüğünüz [ortamınıza planlama](machine-learning-data-science-plan-your-environment.md) Kılavuzu, azure'da hello NYC ücreti dönüşleri veri kümesi ile çeşitli seçenekler toowork vardır:

* Azure BLOB'ları hello verilerde sonra Azure Machine Learning modeli ile çalışma
* SQL Server veritabanı sonra Azure Machine Learning modelinde içine Hello veri yükleme

Bu öğreticide biz hello veri tooa SQL sunucusu, veri keşfi, özellik paralel toplu olarak alma işlemi gösterilmektedir mühendislik ve aşağı örnekleme SQL Server Management Studio'yu kullanarak yanı sıra IPython Not Defteri kullanarak. [Örnek komutlar](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) ve [IPython not defterlerini](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) Github'da paylaşılır. Bir örnek IPython not defteri toowork hello verileri Azure BLOB'ları da hello kullanılabilir aynı konumu.

Azure veri bilimi ortamınızı tooset:

1. [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md)
2. [Bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md)
3. [Bir veri bilimi sanal makine sağlama](machine-learning-data-science-setup-sql-server-virtual-machine.md), bir SQL sunucusu ve bir IPython dizüstü sunucusu sağlar.
   
   > [!NOTE]
   > Merhaba örnek komut dosyaları ve IPython not defterlerini indirilen tooyour veri bilimi sanal makine hello Kurulum işlemi sırasında olacaktır. Merhaba VM yükleme sonrası betik tamamlandığında hello örnekleri VM Belge Kitaplığı'nda olur:  
   > 
   > * Örnek komut dosyaları:`C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Örnek IPython dizüstü bilgisayarlar:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   Burada `<user_name>` VM Windows oturum açma adıdır. Toohello örnek klasörler olarak başvuruda bulunacak **örnek betikler** ve **örnek IPython not defterlerini**.
   > 
   > 

Merhaba veri kümesi boyutu, veri kaynağı konumu ve hello seçili Azure hedef ortam bağlı olarak, bu senaryo çok benzer[senaryo \#5: yerel dosyaları büyük bir veri kümesini hedef Azure VM'deki SQL Server](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Ortak kaynağından Hello Veri Al
tooget hello [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) dataset ortak konumundan kullandığınız açıklanan hello yöntemlerden herhangi birini [Azure Blob depolama biriminden verileri Taşı tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello veri tooyour yeni sanal makine.

AzCopy kullanarak toocopy hello verileri:

1. Tooyour sanal makine (VM) oturum
2. Merhaba sanal makinenin veri diski yeni bir dizin oluşturun (Not: hello hello bir veri diski olarak VM ile birlikte geçici Disk kullanmayın).
3. Bir komut istemi penceresinde aşağıdaki Azcopy komut satırı, (2)'de oluşturduğunuz veri klasörünüz < path_to_data_folder > yerine hello çalıştırın:
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Merhaba AzCopy tamamlandığında 24 toplam CSV dosyaları sıkıştırılmış (seyahat için 12\_veri ve seyahat için 12\_ücreti) hello veri klasörde olmalıdır.
4. Merhaba indirilen dosyaları ayıklayın. Sıkıştırılmamış hello dosyalarının bulunduğu hello klasörü not alın. Bu klasör başvurulan tooas hello olacaktır < yol\_için\_veri\_dosyaları\>.

## <a name="dbload"></a>SQL Server veritabanına veri toplu İçeri Aktar
Merhaba, yükleme ve aktarma büyük miktarlarda veri tooan SQL veritabanı ve sonraki sorguları Performans kullanılarak geliştirilebilir *bölümlenmiş tabloları ve görünümleri*. Bu bölümde, biz açıklandığı hello yönergeleri [paralel toplu veri içeri aktarma kullanarak SQL bölüm tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate paralel bölümlenmiş tablolar halinde yeni bir veritabanı ve yük hello verileri.

1. Tooyour VM açmışken Başlat **SQL Server Management Studio**.
2. Windows kimlik doğrulaması kullanarak bağlanın.
   
    ![SSMS bağlanma][12]
3. Eğer henüz hello SQL Server kimlik doğrulama modu değiştirildi ve yeni bir SQL oturum açma kullanıcı oluşturulan adlı hello betik dosyasını açma **değiştirme\_auth.sql** hello içinde **örnek betikler** klasör. Merhaba varsayılan kullanıcı adı ve parolasını değiştirin. Tıklatın **! Yürütme** hello araç toorun hello komut.
   
    ![Komut dosyası yürütme][13]
4. Doğrulayın ve/veya SQL Server veritabanlarını yeni oluşturulan varsayılan veritabanı ve günlük klasörleri tooensure bir veri diski depolanacak hello değiştirin. datawarehousing yükler için en iyi duruma getirilmiş hello SQL Server VM görüntüsü veri ve günlük disklerle önceden yapılandırılmıştır. VM'yi bir veri diski içermeyen ve yeni sanal sabit diskler hello VM Kurulum işlemi sırasında eklediyseniz hello varsayılan klasörler aşağıdaki gibi değiştirin:
   
   * Sol paneli ve tıklatın hello sağ hello SQL Server adı **özellikleri**.
     
       ![SQL Server özellikleri][14]
   * Seçin **veritabanı ayarlarını** hello gelen **sayfa Seç** toohello sol listeleyin.
   * Doğrulayın ve/veya hello değiştirme **veritabanı varsayılan konumları** toohello **veri diski** tercih ettiğiniz konumları. Yeni veritabanları hello varsayılan konumu ayarlarını oluşturduysanız bulunduğu budur.
     
       ![SQL veritabanı Varsayılanları][15]  
5. toocreate yeni bir veritabanı ve dosya grupları toohold kümesi hello bölümlenmiş tablolar, açık hello örnek betik **oluşturma\_db\_default.sql**. Merhaba betik adlı yeni bir veritabanı oluşturacak **TaxiNYC** ve hello varsayılan veri konumu 12 grupları. Her dosya seyahat bir aylık tutacak\_veri ve seyahat\_masrafları veri. İsterseniz Hello veritabanı adını değiştirin. Tıklatın **! Yürütme** toorun hello komut dosyası.
6. Ardından, iki bölüm tabloları hello seyahat için bir tane oluşturun\_veri ve hello seyahat için başka bir\_ücreti. Açık hello örnek betik **oluşturma\_bölümlenmiş\_table.sql**, hangi olur:
   
   * Bir bölüm işlevi toosplit hello veri aya göre oluşturun.
   * Bir bölüm düzeni toomap her ayın veri tooa farklı dosya grubu oluşturun.
   * İki bölümlenmiş tabloları eşlenen toohello bölüm düzeni oluşturma: **nyctaxi\_seyahat** hello seyahat tutacak\_veri ve **nyctaxi\_ücreti** hello seyahat tutar \_masrafları veri.
     
     Tıklatın **! Yürütme** toorun hello komut dosyası ve hello bölümlenmiş tablolar oluşturun.
7. Merhaba, **örnek betikler** klasörü, iki örnek PowerShell betik veri tooSQL Server tabloları paralel Toplu Almalar toodemonstrate sağlanan vardır.
   
   * **BCP\_paralel\_generic.ps1** bir genel komut dosyası tooparallel toplu içeri aktarma bir tabloya verilerdir. Bu komut dosyası tooset hello giriş ve hedef değişkenleri hello yorum hello komut satırlarında belirtildiği şekilde değiştirin.
   * **BCP\_paralel\_nyctaxi.ps1** hello genel komut dosyası, önceden yapılandırılmış bir sürümüdür ve her iki tabloyu hello NYC ücreti dönüş verileri için kullanılan tootooload olabilir.  
8. Sağ hello **bcp\_paralel\_nyctaxi.ps1** betik adı ve tıklatın **Düzenle** tooopen PowerShell içinde. Gözden geçirme hello önceden değişkenleri ve according tooyour seçili veritabanı adı, giriş veri klasörü, hedef günlük klasörü ve yolları toohello örnek biçim dosyalarını değiştirme **nyctaxi_trip.xml** ve **nyctaxi\_ Fare.xml** (hello sağlanan **örnek betikler** klasörü).
   
    ![Toplu Veri Al][16]
   
    Merhaba kimlik doğrulama modu seçin, varsayılan Windows kimlik doğrulaması. Merhaba araç toorun Hello yeşil oku tıklatın. Merhaba betik 24 toplu içeri aktarma işlemleri paralel 12 bölümlenmiş her tablo için başlatır. Yukarıdaki küme olarak hello SQL Server varsayılan veri klasörü açarak hello veri içeri aktarma ilerlemesi izleyebilirsiniz.
9. Merhaba PowerShell komut dosyası raporları başlangıç ve bitiş saatleri hello. Tüm içeri aktarmalar tam toplu, bitiş saati başlangıç bildirilir. Yani, hello Toplu Almalar başarılıysa hello hedef günlük klasörü tooverify hello hedef günlük klasöründe herhangi bir hata bildirdi denetleyin.
10. Veritabanınızı artık araştırması, özellik Mühendisliği ve istediğiniz gibi diğer işlemler için hazırdır. Merhaba tabloları toohello göre bölümlenir beri **toplama\_datetime** alan, içeren sorguları **toplama\_datetime** hello koşullarında  **Burada** yan tümcesi hello bölüm düzeni yararlanacaktır.
11. İçinde **SQL Server Management Studio**, sağlanan hello örnek betik keşfedin **örnek\_queries.sql**. Merhaba örnek sorgular, Vurgu hello hiçbirini sorgu satırları ardından tıklatın toorun **! Yürütme** hello araç.
12. Merhaba NYC ücreti dönüş verileri iki ayrı tablolarda yüklenir. tooimprove birleştirme işlemleri tooindex hello tabloları kullanmamanız önerilir. Merhaba örnek komut dosyası **oluşturma\_bölümlenmiş\_index.sql** bölümlenmiş dizinlerini hello bileşik birleştirme anahtarı oluşturur **medallion, korsan\_lisans ve alma\_datetime**.

## <a name="dbexplore"></a>Veri keşfi ve SQL Server'daki özelliği mühendislik
Bu bölümde, veri keşfi ve özellik nesil doğrudan hello SQL sorguları çalıştırarak gerçekleştiririz **SQL Server Management Studio** hello SQL Server veritabanı kullanılarak oluşturulan önceki. Adlandırılmış bir örnek komut dosyası **örnek\_queries.sql** hello sağlanan **örnek betikler** klasör. Merhaba varsayılandan farklı ise hello betik toochange hello veritabanı adı değiştirin: **TaxiNYC**.

Bu alıştırmada, şunları yapacağız:

* Çok bağlanmak**SQL Server Management Studio** ya da Windows kimlik doğrulaması veya SQL kimlik doğrulaması ve hello SQL oturum açma adı ve parola kullanarak.
* Veri dağıtımları değişen zaman pencereleri birkaç alanların keşfedin.
* Veri Kalitesi hello boylam ve enlem alanlarının araştırın.
* Merhaba üzerinde dayalı çok sınıflı ve ikili sınıflandırma etiketleri oluşturmak **İpucu\_tutar**.
* Özellikler oluşturmak ve işlem/seyahat uzaklıklar karşılaştırın.
* Merhaba iki tabloları birleştirme ve kullanılan toobuild modelleri olacaktır rasgele bir örnek ayıklayın.

Hazır tooproceed tooAzure Machine Learning olduğunda ya da görebilirsiniz:  

1. Merhaba nihai SQL sorgu tooextract ve örnek hello veri ve kopyala-yapıştır hello sorguyu doğrudan kaydetmek bir [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde veya
2. Örneklenen hello kalıcı tasarlanan veri modeli içindeki yeni bir veritabanı oluşturmak için toouse planladığınız tablo hello yeni tablo hello kullanılacağını ve [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde.

Bu bölümde biz hello son sorgu tooextract ve örnek hello verilerini kaydeder. Merhaba ikinci yöntem hello gösterilen [veri keşfi ve özellik Mühendisliği IPython Not](#ipnb) bölümü.

Merhaba sayısı hello sayfasındaki satır ve sütunları hızlı doğrulanması için daha önce paralel toplu içeri kullanarak tabloları doldurulmuş,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Araştırması: Medallion seyahat dağıtım
Bu örnek, belirli bir süre içinde ile 100'den fazla dönüşleri hello medallion (ücreti sayılar) tanımlar. Hello sorgu tarafından hello bölümleme düzeni söylediğinizde bu yana bölümlenmiş hello tablo erişimden yararlanan **toplama\_datetime**. Merhaba tam veri kümesini sorgulama hello bölümlenmiş tablosu kullanın ve/veya dizin tarama ayrıca olun.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Keşfetme: dağıtım medallion ve hack_license tarafından seyahat
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Veri Kalitesi değerlendirmesi: yanlış boylam ve/veya enlem ile kayıtlarını doğrulama
Merhaba boylam ve/veya enlem alanların hiçbirini ya da geçersiz bir değer içeriyorsa, bu örnek araştırır (radian derece -90 ile 90 arasında olmalıdır), ya da sahip (0, 0) koordinatları.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Keşfetme: Eğimli vs. Değil Eğimli dönüşleri dağıtım
Bu örnek karşılaştırması belirli bir zaman aralığı (veya hello tam yıl kapsayan varsa hello tam veri kümesi) Eğimli değil Eğimli dönüş hello sayısı bulur. Bu dağıtım için ikili sınıflandırma modelleme daha sonra kullanılan hello ikili etiket dağıtım toobe yansıtır.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Araştırması: Sınıf/Range dağıtım İpucu
Bu örnek hello dağıtımlarında ipucu aralıklarının belirli bir zaman aralığı (veya hello tam yıl kapsayan varsa hello tam veri kümesi) hesaplar. Daha sonra çok sınıflı sınıflandırma model için kullanılacak hello etiket sınıfların hello dağıtım budur.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Keşfi: İşlem ve seyahat uzaklığı Karşılaştır
Bu örnek hello alma ve teslim boylam dönüştürür ve enlem tooSQL Coğrafya noktaları, SQL Coğrafya noktaları fark kullanarak hello seyahat uzaklığı hesaplar ve hello sonuçları karşılaştırma için rastgele bir örneğini döndürür. Merhaba örneği yalnızca daha önce ele hello veri kalitesi değerlendirme sorgu kullanarak toovalid koordinatları hello sonuçlarını sınırlandırır.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Özellik Mühendisliği SQL sorguları
Merhaba etiket oluşturma ve Coğrafya dönüştürme araştırması sorguları bölümü sayım hello kaldırarak kullanılan toogenerate etiketleri/özellikleri de olabilir. Ek özellik Mühendisliği SQL örnekleri hello sağlanan [veri keşfi ve özellik Mühendisliği IPython Not](#ipnb) bölümü. Daha verimli toorun hello özelliği nesil sorguları hello tam veri kümesinin veya büyük bir alt kümesini doğrudan hello SQL Server veritabanı örneği üzerinde çalışan SQL sorgularını kullanarak olur. Merhaba sorguları yürütülebilir içinde **SQL Server Management Studio**, IPython Not Defteri veya herhangi bir geliştirme aracı/erişebileceğiniz ortamında yerel olarak veya uzaktan veritabanı hello.

#### <a name="preparing-data-for-model-building"></a>Model oluşturmanın için verileri hazırlama
Merhaba aşağıdaki birleşimler hello sorgu **nyctaxi\_seyahat** ve **nyctaxi\_ücreti** tabloları, ikili sınıflandırma etiketini oluşturur **Eğimli**, birden çok sınıf sınıflandırma etiketini **İpucu\_sınıfı**ve hello tam birleştirilmiş kümesinden %1 rasgele örnek ayıklar. Bu sorgu kopyalanır, ardından doğrudan hello yapıştırılan [Azure Machine Learning Studio](https://studio.azureml.net) [veri içeri aktarma] [ import-data] hello SQL Server veritabanından doğrudan veri alımı için Modülü Azure örneği. Merhaba sorgu dışlar yanlış kayıtlarıyla (0, 0) koordinatları.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Veri keşfi ve özellik Mühendisliği IPython Not
Bu bölümde, biz veri keşfi ve özellik oluşturma hello SQL Server veritabanını daha önce oluşturduğunuz Python ve SQL sorguları kullanarak gerçekleştirir. Adlandırılmış bir örnek IPython not defteri **machine-Learning-data-science-process-sql-story.ipynb** hello sağlanan **örnek IPython not defterlerini** klasör. Bu dizüstü bilgisayar da kullanılabilir [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

sıralı büyük verilerle çalışırken, önerilen hello hello aşağıda verilmiştir:

* Merhaba veri küçük bir örnek, bir bellek içi veri çerçeveye okuyun.
* Bazı Görselleştirme ve explorations hello örneklenen verileri kullanarak gerçekleştirin.
* Merhaba örneklenen verileri kullanarak özellik Mühendisliği ile deneyin.
* Büyük veri keşfi veri işleme ve özellik Mühendisliği kullanın Python tooissue SQL sorguları doğrudan hello SQL Server veritabanı hello Azure VM.
* Azure Machine Learning modeli oluşturma Hello örnek boyutu toouse karar verin.

Ne zaman tooproceed tooAzure Machine Learning hazır, ya da olabilir:  

1. Merhaba nihai SQL sorgu tooextract ve örnek hello veri ve kopyala-yapıştır hello sorguyu doğrudan kaydetmek bir [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde. Bu yöntem hello gösterilmiştir [Azure Machine Learning yapı modellerinde](#mlmodel) bölümü.    
2. Örneklenen hello ve yeni bir veritabanı tablosunda derleme modeli için toouse planladığınız tasarlanan verilerinin kalıcı olmasını sonra hello yeni tablo hello kullanın [veri içeri aktarma] [ import-data] modülü.

birkaç veri keşfi, veri Görselleştirme ve örnekler mühendislik özelliği Hello aşağıda verilmiştir. Merhaba örnek SQL IPython not defterinde hello daha fazla örnek için bkz **örnek IPython not defterlerini** klasör.

#### <a name="initialize-database-credentials"></a>Veritabanı kimlik bilgileri başlatma
Veritabanı bağlantı ayarlarınızda değişkenleri aşağıdaki hello başlatın:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Veritabanı bağlantısı oluşturma
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Tablo nyctaxi_trip sayfasındaki satır ve sütunları rapor sayısı
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Toplam satır sayısı 173179759 =  
* Toplam sütun sayısı = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Okuma bileşenini hello SQL Server veritabanı küçük veri örnekten
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Zaman tooread hello örnek Tablo 6.492000 saniyedir  
Satır ve sütunların sayısı, alınan = (84952, 21)

#### <a name="descriptive-statistics"></a>Açıklayıcı istatistikleri
Hazır tooexplore örneklenen hello veri sunulmuştur. Merhaba açıklayıcı istatistiklerini bakarak ile başlangıç **seyahat\_uzaklığı** (veya diğer) alan:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Görselleştirme: Kutusu çizim örneği
Sonraki hello Kutu Çizimi hello seyahat uzaklığı toovisualize hello quantiles için ele

    df1.boxplot(column='trip_distance',return_type='dict')

![#1 Çiz][1]

#### <a name="visualization-distribution-plot-example"></a>Görselleştirme: Dağıtım çizim örneği
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![#2 Çiz][2]

#### <a name="visualization-bar-and-line-plots"></a>Görselleştirme: Çubuğu ve satır çizimleri
Bu örnekte, beş depo içine hello seyahat uzaklığı bin ve sonuçları binning hello görselleştirin.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Biz depo dağıtım çubuğundaki yukarıda hello çizmek veya aşağıdaki şekilde çizim satır

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![#3 Çiz][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![#4 Çiz][4]

#### <a name="visualization-scatterplot-example"></a>Görselleştirme: Scatterplot örneği
Dağılım çizim arasında gösteriyoruz **seyahat\_zaman\_içinde\_saniye** ve **seyahat\_uzaklığı** herhangi bağıntı ise toosee

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 Çiz][6]

Benzer şekilde biz hello ilişkisi denetleyebilirsiniz **oranı\_kod** ve **seyahat\_uzaklığı**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 Çiz][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Alt örnekleme hello SQL verileri
Veri modeli oluşturmaya için hazırlarken [Azure Machine Learning Studio](https://studio.azureml.net), üzerinde hello ya da karar verebilirsiniz **hello veri içeri aktarma modülünde doğrudan SQL sorgu toouse** ya da mühendislik ve örneklenen hello kalıcı hello kullanabilen yeni bir tabloda veri [veri içeri aktarma] [ import-data] basit bir modülüyle **seçin * FROM <,\_yeni\_tablo\_adı >**.

Bu bölümde oluşturacağız yeni bir tablo toohold hello örneklenen ve veri mühendislik. Model oluşturmanın için doğrudan bir SQL sorgusu örneği hello sağlanan [veri keşfi ve özellik Mühendisliği SQL Server'daki](#dbexplore) bölümü.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Bir örnek tablo ve Populate hello birleştirilmiş tablolar, %1 ile oluşturun. Varsa Tablo ilk bırakın.
Bu bölümde, biz hello tabloları birleştirme **nyctaxi\_seyahat** ve **nyctaxi\_ücreti**%1 rasgele örnek ayıklayın ve yeni bir tablo adı örneklenen hello veriyi kalıcı  **nyctaxi\_bir\_yüzde**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Veri keşfi IPython not defterinde SQL sorgularını kullanma
Bu bölümde, yukarıda oluşturduğumuz hello yeni tabloda kalıcı hello %1 örneklenen verileri kullanarak veri dağıtımları keşfedin. Benzer explorations isteğe bağlı olarak kullanarak hello özgün tabloları kullanılarak gerçekleştirilebilir Not **TABLESAMPLE** toolimit hello araştırması örnek veya hello sınırlayarak sonuçları hello kullanarak süre verilen tooa **alma \_datetime** hello gösterildiği gibi bölümler [veri keşfi ve özellik Mühendisliği SQL Server'daki](#dbexplore) bölümü.

#### <a name="exploration-daily-distribution-of-trips"></a>Araştırması: Dönüş günlük dağıtımını
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Keşfetme: medallion başına dağıtım seyahat
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>IPython not defterinde SQL sorgularını kullanarak özelliği oluşturma
Bu bölümde yeni etiketler oluşturacağız ve doğrudan SQL sorgularını kullanarak özellik hello %1 örnek tablo üzerinde işletim hello önceki bölümde oluşturduğumuz.

#### <a name="label-generation-generate-class-labels"></a>Etiket oluşturma: Sınıf etiketleri oluşturmak
Aşağıdaki örneğine hello etiketleri toouse modelleme için iki kümesi oluştur:

1. İkili sınıfı etiketleri **Eğimli** (bir ipucu verilir tahmin etmeye)
2. Çok sınıflı etiketleri **İpucu\_sınıfı** (Merhaba ipucu depo veya aralık tahmin etmeye)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Özellik Mühendisliği: Kategorik sütunlar sayısı özellikleri
Bu örnek, yineleme hello verilerdeki hello sayısı ile her kategori değiştirerek kategorik alan bir sayısal alana dönüştürür.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Özellik Mühendisliği: Sayısal sütunlar Bin özellikleri
Bu örnek sürekli bir sayısal alana hazır kategori aralıkları, yani, sayısal alana kategorik alan dönüştürme dönüştürür.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Özellik Mühendisliği: Ondalık enlem/boylam konumu özelliklerinden Extract
Bu örnek hello ondalık gösterimini enlem ve/veya boylam alan farklı bir ayrıntı düzeyi birden çok bölgede alanlarına gibi keser ülke, şehir, şehir, engelleme, vb.. Merhaba yeni coğrafi alanlar değil eşlenen tooactual konumları olduğuna dikkat edin. Eşleme geocode konumları hakkında daha fazla bilgi için bkz: [Bing Haritalar REST Hizmetleri](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Merhaba featurized tablosunun son form Hello doğrulayın
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Şimdi hazır tooproceed toomodel yapı ve model dağıtımda duyuyoruz [Azure Machine Learning](https://studio.azureml.net). Merhaba veri herhangi bir önceki sürümlerinde, yani tanımlanan hello tahmin sorunları için hazırdır:

1. İkili sınıflandırma: olsun veya olmasın bir ipucu Ücretli bir seyahat için toopredict.
2. Çok sınıflı sınıflandırma: Ücretli, ipucu önceden tanımlanmış sınıfları toohello göre toopredict hello aralığı.
3. Regresyon görevi: seyahat için ödenen ucunun toopredict hello tutar.  

## <a name="mlmodel"></a>Azure Machine Learning oluşturma modelleri
toobegin alıştırma modelleme Merhaba, tooyour Azure Machine Learning çalışma alanına oturum açın. Machine learning çalışma alanı henüz oluşturmadıysanız, bkz: [bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md).

1. Azure Machine Learning ile başlatılan tooget bakın [Azure Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md)
2. Çok oturum[Azure Machine Learning Studio](https://studio.azureml.net).
3. Merhaba Studio giriş sayfası bol miktarda bilgi, videoları, öğreticiler, bağlantılar toohello modülleri başvurusu ve diğer kaynakları sağlar. Azure Machine Learning hakkında daha fazla bilgi için hello başvurun [Azure Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).

Tipik eğitim denemenizi hello şunlardan oluşur:

1. Oluşturma bir **+ yeni** deneyin.
2. Merhaba veri tooAzure Machine Learning alın.
3. Önceden işler, dönüştürme ve gerektiği gibi hello veri arabirimidir.
4. Özellikler gerektiği şekilde oluşturun.
5. Eğitim/doğrulama/test kümelerine Hello veri bölme (veya ayrı veri kümeleri her).
6. Bir veya daha fazla makine öğrenimi algoritmaları sorun toosolve öğrenme hello bağlı olarak seçin. Örneğin, ikili Sınıflandırma, çok sınıflı Sınıflandırma, regresyon.
7. Merhaba eğitim veri kümesini kullanarak bir veya daha fazla modelleri eğitme.
8. Merhaba, eğitilen modellerini kullanarak hello doğrulama dataset puan.
9. Merhaba modellere toocompute hello ilgili ölçümlerini sorun öğrenme hello değerlendirin.
10. Merhaba modellerini ve select hello en iyi modeli toodeploy ince.

Bu alıştırmada, biz varsa zaten incelediniz ve SQL Server'daki hello veri mühendislik ve hello örnek boyutu tooingest Azure Machine learning'de karar. bir veya daha fazla karar hello tahmin modellerinin toobuild:

1. Merhaba veri tooAzure Machine Learning almak hello kullanarak [veri içeri aktarma] [ import-data] modülü, hello kullanılabilir **veri giriş ve çıkış** bölümü. Merhaba daha fazla bilgi için bkz: [veri içeri aktarma] [ import-data] modül başvuru sayfası.
   
    ![Azure Machine Learning Veri Al][17]
2. Seçin **Azure SQL veritabanı** hello olarak **veri kaynağı** hello içinde **özellikleri** paneli.
3. Hello Hello veritabanı DNS adını girin **veritabanı sunucusu adı** alan. Biçimi:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Merhaba girin **veritabanı adı** hello karşılık gelen alandaki.
5. Merhaba girin **SQL kullanıcı adı** hello içinde ** sunucu kullanıcı aqccount adı ve hello hello Parolada **Server kullanıcı hesabı parolasını**.
6. Denetleme **herhangi bir sunucu sertifikayı kabul** seçeneği.
7. Merhaba, **veritabanı sorgusu** metin alanı düzenleme, hello gerekli veritabanı (Merhaba etiketler gibi hesaplanan alanları dahil) alanları ve aşağı hangi ayıklar örnekleri hello veri istenen toohello örnek boyutu hello sorguyu yapıştırın.

Merhaba aşağıdaki çizimde doğrudan hello SQL Server veritabanından veri okunurken bir ikili sınıflandırma deneme örnektir. Benzer denemeler, çok sınıflı sınıflandırma ve regresyon sorunları için oluşturulabilir.

![Azure Machine Learning eğitimi][10]

> [!IMPORTANT]
> Veri ayıklama modelleme ve önceki bölümlerde verilen sorgu örnekler örnekleme hello içinde **hello üç modelleme alıştırmaları için tüm etiketleri hello sorguya dahil**. Önemli bir (gerekli) her alıştırmaları modelleme hello çok adımdır**hariç** gereksiz etiketler Merhaba için iki diğer sorunlar ve diğer hello **hedef sızıntıları**. İçin örn., ikili Sınıflandırma, kullanırken hello etiket **Eğimli** ve hello alanları dışarıda **İpucu\_sınıfı**, **İpucu\_tutar**, ve **toplam\_tutar**. Merhaba ikinci hello ipucu kapsıyor beri hedef sızıntıları Ücretli.
> 
> tooexclude gereksiz sütunları ve/veya hedef sızıntıları, hello kullanabilir [Select Columns in Dataset sütun] [ select-columns] modül veya hello [Düzenle meta veri] [ edit-metadata]. Daha fazla bilgi için bkz: [Select Columns in Dataset sütun] [ select-columns] ve [Düzenle meta veri] [ edit-metadata] başvuru sayfaları.
> 
> 

## <a name="mldeploy"></a>Azure Machine Learning modellerini dağıtma
Modeliniz hazır olduğunda, kolayca onu hello deneme doğrudan bir web hizmeti olarak dağıtabilirsiniz. Azure Machine Learning web hizmetleri dağıtma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy yeni bir web hizmeti, şunları yapmanız gerekir:

1. Puanlama bir deneme oluşturma.
2. Merhaba web hizmetini dağıtın.

bir Puanlama denemeler toocreate bir **tamamlandı** deneme eğitim, tıklatın **oluşturma PUANLAMA DENEMELER** hello alt eylem çubuğunda.

![Azure Puanlama][18]

Azure Machine Learning toocreate hello eğitim denemenizi hello bileşenlerini temel alan bir Puanlama deneme deneyecek. Özellikle, çıkarır:

1. Merhaba, eğitilen model kaydetmek ve hello model eğitim modüllerini kaldırın.
2. Bir mantıksal tanımlamak **giriş bağlantı noktası** toorepresent hello giriş veri şeması bekleniyordu.
3. Bir mantıksal tanımlamak **çıkış bağlantı noktasına** toorepresent hello beklenen web hizmeti çıkış şeması.

Deneme Puanlama hello oluşturulduğunda, gözden geçirin ve gerektiği gibi ayarlayın. Merhaba hizmeti çağrıldığında bunlar kullanılamaz tipik ayarlama tooreplace hello girdi veri kümesi ve/veya sorgu etiket alanları hariç biri ile aynıdır. Ayrıca, hello iyi bir uygulama tooreduce hello boyutunu veri kümesi ve/veya sorgu tooa birkaç kayıtları, yeterli tooindicate hello giriş şemasını giriş unutulmamalıdır. Merhaba çıkış bağlantı noktasına ilişkin tüm giriş alanları ortak tooexclude olduğundan ve yalnızca hello dahil **skoru etiketleri** ve **skoru olasılıklar** hello kullanarak çıktıyı hello içinde [veri kümesinde Sütun Seç ] [ select-columns] modülü.

Deneme Puanlama bir örnek hello aşağıdaki çizimde gösterilmektedir. Ne zaman toodeploy, hazır hello tıklatın **yayımlama WEB hizmeti** hello alt eylem çubuğunda düğmesi.

![Azure Machine Learning yayımlama][11]

toorecap, bu gözden geçirme öğreticide büyük ortak veri kümesi eğitim ve bir Azure Machine Learning web hizmeti dağıtma veri alım toomodel tüm hello şekilde ile çalışan bir Azure veri bilimi ortam oluşturdunuz.

### <a name="license-information"></a>Lisans bilgileri
Bu örnek gözden geçirme ve kendi eşlik eden komut dosyaları ve IPython notebook(s) paylaşıldığı Microsoft tarafından hello MIT lisansı altında. Lütfen hello LICENSE.txt dosyayı daha fazla ayrıntı için GitHub üzerindeki hello örnek kodu hello dizininde iade edin.

### <a name="references"></a>Başvurular
• [Andrés Monroy NYC ücreti dönüşleri indirme sayfası](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC ait ücreti seyahat veri Chris Whong tarafından](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC ücreti ve Limousine devreye sokmak araştırma ve istatistikleri](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
