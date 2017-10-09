---
title: "Akış analizi kullanarak bir IOT çözüm aaaBuild | Microsoft Docs"
description: "Başlangıç Öğreticisi hello gişe senaryosu Stream Analytics IOT çözüm için"
keywords: "IOT çözüm, pencere işlevleri"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Akış analizi kullanarak bir IOT çözüm oluşturma
## <a name="introduction"></a>Giriş
Bu öğreticide şunları öğreneceksiniz nasıl toouse Azure akış analizi tooget gerçek zamanlı Öngörüler verilerinizden. Geliştiriciler, kolayca geçmiş kayıtlarını veya başvuru veri tooderive iş öngörüleri tıklatın akışlar, günlükler ve cihaz tarafından oluşturulan olaylar gibi veri akışları birleştirebilirsiniz. Microsoft Azure üzerinde barındırılan bir tam olarak yönetilen, gerçek zamanlı akış hesaplama hizmeti, yukarı ve dakika içinde çalışan yerleşik dayanıklılık, düşük gecikme süresi ve ölçeklenebilirlik tooget Azure akış analizi sağlar.

Bu öğreticiyi tamamladıktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Hello Azure akış analizi portalıyla hakkında bilgi edinin.
* Yapılandırın ve iş akışında dağıtın.
* Gerçek dünyadaki sorunları iyileştirir ve hello Stream Analytics sorgu dilini kullanarak çözün.
* Stream Analytics güvenle kullanarak çözümleri müşterileriniz için akış geliştirin.
* İzleme ve deneyimi tootroubleshoot sorunları günlüğe kaydetme hello kullanın.

## <a name="prerequisites"></a>Ön koşullar
Önkoşullar toocomplete Bu öğretici hello:

