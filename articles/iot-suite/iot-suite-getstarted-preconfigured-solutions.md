---
title: "kullanmaya aaaGet önceden yapılandırılmış çözümleri | Microsoft Docs"
description: "Bu öğretici toolearn izleyin nasıl çözüm toodeploy bir Azure IOT paketi önceden yapılandırılmış."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Merhaba önceden yapılandırılmış çözümleri kullanmaya başlama

Azure IOT paketi [önceden yapılandırılmış çözümleri] [ lnk-preconfigured-solutions] ortak IOT iş senaryolarını uygulayan birden çok Azure IOT Hizmetleri toodeliver uçtan uca çözümler birleştirin. Merhaba *Uzaktan izleme* önceden yapılandırılmış çözüm aygıtlarınızı tooand izleyiciler bağlanır. Otomatik olarak veri toothat akışı yanıt işlemleri yaparak hello çözüm tooanalyze hello akış cihazlarınız ve tooimprove işletme sonuçlarını verilerini kullanabilirsiniz.

Bu öğretici nasıl tooprovision hello çözüm önceden yapılandırılmış Uzaktan izleme gösterir. Bu ayrıca, hello aracılığıyla hello önceden yapılandırılmış çözümün temel özellikleri açıklanmaktadır. Bu özelliklerin çoğunu hello çözümden erişebilirsiniz *Pano* hello önceden yapılandırılmış çözümün bir parçası dağıtır:

![Önceden yapılandırılmış uzaktan izleme panosu][img-dashboard]

toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.

> [!NOTE]
> Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Senaryoya genel bakış

Merhaba Uzaktan izleme çözümü dağıttığınızda, bunu, toostep yaygın bir uzaktan izleme senaryo aracılığıyla kaynak ile önceden doldurulmaz. Bu senaryoda, çeşitli aygıtlar bağlı toohello çözümü raporlama beklenmeyen sıcaklık değerleri. Merhaba aşağıdaki bölümlerde, nasıl göstermek için:

* Beklenmeyen sıcaklık değerleri gönderme hello aygıtları belirleyin.
* Bu cihazların yapılandırma toosend daha ayrıntılı telemetri.
* Bu cihazlarda hello bellenim güncelleştirerek Hello sorunu düzeltin.
* Eyleminizi hello sorunu Çözümlendi doğrulayın.

Bir anahtar, bu senaryo bu eylemleri uzaktan hello çözüm panodan için gerçekleştirebilir özelliğidir. Fiziksel erişim toohello aygıtları gerekmez.

## <a name="view-hello-solution-dashboard"></a>Görünüm hello çözüm Panosu

Merhaba çözüm Panosu toomanage dağıtılan hello çözümü sağlar. Örneğin, telemetriyi görüntüleyebilir, cihazları ekleyebilir ve kuralları yapılandırabilirsiniz.

1. Ne zaman hello Sağlama tamamlandıktan ve önceden yapılandırılmış çözümünüzün kutucuğu hello gösterir **hazır**, seçin **başlatma** tooopen Uzaktan izleme çözümü portalınızı yeni bir sekmede.

    ![Merhaba önceden yapılandırılmış çözüm başlatma][img-launch-solution]

1. Varsayılan olarak, hello çözüm portalı hello gösterir *Pano*. Merhaba sol taraftaki hello sayfasının hello menüsünü kullanarak hello çözüm portalı tooother alanlarının gidebilirsiniz.

    ![Önceden yapılandırılmış uzaktan izleme panosu][img-menu]

Başlangıç Panosu aşağıdaki bilgilerle hello görüntüler:

* Her cihaz hello konumunu görüntüler bir harita toohello çözüm bağlı. Merhaba çözümü ilk kez çalıştırdığınızda, 25 sanal cihazlar vardır. Merhaba sanal cihazlar Azure WebJobs olarak uygulanır ve hello çözüm hello haritada hello Bing Haritalar API'si tooplot bilgileri kullanır. Merhaba bkz [SSS] [ lnk-faq] toolearn nasıl toomake hello harita dinamik.
* Seçilen yakın gerçek zamanlı cihazdan nem ve sıcaklık telemetrisini çizen ve maksimum, minimum ve ortalama nem gibi toplu verileri görüntüleyen bir **Telemetri Geçmişi** paneli.
* Bir telemetri değeri bir eşiği aştığında yeni uyarı etkinliklerini gösteren bir **Uyarı Geçmişi** paneli. Merhaba önceden yapılandırılmış çözümü tarafından oluşturulan ek toohello örneklerde kendi alarmlarınızı tanımlayabilirsiniz.
* Zamanlanmış işler hakkında bilgiler gösteren bir **İşler** paneli. **Yönetim işleri** sayfasından kendi işlerinizi zamanlayabilirsiniz.

## <a name="view-alarms"></a>Uyarıları görüntüleme

Merhaba alarm geçmişi paneli beş cihaza beklenen telemetri değerleri daha yüksek raporlama gösterir.

![Merhaba çözüm Panosu Yapılacaklar Alarm geçmişi][img-alarms]