* Merhaba en son sürümünü [Azure PowerShell](/powershell/azure/overview)
* 2015, Visual Studio 2017 veya hello ücretsiz [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* Bir [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/)
* Merhaba bilgisayarda yönetim ayrıcalıkları
* İndirme [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) hello Microsoft Download Center gelen
* İsteğe bağlı: Kaynak kodu hello TollApp olay üreteci için [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Senaryo giriş: "Hello, ücretli!"
Ücretli istasyonu ortak olguya ' dir. Bunları birçok expressways, köprüleri ve tünelleri Merhaba dünya genelindeki karşılaştığınız. Her Ücretli istasyon birden çok Ücretli booths sahiptir. El ile booths toopay hello Ücretli tooan Görevlisi durdurun. Otomatik booths üstünde her Stand algılayıcı hello Ücretli Stand geçirirken yapıştırılmış toohello ön, araç, bir RFID kartı tarar. Bu araçlar bu Ücretli istasyonları aracılığıyla kolay toovisualize hello geçişini ilginç işlemleri gerçekleştirilebilir bir olay akışı gösterir.

![Ücretli booths adresindeki araba resmi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Gelen veriler
Bu öğretici, iki veri akışları ile çalışır. Algılayıcılar hello giriş yüklü ve çıkış hello Ücretli istasyonları hello ilk akış üretir. Merhaba ikinci araç kayıt verileri içeren bir statik arama dataset akışıdır.

### <a name="entry-data-stream"></a>Girdi veri akışı
Ücretli istasyonları girerken hello giriş veri akışı araba hakkında bilgiler içerir.

| TollID | EntryTime | LicensePlate | Durum | Yapma | modeli | VehicleType | VehicleWeight | Ücretli | Etiket |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |U |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |U |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |BNJ 1007 |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4 x 4 |1 |0 |6 |321987654 |

Merhaba sütunların kısa bir açıklaması verilmiştir:

| Sütun | Açıklama |
| --- | --- |
| TollID |Ücretli Stand benzersiz olarak tanıtan hello Ücretli Stand kimliği |
| EntryTime |Başlangıç tarihi ve saati hello araç toohello Ücretli Stand UTC girişinin |
| LicensePlate |Merhaba lisans kalıbı hello araç sayısı |
| Durum |Amerika Birleşik Devletleri bir durumda |
| Yapma |Merhaba otomobil Hello üreticisi |
| modeli |Merhaba otomobil Hello model numarası |
| VehicleType |Yolcu taşıtlardan veya ticari araçları için 2 ya da 1 |
| WeightType |Araç ağırlık ton cinsinden; yolcu araçları için 0 |
| Ücretli |Merhaba Ücretli değeri ABD Doları |
| Etiket |e-Tag ödeme otomatikleştirir hello otomobil üzerinde hello; Merhaba ödeme el ile yapılan burada boş |

### <a name="exit-data-stream"></a>Çıkış veri akışı
Merhaba çıkış veri akışı hello Ücretli istasyon bırakarak araba hakkında bilgiler içerir.

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |BNJ 1007 |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

Merhaba sütunların kısa bir açıklaması verilmiştir:

| Sütun | Açıklama |
| --- | --- |
| TollID |Ücretli Stand benzersiz olarak tanıtan hello Ücretli Stand kimliği |
| ExitTime |Başlangıç tarihi ve saati hello araç çıkış Ücretli Stand UTC ' |
| LicensePlate |Merhaba lisans kalıbı hello araç sayısı |

### <a name="commercial-vehicle-registration-data"></a>Ticari araç kayıt verileri
Merhaba öğretici bir ticari araç kayıt veritabanının statik bir anlık görüntü kullanır.

| LicensePlate | RegistrationId | Süresi dolmuş |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| İCLOU 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Merhaba sütunların kısa bir açıklaması verilmiştir:

| Sütun | Açıklama |
| --- | --- |
| LicensePlate |Merhaba lisans kalıbı hello araç sayısı |
| RegistrationId |Merhaba araç'ın kayıt kimliği |
| Süresi dolmuş |Merhaba hello araç kayıt durumunu: araç kayıt etkinse 0 kayıt süresi 1 |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Azure akış analizi için Hello ortamını ayarlama
toocomplete Bu öğreticide, Microsoft Azure aboneliğinizin olması gerekir. Microsoft, ücretsiz deneme sürümü için Microsoft Azure hizmetleri sunar.

Bir Azure hesabınız yoksa, şunları yapabilirsiniz [ücretsiz deneme sürümü isteği](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign ücretsiz deneme için metin iletileri ve geçerli bir kredi kartı alabileceği bir mobil aygıtı gerekir.
> 
> 

Böylece Azure kredi en iyi kullanımı hello yapabilirsiniz toofollow hello hello bu makalenin sonunda hello "Azure hesabınızı temizleme" bölümündeki adımları emin olun.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Merhaba öğretici için gerekli Azure kaynaklarını hazırlama
Bu öğretici iki olay hub'ları tooreceive gerektirir *girişi* ve *çıkmak* veri akışları. Azure SQL veritabanı hello akış analizi işleri hello sonuçlarını çıkarır. Azure depolama araç kayıtlar hakkında başvuru verileri depolar.

Tüm gerekli kaynaklar üzerinde GitHub toocreate hello TollApp klasöründe hello Setup.ps1 komut dosyası kullanabilirsiniz. Hello ilgisini zaman, onu çalıştırmanızı öneririz. Toolearn nasıl tooconfigure hello Azure portalı, bu kaynaklara başvuran hakkında daha fazla bilgi isterseniz toohello "öğretici kaynakları Azure Portalı'nda yapılandırma" ek.

Karşıdan yükle ve Kaydet hello destekleyen [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) klasör ve dosyaları.

Açık bir **Microsoft Azure PowerShell** penceresi *yönetici olarak*. Azure PowerShell henüz yoksa hello yönergeleri izleyin [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) tooinstall onu.

Windows otomatik olarak .ps1, .dll ve .exe dosyaları engellediğinden, hello betiği çalıştırmadan önce tooset hello yürütme İlkesi gerekir. Hello Azure PowerShell penceresi çalıştığından emin olun *yönetici olarak*. Çalıştırma **Set-ExecutionPolicy unrestricted**. İstendiğinde yazın **Y**.

!["Set-Kısıtlanmamış Azure PowerShell penceresinde çalıştıran ExecutionPolicy" ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Çalıştırma **Get-ExecutionPolicy** toomake hello komutu çalıştığından emin.

!["Get-ExecutionPolicy Azure PowerShell penceresinde Çalıştırma" ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Merhaba komut dosyaları ve oluşturucu uygulama sahip toohello dizinine gidin.

!["Hello Azure PowerShell penceresinde çalıştıran cd .\TollApp\TollApp" ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Tür **.\\ Setup.ps1** tooset Azure hesabınızı ayarlama oluşturmak ve gerekli tüm kaynaklarını yapılandırmak ve toogenerate olayları başlatın. Merhaba betik bölge toocreate kaynaklarınızı rastgele seçer. tooexplicitly bir bölge belirtin, hello geçirebilirsiniz **-konum** aşağıdaki örneğine hello olduğu gibi parametre:

**. \\Setup.ps1-konum "Orta ABD"**

![Hello Azure oturum açma sayfasının ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

Merhaba betik açar hello **oturum** Microsoft Azure için sayfa. Hesap kimlik bilgilerinizi girin.

> [!NOTE]
> Hesabınıza erişim toomultiple abonelikleri varsa, toouse hello öğretici için istediğiniz sorulan tooenter hello abonelik adı olacaktır.
> 
> 

Merhaba betik birkaç dakika toorun alabilir. Sona erdikten sonra hello çıkışı hello ekran aşağıdaki gibi görünmelidir.

![Hello Azure PowerShell penceresinde hello komut dosyası çıkışını ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

Ayrıca, aşağıdaki ekran görüntüsüne benzer toohello olan başka bir pencere görürsünüz. Bu uygulamayı gerekli toorun hello öğretici olduğu tooAzure Event Hubs, olayları gönderiyor. Bu nedenle, değil hello uygulamayı durdurun veya hello öğretici tamamlanana kadar bu pencereyi kapatın.

!["Gönderme olay hub'ı veri" ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

Mümkün toosee kaynaklarınızı Azure Portalı'nda artık olması gerekir. Çok Git<https://portal.azure.com>ve hesabı kimlik bilgilerinizle oturum açın. Şu anda bazı işlevler hello Klasik portal kullanır olduğunu unutmayın. Bu adımları açıkça gösterilir.

### <a name="azure-event-hubs"></a>Azure Event Hubs
Hello Azure portal'ı tıklatın **daha fazla hizmet** hello bölmesinin hello sol Yönetim üzerinde. Tür **olay hub'ları** hello sağlanan alan ve tıklatın **olay hub'ları**. Bu yeni bir tarayıcı penceresi toodisplay hello başlatır **SERVICE BUS** hello alanında **Klasik portal**. Burada hello Event Hub'ın hello Setup.ps1 komut dosyası tarafından oluşturulan görebilirsiniz.

![Service Bus](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Merhaba ile başlayan bir tıklatın *tolldata*. Merhaba tıklatın **olay hub'ları** sekmesi. Adlı iki olay hub görürsünüz *girişi* ve *çıkmak* bu ad alanında oluşturuldu.

![Merhaba Klasik Portalı'nda olay hub'ları sekmesi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Azure depolama kapsayıcısı
1. Tarayıcı açık tooAzure portalınızın toohello sekmesine geri dönün. Tıklatın **depolama** sol hello öğreticide kullanılan hello Azure portal toosee hello Azure depolama kapsayıcısının tarafı hello üzerinde.
   
    ![Depolama menü öğesi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Merhaba ile başlayan bir tıklatın *tolldata*. Merhaba tıklatın **KAPSAYICILARI** sekmesini toosee oluşturulan hello kapsayıcı.
   
    ![Kapsayıcıları sekmesinde hello Azure portalı](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Merhaba tıklatın **tolldata** kapsayıcı toosee hello araç kayıt verileri içeren bir JSON dosyası karşıya yüklendi.
   
    ![Merhaba kapsayıcısında hello registration.json dosyasının ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Azure SQL Database
1. Geri hello tarayıcıda açılan ilk sekme hello toohello Azure portalına gidin. Tıklatın **SQL veritabanları** sol hello öğreticide kullanılan tıklatın hello Azure portal toosee hello SQL veritabanını tarafı hello üzerinde **tolldatadb**.
   
    ![Oluşturulan hello SQL veritabanı'nın ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Kopya hello sunucu adı olmadan hello bağlantı noktası numarası (*servername*. Örneğin database.windows.net).
    ![Oluşturulan hello SQL veritabanı db ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Visual Studio'dan toohello veritabanına bağlanın
Visual Studio tooaccess sorgu sonuçları hello çıkış veritabanında kullanın.

Visual Studio'dan bağlantı toohello SQL veritabanı (Merhaba hedef):

1. Visual Studio'yu açın ve ardından **Araçları** > **tooDatabase bağlanmak**.
2. İstenirse, tıklatın **Microsoft SQL Server** veri kaynağı olarak.
   
    ![Değişikliği veri kaynağı iletişim kutusu](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. Merhaba, **sunucu adı** alan, Azure portal hello hello önceki bölümünde kopyaladığınız hello adını yapıştırın (diğer bir deyişle, *servername*. database.windows.net).
4. Tıklatın **SQL Server kimlik doğrulaması kullanmak**.
5. Girin **tolladmin** hello içinde **kullanıcı adı** alan ve **123toll!** Merhaba, **parola** alan.
6. Tıklatın **seçin veya bir veritabanı adı girin**seçip **TollDataDB** hello veritabanı olarak.
   
    ![Bağlantı Ekle iletişim kutusu](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. **Tamam** düğmesine tıklayın.
8. Sunucu Gezgini'ni açın.
   
    ![Sunucu Gezgini](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Merhaba TollDataDB veritabanında dört tablolara bakın.
   
    ![Merhaba TollDataDB veritabanındaki tabloları](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Olay Oluşturucusu: TollApp örnek proje
Merhaba PowerShell Betiği hello TollApp örnek uygulama programı kullanarak toosend olayları otomatik olarak başlar. Herhangi bir ilave adımı tooperform gerekmez.

Uygulama Ayrıntıları ilgileniyorsanız, ancak hello TollApp uygulama hello kaynak kodu Github'da bulabilirsiniz [samples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Visual Studio'da görüntülenen örnek kodunu ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Akış Analizi işi oluşturma
1. Hello Azure portal, tıklatın, yeni bir akış analizi işi hello sayfa toocreate hello sol üst köşesindeki yeşil bir artı işareti hello. Seçin **Intelligence + analiz** ve ardından **Stream Analytics işi**.
   
    ![Yeni düğmesi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Bir iş adı sağlayın, hello abonelik doğrulama düzeltin ve ardından yeni bir kaynak grubu hello oluşturun hello olay hub'ı depolama aynı bölgede (varsayılan, Orta Güney ABD hello komut dosyası için).
3. Tıklatın **PIN toodashboard** ve ardından **oluşturma** hello sayfanın hello sonundaki.
   
    ![Akış analizi işi seçeneği oluşturun](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Giriş kaynağı tanımlayın
1. Merhaba işi oluşturmak ve hello iş sayfasını açın. Veya analytics işi hello portal panosunda oluşturulan hello tıklatabilirsiniz.

2. Merhaba tıklatın **GİRİŞLERİ** sekmesinde toodefine hello kaynak verileri.
   
    ![Merhaba girişleri sekmesi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Tıklatın **bir giriş eklemek**.
   
    ![Merhaba Ekle giriş seçeneği](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Girin **EntryStream** olarak **giriş diğer adı**.
5. Kaynak türü **veri akışı**
6. Kaynak **olay hub'ı**.
7. **Hizmet veri yolu ad alanı** hello içinde TollData açılan hello olmalıdır.
8. **Olay hub'ı adı** çok ayarlanmalıdır**girişi**.
9. **Olay hub'ı ilke adı*olan **RootManageSharedAccessKey** (Merhaba varsayılan değer).
10. Seçin **JSON** için **OLAYI seri hale getirme biçimi** ve **UTF8** için **kodlama**.
   
    Ayarlarınızı gibi görünür:
   
    ![Olay hub'ı ayarları](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Tıklatın **oluşturma** hello altındaki hello sayfası toofinish hello Sihirbazı.
    
    Merhaba Giriş akışı oluşturduğunuza göre hello izleyeceği aynı adımları toocreate hello çıkış akışı. Emin tooenter değerleri hello ekran aşağıdaki gibi olması.
    
    ![Merhaba çıkış akışı için ayarları](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    İki giriş akışları tanımladınız:
    
    ![Giriş akışları hello Azure portal tanımlı](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Sonra başvuru veri girişi araba kayıt verilerini içeren hello blob dosyası için ekleyeceksiniz.
11. Tıklatın **ekleme**ve ardından aynı işlem hello akış girişleri için ancak seçin hello izleyin **başvuru verileri** yerine **veri akışı** ve hello **giriş diğer adı**  olan **kayıt**.

12. ile başlayan depolama hesabı **tolldata**. Merhaba kapsayıcı adı olmalıdır **tolldata**ve hello **yol DESENİ** olmalıdır **registration.json**. Bu dosya adı büyük/küçük harfe duyarlıdır ve olmalıdır **küçük**.
    
    ![Blog depolama ayarları](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Tıklatın **oluşturma** toofinish hello Sihirbazı.

Şimdi tüm girişleri tanımlanır.

## <a name="define-output"></a>Çıktı tanımlayın
1. Hello akış analizi işi'ne genel bakış bölmesinde, seçin **ÇIKIŞLARI**.
   
    ![Çıktı sekmesi ve "bir çıktı Ekle" seçeneğini hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. **Ekle**'ye tıklayın.
3. Set hello **çıkış diğer adları** too'output' ardından **havuzu** çok**SQL veritabanı**.
3. Hello hello makalenin "Bağlan tooDatabase Visual Studio'dan" bölümüne kullanılan hello sunucu adını seçin. Merhaba veritabanı adı **TollDataDB**.
4. Girin **tolladmin** hello içinde **kullanıcıadı** alanı **123toll!** Merhaba, **parola** alan ve **TollDataRefJoin** hello içinde **tablo** alan.
   
    ![SQL veritabanı ayarları](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. **Oluştur**'a tıklayın.

## <a name="azure-stream-analytics-query"></a>Azure Stream analytics sorgusu
Merhaba **sorgu** sekmesi dönüşümler gelen veri hello bir SQL sorgusu içerir.

![Bir sorgu toohello sorgu sekmesi eklenmiştir](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

Bu öğretici Azure akış analizi tooprovide tootoll verileri ve yapıları Stream Analytics sorgular, ilgili birkaç iş sorularını kullanılabilir tooanswer ilgili yanıt çalışır.

İlk Stream Analytics işiniz başlamadan önce birkaç senaryo ve hello sorgu sözdizimini inceleyelim.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Giriş tooAzure Stream Analytics sorgu dili
- - -
Ücretli Stand girin taşıtlardan toocount hello sayısı gerektiğini varsayalım. Bu olayların sürekli akışı olduğundan toodefine bir "dönem süresini." sahip "Kaç taşıtlardan üç dakikada Ücretli Stand girin?" Merhaba soru toobe değiştirelim. Yaygın olarak başvurulan tooas hello sayısı dönen budur.

Bu soruya yanıt veren hello Azure Stream Analytics sorgusu bakalım:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Gördüğünüz gibi Azure akış analizi gibi SQL ve birkaç uzantıları toospecify saati ile ilgili yönlerini hello sorgu ekleyen bir sorgu dili kullanır.

Hakkında daha fazla ayrıntı için okuma [zaman Yönetimi](https://msdn.microsoft.com/library/azure/mt582045.aspx) ve [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN'den hello sorguda kullanılan yapılar.

## <a name="testing-azure-stream-analytics-queries"></a>Azure Stream Analytics sorgu test etme
İlk Azure akış analizi sorgu yazılmış, örnek veri dosyalarını kullanarak TollApp klasörü yolu izleyerek hello içinde bulunan zaman tootest şöyledir:

**.. \\TollApp\\TollApp\\veri**

Bu klasör, aşağıdaki dosyaları hello içerir:

* Entry.JSON
* Exit.JSON
* Registration.JSON

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Soru 1: Ücretli Stand girme taşıtlardan sayısı
1. Hello Azure portal ve oluşturulan gidin tooyour Azure Stream Analytics işi açın. Merhaba tıklatın **sorgu** sekmesinde ve hello önceki bölümde sorgudan yapıştırın.

2. toovalidate örnek veriler, karşıya yükleme hello hello tıklayarak EntryStream giriş verisine bu sorgusu hello... simge ve seçme **dosyasından örnek verileri yükleme**.

    ![Merhaba Entry.json dosyasının ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. Select hello dosyası (Entry.json) tıklayın ve yerel makine üzerinde görünür hello bölmesinde **Tamam**. Merhaba **Test** simgesi artık karanl ve tıklatılabilir.
   
    ![Merhaba Entry.json dosyasının ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Merhaba sorgu Hello çıktısını beklendiği gibi olduğunu doğrulayın:
   
    ![Merhaba test sonuçları](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Soru 2: her araba toopass hello Ücretli Stand aracılığıyla toplam süresi raporu
bir araba toopass hello Ücretli aracılığıyla için gerekli olan hello ortalama süre tooassess hello verimliliğini hello işlemi ve hello Müşteri Deneyimi yardımcı olur.

toofind hello toplam süre, hello ExitTime akış olan toojoin hello EntryTime akış gerekir. Merhaba akışları TollId ve LicencePlate sütunlarda katılır. Merhaba **katılma** işleci hello kabul edilebilir zaman hello arasındaki farkı birleştirilmiş olayları tanımlayan toospecify zamana bağlı leeway gerektirir. Kullanacağınız **DATEDIFF** işlev toospecify olayları birbirinden en fazla 15 dakika olmalıdır. Ayrıca hello uygulanacak **DATEDIFF** işlevi tooexit ve bir araba hello harcadığı toocompute hello gerçek zaman zaman giriş hat istasyon. Not hello fark kullanımını hello **DATEDIFF** içinde kullanıldığında bir **seçin** deyimi yerine **katılma** koşulu.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest bu sorgu, güncelleştirme hello sorgusu hello üzerinde **sorgu** hello işi için. Merhaba test dosyası için ekleme **ExitStream** olduğu gibi **EntryStream** yukarıda girildi.
   
2. Tıklatın **Test**.

3. Merhaba onay kutusunu tootest hello sorgu ve görünüm hello çıktı seçin:
   
    ![Merhaba test çıkışı](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Soru 3: süresi dolan kayıt ile tüm ticari araçları rapor
Azure Stream Analytics, zamana bağlı veri akışları ile veri toojoin statik anlık görüntülerini kullanabilirsiniz. toodemonstrate bu özelliği, örnek soru aşağıdaki kullanım hello.

Bir ticari araç hello Ücretli şirketle kaydedilmişse hello Ücretli Stand İnceleme için durdurulmadan geçirebilirsiniz. Ticari araç kayıt arama tablosu tooidentify kayıtlar süresi dolmuş tüm ticari araçları kullanır.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

başvuru verileri kullanarak bir sorgu tootest, yapmış olduğunuz hello başvuru verileri için bir giriş kaynağı toodefine gerekir.

tootest bu sorgu, hello içine yapıştırma hello sorgu **sorgu** sekmesini tıklatın, **Test**ve hello iki giriş kaynaklarıyla hello kayıt örnek veri tıklatın ve belirtin **Test**.  
   
![Merhaba test çıkışı](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Merhaba Stream Analytics işi Başlat
Artık süresi toofinish hello yapılandırma ve başlangıç hello işi durumdadır. Eşleşme hello şeması hello çıktı üretir soru 3'Hello sorguyu kaydetmek **TollDataRefJoin** çıktı tablosu.

Git toohello iş **PANO**, tıklatıp **Başlat**.

![Merhaba proje panosunda hello Başlat düğmesinin Ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

Merhaba açılan hello iletişim kutusunda, değiştirmek **Başlat çıktı** çok zaman**özel zaman**. Başlangıç saati tooone saat hello geçerli saat önce değiştirin. Bu değişiklik hello hello öğretici başında toogenerate hello olayları başlatıldığından bu yana hello olay hub'ı tüm olayları işlenir sağlar. Şimdi hello tıklayın **Başlat** düğmesini toostart hello işi.

![Özel süre seçimi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Başlangıç hello işi birkaç dakika sürebilir. Akış analizi için hello en üst düzey sayfasında hello durumunu görebilirsiniz.

![Merhaba hello işinin durumunu ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Visual Studio'da denetim sonuçları
1. Visual Studio sunucu Gezgini'ni açın ve hello sağ **TollDataRefJoin** tablo.
2. Tıklatın **Show Table Data** işinizin toosee hello çıktı.
   
    ![Sunucu Gezgini içinde "Tablo verileri göster" seçimi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Out Azure Stream Analytics işlerini ölçeklendirme
Azure Stream Analytics tasarlanmıştır tooelastically ölçeklendirmenizi çok miktarda veri işleyebilir. Hello Azure akış analizi sorgu kullanabileceğiniz bir **bölüm tarafından** bu adımı ölçeğini yan tümcesi tootell hello sistem. **PartitionID** sistem hello özel bir sütun ekler toomatch hello bölüm kimliği hello giriş (olay hub) değil.

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Durdurma hello geçerli işi, güncelleştirme hello hello sorguda **sorgu** sekmesi ve açık hello **ayarları** gear hello proje panosunda. Tıklatın **ölçek**.
   
    **Akış birimleri** tanımlamak hello tutar iş hello işlem gücü alabilir.
2. Değişiklik hello açılan 6 1.
   
    ![6 akış birimleri seçme ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Toohello Git **ÇIKIŞLARI** sekmesinde ve çok hello hello SQL tablo adını değiştirin**TollDataTumblingCountPartitioned**.

Merhaba iş başlatırsanız şimdi, Azure akış analizi iş üzerinde daha fazla işlem kaynağı dağıtabilir ve daha iyi verim elde etmek. Lütfen bu hello TollApp uygulama da TollId tarafından bölümlenmiş olayların gönderilmesi unutmayın.

## <a name="monitor"></a>İzleme
Merhaba **İZLEYİCİ** alanı işi hello hakkındaki istatistiklerdir içerir. İlk kez yapılandırması gerekli hello toouse hello depolama hesabında aynı bölgede (Bu belgenin hello rest gibi ad Ücretli).   

![İzleyici'nin ekran görüntüsü](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

Erişebileceğiniz **etkinlik günlükleri** hello iş panosundan **ayarları** de alanı.


## <a name="conclusion"></a>Sonuç
Bu öğretici toohello Azure Stream Analytics hizmeti kullanıma sunuldu. Bunu nasıl tooconfigure girişleri ve çıkışları için Stream Analytics işi hello gösterilmektedir. Merhaba Ücretli veri senaryosu kullanarak hello öğretici Azure akış analizi basit SQL benzeri sorguları hareket ve bunların nasıl çözülebilir verilerle hello alanındaki çıkan sorunları genel türleri açıklanmıştır. Başlangıç Öğreticisi zamana bağlı verilerle çalışmak için SQL uzantısı yapıları açıklanmaktadır. Statik başvuru verileri ile tooenrich hello veri akışı nasıl ve nasıl, toojoin veri nasıl akışlarını gösterdi tooscale sorgu tooachieve daha yüksek verimlilik çıkışı.

Bu öğretici bir iyi giriş sağlasa da, herhangi bir yolla tam değil. Daha fazla sorgu desenlerine hello SAQL dil desteğini kullanarak bulabilirsiniz [sorgu örnekler için ortak Stream Analytics kullanım desenlerini](stream-analytics-stream-analytics-query-patterns.md).
Toohello başvuran [çevrimiçi belgeleri](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn Azure Stream Analytics hakkında daha fazla bilgi.

## <a name="clean-up-your-azure-account"></a>Azure hesabınızı Temizle
1. Hello Azure portal Hello Stream Analytics işinde durdurun.
   
    Merhaba Setup.ps1 komut dosyası, iki olay hub'ları ve bir SQL veritabanı oluşturur. Aşağıdaki yönergeler Yardım hello hello öğreticinin sonunda kaynakları temizlemek hello.
2. Bir PowerShell penceresinde yazın **.\\ CleanUp.ps1** hello öğreticide kullanılan kaynakları siler toostart hello komut dosyası.
   
   > [!NOTE]
   > Kaynakları hello ada göre tanımlanır. Dikkatle kaldırma onaylamadan önce her bir öğeyi gözden emin olun.
   > 
   > 