> [!NOTE]
> Bu uyarılar hello önceden yapılandırılmış çözümde bulunan bir kural tarafından üretilir. Bir aygıt tarafından gönderilen hello sıcaklık değeri 60 aşarsa bu kural bir uyarı oluşturur. Seçerek kendi kurallar ve eylemler tanımlayabilirsiniz [kuralları](#add-a-rule) ve [Eylemler](#add-an-action) hello sol menüde.

## <a name="view-devices"></a>Cihazları görüntüleme

Merhaba *aygıtları* listesi hello çözümde tüm kayıtlı hello cihazları gösterir. Görüntüleyebilir ve cihaz meta verilerini düzenleme hello aygıt listesinde, eklemek veya cihazları kaldırın ve cihazlarda yöntemleri çağırma. Filtrelemek ve sıralamak hello aygıt listesinde cihazların Merhaba listesi. Merhaba aygıt listesinde gösterilen hello sütunlar özelleştirebilirsiniz.

1. Seçin **aygıtları** Bu çözüm için tooshow hello cihaz listesi.

   ![Görünüm hello aygıt hello çözüm portalı listesinde][img-devicelist]

1. Merhaba cihaz listesi, başlangıçta hello sağlama işlemi tarafından oluşturulan 25 sanal cihazlar gösterir. Ek sanal ve fiziksel cihaz toohello çözüm ekleyebilirsiniz.

1. bir aygıt tooview hello ayrıntılarını hello aygıt listesinde bir cihaz seçin.

   ![Hello çözüm portalında Hello cihaz ayrıntıları görüntüleyin][img-devicedetails]

Merhaba **cihaz ayrıntıları** Masası altı bölümleri içerir:

* Toocustomize hello aygıt simgesini etkinleştirmek, hello aygıtı devre dışı bırakmak, bir kural eklemek, bir yöntemi çağırma veya bir komut gönderme bağlantıları koleksiyonu. Komutlar (cihazdan buluta iletiler) ile yöntemlerin (doğrudan yöntemler) bir karşılaştırması için bkz. [Buluttan cihaza iletişim kılavuzu][lnk-c2d-guidance].
* Merhaba **cihaz çifti - etiketleri** bölüm hello aygıt tooedit etiket değerlerini sağlar. Etiket değerleri hello aygıt listesinde görüntülemek ve etiket değerleri toofilter hello aygıt listesini kullanın.
* Merhaba **cihaz çifti - istenen özellikleri** bölüm tooset özellik değerlerini gönderilen toobe toohello aygıt sağlar.
* Merhaba **cihaz çifti - bildirilen özellikleri** bölüm hello aygıtından gönderilen özellik değerlerini gösterir.
* Merhaba **cihaz özellikleri** bölüm kimliği ve kimlik doğrulama anahtarlarının hello kimlik kayıt defteri hello cihazı gibi bilgileri gösterir.
* Merhaba **en son işlerin** bölüm bu cihazı kısa bir süre önce hedeflenen herhangi bir işi hakkında bilgileri gösterir.

## <a name="filter-hello-device-list"></a>Filtre hello cihaz listesi

Bir filtre toodisplay beklenmeyen sıcaklık değerleri gönderen cihazları kullanabilirsiniz. Uzaktan izleme çözümü Hello içerir hello **sağlıksız aygıtları** 60'dan büyük bir ortalama sıcaklık değer tooshow aygıtlarla filtre. Ayrıca [kendi filtrelerinizi oluşturabilirsiniz](#add-a-filter).

1. Seçin **kaydedilmiş filtre Aç** toodisplay kullanılabilir filtrelerin listesi. Ardından **sağlıksız aygıtları** tooapply hello Filtresi:

    ![Filtreler hello listesini görüntüle][img-unhealthy-filter]

1. Merhaba cihaz listesi yalnızca ortalama sıcaklık değeri ile cihazları şimdi 60'dan büyük gösterir.

    ![Sağlıksız aygıtları gösteren hello filtrelenmiş aygıt listesini görüntüle][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>İstenen özellikleri güncelleştirme

Düzeltilmesi gerekebilen bir cihaz kümesi belirlediniz. Ancak, hello veri sıklığı 15 saniye düz bir hello sorunu tanılama için yeterli değil karar verin. Daha fazla veri noktaları toobetter sizinle hello sorunu tanılamak Hello telemetri sıklığı toofive saniye tooprovide değiştirme. Bu yapılandırma değişikliği tooyour uzak aygıtlar hello çözüm Portalı'ndan gönderebilir. Bir kez hello etkiyi değerlendirmek ve hello sonuçlarına hareket hello değişiklik yapabilirsiniz.

Bu adımları toorun hello değiştiren bir iş izleyin **TelemetryInterval** özelliği hello etkilenen cihazlar için istenen. Merhaba cihazların Merhaba yeni aldığınızda **TelemetryInterval** özellik değeri, bunlar değişiklik her beş saniyede 15 dakikada yerine kendi yapılandırma toosend telemetri:

1. Merhaba aygıt listesinde sağlıksız cihazların Merhaba listesini gösteren sırada seçin **İş Zamanlayıcısı**, ardından **Düzenle cihaz çifti**.

1. Merhaba iş çağrısı **değiştirme telemetri aralığı**.

1. Merhaba hello değerini değiştirin **istenen özelliği** adı **istenen. Config.TelemetryInterval** toofive saniye.

1. **Zamanlama**’yı seçin.

    ![Merhaba TelemetryInterval özelliği toofive saniye değiştirme][img-change-interval]

1. Merhaba hello işinde hello ilerlemesini izleyebilirsiniz **Yönetim işleri** hello portalında sayfası.

> [!NOTE]
> Toochange istenen özellik değeri için tek bir cihaza istiyorsanız, hello kullanın **istenen özellikleri** hello bölümünde **cihaz ayrıntıları** bir iş çalıştırmak yerine paneli.

Bu iş hello hello değerini ayarlar **TelemetryInterval** tüm aygıtları hello Filtresi tarafından seçilen hello için hello cihaz çifti özelliğinde istenen. Merhaba aygıtları hello cihaz çifti bu değerini almak ve davranışlarını güncelleştirin. Bir aygıt alır ve bir cihaz çifti istenen özelliğinden işler hello karşılık gelen bildirilen değer özelliğini ayarlar.

## <a name="invoke-methods"></a>Çağırma yöntemleri

Merhaba iş çalışırken, hello sağlıksız aygıtlar listesinde tüm bu cihazların eski (küçüktür sürüm 1. 6) bellenim olduğunu fark sürümleri.

![Üretici yazılımı sürümüne hello sağlıksız cihazlar için Görünüm hello bildirdi][img-old-firmware]

Bu üretici yazılımı sürümüne hello beklenmeyen hello kök nedeni olabilir sıcaklık değerleri sağlıklı diğer cihazları yeni güncelleştirilen tooversion 2.0 olduğunu bildiğiniz için. Merhaba yerleşik kullanabilirsiniz **eski bellenim aygıtları** tooidentify eski bellenim sürümleri aygıtlarla filtre. Merhaba Portalı'ndan sonra uzaktan hala eski bellenim sürümleri çalıştıran tüm hello cihazlar güncelleştirebilirsiniz:

1. Seçin **kaydedilmiş filtre Aç** toodisplay kullanılabilir filtrelerin listesi. Ardından **eski bellenim aygıtları** tooapply hello Filtresi:

    ![Filtreler hello listesini görüntüle][img-old-filter]

1. Merhaba cihaz listesi şimdi yalnızca eski bellenim sürümleri ile cihazları gösterir. Bu liste hello tarafından tanımlanan hello beş aygıtları içerir **sağlıksız aygıtları** filtre ve üç ek aygıtları:

    ![Eski aygıtları gösteren hello filtrelenmiş aygıt listesini görüntüle][img-filtered-old-list]

1. **İş Zamanlayıcı**’yı ve ardından **Invoke Yöntemi**’ni seçin.

1. Ayarlama **iş adı** çok**bellenim güncelleştirme tooversion 2.0**.

1. Seçin **InitiateFirmwareUpdate** hello olarak **yöntemi**.

1. Set hello **FwPackageUri** parametresi çok**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. **Zamanlama**’yı seçin. Merhaba varsayılan hello iş toorun için sunulmuştur.

    ![İş tooupdate hello bellenim seçili hello aygıtların oluşturma][img-method-update]

> [!NOTE]
> Tek bir cihaza bir yöntem tooinvoke istiyorsanız, tercih **yöntemleri** hello içinde **cihaz ayrıntıları** bir iş çalıştırmak yerine paneli.

Bu iş hello çağırır **InitiateFirmwareUpdate** hello Filtresi tarafından seçilen tüm hello cihazlarda yöntemi doğrudan. Aygıtları hemen tooIoT Hub yanıt ve hello bellenim güncelleştirme işlemini zaman uyumsuz olarak başlatır. Merhaba aygıtlar hello ekran görüntüleri aşağıdaki gösterildiği gibi hello bellenim güncelleştirme işlemini bildirilen özellik değerleri ile ilgili durum bilgilerini sağlar. Merhaba seçin **yenileme** hello cihaz ve iş listelerindeki simgesi tooupdate hello bilgileri:

![Merhaba bellenim güncelleştirme listesi çalışan gösteren iş listesi][img-update-1]
![bellenim güncelleştirme durumunu gösteren cihaz listesi][img-update-2]
![iş listesini gösteren hello bellenim güncelleştirme listesi tamamlandı][img-update-3]

> [!NOTE]
> Bir üretim ortamında, belirlenen bakım penceresi sırasında işleri toorun zamanlayabilirsiniz.

## <a name="scenario-review"></a>Senaryo gözden geçirme

Bu senaryoda, bazı hello alarm geçmişi hello Pano ve bir filtre kullanarak uzak aygıtlarınız ile olası bir sorunu tanımlanır. Ardından kullanılan hello filtre ve iş tooremotely hello aygıtları tooprovide yapılandırmak daha fazla bilgi toohelp hello sorunu tanılamak. Son olarak, bir filtre ve iş tooschedule bakım etkilenen hello cihazlarda kullanılır. Toohello Pano döndürmesi durumunda olduğunu artık çözümünüzdeki aygıtlardan gelen uyarılar kontrol edebilirsiniz. Bir filtre kullanabilirsiniz bellenim hello tooverify çözümünüzdeki tüm hello cihazlarda güncel olduğunu ve artık uygun olmayan cihazlar:

![Tüm cihazlarda güncel üretici yazılımı olduğunu gösteren filtre][img-updated]

![Tüm cihazların sistem durumunun iyi olduğunu gösteren filtre][img-healthy]

## <a name="other-features"></a>Diğer özellikler

Merhaba aşağıdaki bölümlerde hello önceki senaryoda bir parçası olarak açıklanmamaktadır, bazı ek hello Uzaktan izleme çözümü özelliklerini açıklar.

### <a name="customize-columns"></a>Sütunları özelleştirme

Merhaba aygıt listesinde seçerek gösterilen hello bilgileri özelleştirebilirsiniz **sütun düzenleyicisini**. Bildirilen özellik ve etiket değerlerini gösteren sütunlar ekleyip kaldırabilirsiniz. Ayrıca, sütunları yeniden sıralayabilir ve yeniden adlandırabilirsiniz:

   ![Sütun Düzenleyicisi nleri hello cihaz listesi][img-columneditor]

### <a name="customize-hello-device-icon"></a>Merhaba aygıtı simgesi özelleştirme

Merhaba hello aygıt listesinden görüntülenen hello aygıtı simgesi özelleştirebilirsiniz **cihaz ayrıntıları** gibi panel:

1. Merhaba Kurşun Kalem simgesini tooopen hello seçin **görüntü Düzenle** paneli bir aygıt için:

   ![Cihaz görüntüsü düzenleyicisini açma][img-startimageedit]

1. Ya da yeni bir resim yükleyin veya hello mevcut görüntülerden birini kullanın ve ardından **kaydetmek**:

   ![Cihaz görüntüsü düzenleyicisini düzenleme][img-imageedit]

1. Merhaba şimdi seçtiğiniz görüntüsü görüntüler hello **simgesi** hello cihaz için sütun.

> [!NOTE]
> Merhaba görüntü blob depolama alanına depolanır. Merhaba cihaz çifti etiketinde blob depolama bir bağlantı toohello görüntüsü içerir.

### <a name="add-a-device"></a>Cihaz ekleme

Merhaba önceden yapılandırılmış çözümü dağıttığınızda, otomatik olarak hello aygıt listesinde görebilirsiniz 25 örnek cihazları hazırlama. Bu cihazlar bir Azure WebJob içinde çalışan *sanal cihazlardır*. Sanal cihazlar sizin için tooexperiment hello gerek toodeploy gerçek fiziksel aygıtları olmadan hello önceden yapılandırılmış Çözümle kolaylaştırır. Merhaba tooconnect gerçek cihaz toohello çözümü istiyorsanız bkz [Uzaktan izleme çözümü, aygıt toohello bağlanmak] [ lnk-connect-rm] Öğreticisi.

Merhaba aşağıdaki adımlarda size yol gösterecektir tooadd bir sanal cihaz toohello çözüm:

1. Geri toohello cihaz listesine gidin.

1. tooadd bir cihaz seçin **+ Add A Device** sol alt köşede, hello.

   ![Bir aygıt toohello önceden yapılandırılmış Çözüm Ekle][img-adddevice]

1. Seçin **yeni Ekle** hello üzerinde **benzetimli aygıt** döşeme.

   ![Panoda yeni cihaz ayrıntılarını ayarlama][img-addnew]

   Toocreate seçerseniz ek toocreating yeni bir sanal cihaz, ayrıca bir fiziksel cihaz ekleyebilirsiniz bir **özel cihaz**. fiziksel aygıtların toohello çözümünü bağlama hakkında daha fazla toolearn bkz [, aygıt toohello IOT paketi Uzaktan izleme çözümü bağlanmak][lnk-connect-rm].

1. **Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin ve **mydevice_01** gibi benzersiz bir cihaz kimliği girin.

1. **Oluştur**’u seçin.

   ![Yeni bir cihaz kaydetme][img-definedevice]

1. 3. adımında **bir sanal cihaz ekleme**, seçin **Bitti** tooreturn toohello aygıt listesinde.

1. Cihazınızı görüntüleyebilirsiniz **çalıştıran** hello aygıt listesinde.

    ![Cihaz listesinde yeni cihazı görüntüleme][img-runningnew]

1. Ayrıca görüntüleyebilirsiniz hello benzetimli hello Panodaki yeni cihazınızdan telemetri:

    ![Yeni cihazdan telemetri görüntüleme][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Bir cihazı devre dışı bırakma ve silme

Bir Cihazı devre dışı bırakabilir, devre dışı kaldıktan sonra da kaldırabilirsiniz:

![Bir cihazı devre dışı bırakma ve kaldırma][img-disable]

### <a name="add-a-rule"></a>Kural ekleme

Yeni eklediğiniz hello yeni cihaz için hiçbir kural vardır. Bu bölümde, hello sıcaklık 47 dereceyi aygıt aşıyor hello yeni raporlanan bir uyarıyı tetikleyen bir kural ekleyin. Başlamadan önce hello hello hello Panoda yeni cihaz için telemetri geçmişinin hello cihaz sıcaklığının hiçbir zaman 45 dereceyi aşmadığını gösterdiğine dikkat edin.

1. Geri toohello cihaz listesine gidin.

1. tooadd hello aygıtı için bir kural hello yeni Cihazınızı seçin **cihazlar listesi**ve ardından **Ekle kuralı**.

1. Kullanan bir kural oluşturmak **sıcaklık** hello veri alanı olarak **AlarmTemp** hello hello sıcaklık 47 dereceyi aştığında çıktı olarak:

    ![Cihaz kuralı ekleme][img-adddevicerule]

1. yaptığınız değişiklikleri toosave seçin **kuralları Kaydet ve görüntüle**.

1. Seçin **komutları** hello cihaz ayrıntıları bölmesinde hello yeni cihaz için.

    ![Cihaz kuralı ekleme][img-adddevicerule2]

1. Seçin **ChangeSetPointTemp** hello komut listesi ve kümesi **SetPointTemp** too45. Ardından **Komut Gönder**’i seçin:

    ![Cihaz kuralı ekleme][img-adddevicerule3]

1. Geri toohello Pano gidin. Kısa bir süre sonra hello yeni bir giriş görürsünüz **Alarm geçmişi** hello sıcaklık yeni cihazınız tarafından raporlanan bölmesinde hello 47 derece eşiğini aşıyor:

    ![Cihaz kuralı ekleme][img-adddevicerule4]

1. Gözden geçirin ve tüm kurallarınızı hello düzenleyin **kuralları** hello Pano sayfası:

    ![Cihaz kurallarını listeleme][img-rules]

1. Gözden geçirin ve yanıt tooa kuralında hello üzerinde gerçekleştirilecek tüm hello Eylemler Düzenle **Eylemler** hello Pano sayfası:

    ![Cihaz eylemlerini listeleme][img-actions]

> [!NOTE]
> Bir e-posta iletisi gönderebilirsiniz olası toodefine Eylemler olduğu veya yanıt tooa SMS kuralı veya bir satır iş kolu sistemiyle tümleştirme bir [mantıksal uygulama][lnk-logic-apps]. Daha fazla bilgi için bkz: Merhaba [bağlanmak mantıksal uygulama tooyour Azure IOT paketi Uzaktan izleme çözümü önceden yapılandırılmış][lnk-logicapptutorial].

### <a name="manage-filters"></a>Filtreleri yönetme

Merhaba aygıt listesinde, oluşturmak, kaydedin ve filtreler toodisplay aygıtları bağlı tooyour hub özelleştirilmiş listesini yeniden yükleyin. bir filtre toocreate:

1. Cihazların Merhaba listesi yukarıda Hello Düzenle filtre simgesini seçin:

    ![Açık hello filtre Düzenleyicisi][img-editfiltericon]

1. Merhaba, **filtre Düzenleyicisi**, hello alanları, işleçler ve değerler toofilter hello cihaz listesi ekleyin. Filtre birden çok yan tümceleri toorefine ekleyebilirsiniz. Seçin **filtre** tooapply hello Filtresi:

    ![Filtre oluşturma][img-filtereditor]

1. Bu örnekte, üretici ve model numarası tarafından hello listesi filtrelenir:

    ![Filtrelenmiş liste][img-filterelist]

1. toosave filtre ile özel bir ad seçin hello **Farklı Kaydet** simgesi:

    ![Filtre kaydetme][img-savefilter]

1. tooreapply daha önce kaydedilmiş bir filtre seçin hello **kaydedilmiş filtre Aç** simgesi:

    ![Filtre açma][img-openfilter]

Cihaz kimliği, cihaz durumu, istenen özellikler, bildirilen özellikler ve etiketlere göre filtreler oluşturabilirsiniz. Kendi özel etiketler tooa aygıt hello eklemek **etiketleri** hello bölümünü **cihaz ayrıntıları** panel ya da bir iş tooupdate etiketleri birden fazla cihazda çalıştırın.

> [!NOTE]
> Merhaba, **filtre Düzenleyicisi**, hello kullanabilirsiniz **Gelişmiş görünümü** tooedit hello sorgu metni doğrudan.

### <a name="commands"></a>Komutlar

Merhaba gelen **cihaz ayrıntıları** paneli, komutları toohello aygıt gönderebilirsiniz. Bir cihaz ilk kez başlatıldığında toohello çözümünü destekler hello hakkında bilgi komutlar gönderir. Komutlar ve yöntemleri arasındaki farklar hello tartışma için bkz [Azure IOT Hub bulut aygıt seçenekleri][lnk-c2d-guidance].

1. Seçin **komutları** hello içinde **cihaz ayrıntıları** Masası hello seçili cihaz için:

   ![Panoda cihaz komutları][img-devicecommands]

1. Seçin **PingDevice** hello komutu listeden.

1. **Komut Gönder**’i seçin.

1. Merhaba komutu hello komut geçmişinde hello durumunu görebilirsiniz.

   ![Panoda komut durumu][img-pingcommand]

Merhaba çözüm, gönderdiği her bir komutun hello durumunu izler. Başlangıçta hello sonucudur **bekleyen**. Merhaba cihaz onu hello komutu yürüttüğünü raporladığında hello sonuç çok kümesi**başarı**.

## <a name="behind-hello-scenes"></a>Merhaba arka planda

Önceden yapılandırılmış çözümü dağıttığınızda, hello dağıtım işlemi hello Seçtiğiniz Azure aboneliği birden çok kaynak oluşturur. Bu kaynaklar hello Azure görüntüleyebilirsiniz [portal][lnk-portal]. Merhaba dağıtım işlemi oluşturur bir **kaynak grubu** önceden yapılandırılmış çözümünüz için seçtiğiniz hello adına dayalı bir ada sahip:

![Önceden yapılandırılmış çözümde hello Azure portalı][img-portal]

Her bir kaynağın hello ayarları hello hello kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.

Merhaba hello önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz. Merhaba uzaktan önceden yapılandırılmış çözümün kaynak kodunu izleme olduğu hello [azure-iot-remote-monitoring] [ lnk-rmgithub] GitHub deposunu:

* Merhaba **DeviceAdministration** klasörü hello hello Pano için kaynak kodunu içerir.
* Merhaba **Simulator** klasörü hello hello sanal cihaz için kaynak kodunu içerir.
* Merhaba **EventProcessor** klasörü hello gelen telemetriyi işleyen hello arka uç işleme için hello kaynak kodunu içerir.

İşiniz bittiğinde, Azure aboneliğinizin hello üzerinde hello önceden yapılandırılmış çözüm silebilirsiniz [azureiotsuite.com] [ lnk-azureiotsuite] site. Bu sitenin tüm hello önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan kaynakları hello tooeasily Sil sağlar.

> [!NOTE]
> her şeyi silin tooensure toohello önceden yapılandırılmış çözümle ilgili, üzerinde hello silme [azureiotsuite.com] [ lnk-azureiotsuite] site ve hello portal hello kaynak grubunda silmeyin.

## <a name="next-steps"></a>Sonraki Adımlar

Çalışan bir önceden çözüm dağıttıktan sonra aşağıdaki makaleler hello okuyarak IOT paketi ile Başlarken devam edebilirsiniz:

* [Uzaktan izleme önceden yapılandırılmış çözüm kılavuzu][lnk-rm-walkthrough]
* [Uzaktan izleme çözümü, aygıt toohello Bağlan][lnk-connect-rm]
* [Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md