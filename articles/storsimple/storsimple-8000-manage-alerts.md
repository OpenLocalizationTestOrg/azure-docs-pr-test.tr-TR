---
title: "aaaView ve StorSimple 8000 serisi cihaz için uyarıları yönetme | Microsoft Docs"
description: "StorSimple uyarı koşulları ve önem derecesi, nasıl tooconfigure uyarı bildirimleri ve nasıl toouse hello StorSimple cihaz Yöneticisi hizmet toomanage uyarıları açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: fdd1a911ceff542bc6bdeae877e1f0fc381bf27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-storsimple-alerts"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti tooview kullanın ve StorSimple Uyarıları yönetme

## <a name="overview"></a>Genel Bakış

Merhaba **uyarıları** dikey penceresinde hello StorSimple cihaz Yöneticisi hizmeti bir yöntem sunar, tooreview ve Temizle StorSimple cihaz – ilgili uyarıları bir gerçek zamanlı olarak. Bu dikey pencereden merkezi olarak StorSimple aygıtlarınızın hello sistem durumu sorunları izleyebilir ve genel Microsoft Azure StorSimple çözümünüzle hello.

Bu öğretici, sık karşılaşılan uyarı koşulları, uyarı önem düzeyleri ve nasıl tooconfigure uyarı bildirimleri açıklar. Ayrıca, tooquickly etkinleştirmek tabloları belirtilen uyarıyı bulmak ve uygun şekilde yanıt uyarı hızlı başvuru içerir.

![Uyarılar sayfası](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="common-alert-conditions"></a>Sık karşılaşılan uyarı koşulları

StorSimple Cihazınızı yanıt tooa çeşitli koşullar uyarılar oluşturur. Merhaba, en yaygın tür uyarı koşulu hello şunlardır:

* **Donanım sorunları** – Bu uyarılar donanımınız hello durumuyla ilgili söyleyin. Bunlar, bir ağ arabirimi sorunlar varsa, bellenim yükseltmeleri, gerekiyorsa ya da veri sürücülerinizin biri ile ilgili bir sorun varsa bilmenizi sağlar.
* **Bağlantı sorunları** – Bu uyarılar veri aktarma zorluk olduğunda oluşur. İletişim sorunları, veri tooand aktarımı sırasında gerçekleşebilir, hello Azure depolama hesabı ya da son toolack hello cihazlarla hello StorSimple cihaz Yöneticisi hizmeti arasındaki bağlantı. İletişim sorunları hatanın çok fazla sayıda noktası olmadığından hello en zor toofix bazılarıdır. Her zaman ilk sorun giderme Gelişmiş üzerinde toomore devam etmeden önce ağ bağlantısı ve Internet erişimi kullanılabilir olduğunu doğrulamanız gerekir. Sorun giderme ile ilgili daha fazla yardım için çok gidin[hello Bağlantıyı Sına cmdlet ile ilgili sorunları giderme](storsimple-troubleshoot-deployment.md).
* **Performans sorunlarını** – sisteminizi ağır bir yük altında olduğu zaman gibi en iyi şekilde gerçekleştirirken değil, bu uyarılar nedeniyle oluşur.

Ayrıca, uyarıları ilgili toosecurity, güncelleştirmeleri veya iş hataları görebilirsiniz.

## <a name="alert-severity-levels"></a>Uyarı önem düzeyleri

Uyarıları farklı önem düzeyleri vardır, hello hello etkisine bağlı olarak uyarı durumu sahip ve bir yanıt toohello uyarısı gereksinimini hello. Merhaba önem düzeyleri şunlardır:

* **Kritik** – bu uyarı hello başarılı sisteminizin performansını etkileyen yanıt tooa içinde bir durumdur. Merhaba StorSimple hizmeti kesintiye uğramaz gerekli tooensure bir eylemdir.
* **Uyarı** – bu koşul çözümlenen varsa kritik duruma gelebilir. Merhaba durum araştırmak ve herhangi bir eylem gerekli tooclear hello sorun olması gerekir.
* **Bilgi** – bu uyarı sisteminizi yönetme ve izleme de yararlı olabilecek bilgiler içerir.

## <a name="configure-alert-settings"></a>Uyarı ayarlarını yapılandırma

Uyarı koşulu her StorSimple cihazlar için e-posta ile bildirimde toobe isteyip istemediğinizi seçebilirsiniz. Ayrıca, hello e-posta adreslerini girerek diğer uyarı bildirimi alıcılarını tanımlayabilirsiniz **diğer e-posta alıcılarını** kutusu, noktalı virgülle ayrılmış.

> [!NOTE]
> En fazla cihaz başına 20 e-posta adresleri girebilirsiniz.

E-posta bildirim bir aygıt için etkinleştirdikten sonra hello bildirim listesi üyeleri kritik uyarı her oluştuğunda bir e-posta iletisi alır. Merhaba iletileri, gelen gönderilecek  *storsimple-alerts-noreply@mail.windowsazure.com*  ve hello Uyarı koşulu anlatmaktadır. Alıcılar tıklatabilirsiniz **Unsubscribe** tooremove kendilerini hello e-posta bildirim listesinde.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>bir aygıt için uyarıları tooenable e-posta bildirimi
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin. Aygıtların listesi Merhaba, seçin ve tooconfigure istediğiniz hello cihaz seçeneğine tıklayın.
2. Çok Git**ayarları** > **genel** hello cihaz için.

   ![Uyarıları dikey penceresi](./media/storsimple-8000-manage-alerts/configure-alerts-email2.png)
   
2. Merhaba, **genel ayarları** dikey penceresinde çok Git**uyarı ayarları** ve hello aşağıdakileri ayarlayın:
   
   1. Merhaba, **gönderme e-posta bildirimi** alan, select **Evet**.
   2. Merhaba, **hizmet yöneticilerinin e-posta** alan, select **Evet** toohave hello Hizmet Yöneticisi ve tüm ortak Yöneticiler hello uyarı bildirimleri alma.
   3. Merhaba, **diğer e-posta alıcılarını** alanında, hello hello uyarı bildirimleri alması gereken diğer tüm alıcıların e-posta adreslerini girin. Merhaba biçiminde adlarını girin  *someone@somewhere.com* . Noktalı virgül tooseparate hello e-posta adresi kullanın. En fazla cihaz başına 20 e-posta adresleri yapılandırabilirsiniz. 
      
3. bir test e-posta bildirimi toosend tıklatın **test e-postası gönderme**. Merhaba test bildirimi iletir gibi hello StorSimple cihaz Yöneticisi hizmeti durum iletilerini görüntüler.

    ![Uyarı ayarlarını](./media/storsimple-8000-manage-alerts/configure-alerts-email3.png)

4. Merhaba test e-posta gönderilirken bir bildirim görür. 
   
    ![Gönderilen bildirim e-posta uyarıları test](./media/storsimple-8000-manage-alerts/configure-alerts-email4.png)
   
   > [!NOTE]
   > Merhaba test ederseniz bildirim iletisi gönderilemiyor, hello StorSimple cihaz Yöneticisi hizmeti uygun bir hata iletisi görüntülenir. Birkaç dakika bekleyin ve ardından toosend sınama bildirim iletisini yeniden deneyin. 

5. Merhaba yapılandırmasını tamamladıktan sonra tıklayın **kaydetmek**. Onayınız istendiğinde **Evet**’e tıklayın.

     ![Gönderilen bildirim e-posta uyarıları test](./media/storsimple-8000-manage-alerts/configure-alerts-email5.png)

## <a name="view-and-track-alerts"></a>Görünüm ve izleme uyarıları

Merhaba StorSimple cihaz Yöneticisi hizmeti Özet dikey bir bakışta uyarı önem düzeyine göre düzenlenmiş cihazlarınızda hello sayısını sağlar.

![Uyarılar Panosu](./media/storsimple-8000-manage-alerts/device-summary4.png)

Merhaba önem düzeyi tıklatıldığında açılır hello **uyarıları** dikey. Bu önem düzeyi eşleşen hello uyarıları Hello sonuçları içerir.

Hello listesindeki bir uyarı tıklayarak, ek ayrıntılarla hello uyarı sağlar, dahil olmak üzere hello son zaman hello uyarı bildirildi, eylem tooresolve hello uyarı hello hello cihaz ve hello hello uyarının yineleme sayısı önerilir. Donanım uyarı ise, bu da hello donanım bileşeni tanımlar.

![Donanım uyarı örneği](./media/storsimple-8000-manage-alerts/configure-alerts-email14.png)

Toosend hello bilgi tooMicrosoft destek gerekiyorsa hello uyarı ayrıntılarını tooa metin dosyalarını kopyalayabilirsiniz. Hello öneri takip edip hello Uyarı koşulu şirket içi çözümledikten sonra hello hello uyarı seçerek hello uyarı hello aygıttan temizlemelidir **uyarıları** dikey ve tıklayarak **temizleyin**. birden çok uyarı, select her uyarı, tooclear tıklatın hello dışında herhangi bir sütun **uyarı** sütun ve ardından **Temizle** seçtikten sonra tüm uyarıları toobe temizlenmiş hello. Bazı uyarılar otomatik olarak hello sorun çözüldüğünde veya hello sistem hello uyarı yeni bilgilerle güncelleştirir temizlenir unutmayın.

Tıkladığınızda **Temizle**, hello fırsat tooprovide açıklamaları hello uyarı hakkında sahip olur ve tooresolve sürdü hello adımları hello sorun. Başka bir olay yeni bilgilerle tetikleniyorsa, bazı olaylar hello sistem tarafından temizlenir. Bu durumda, sonraki hello görürsünüz.

![Temiz uyarı iletisi](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Sıralama ve İnceleme uyarıları

Böylece gözden geçirin ve bunları gruplara temizleyin, uyarıları daha verimli toorun raporlarda bulabilirsiniz. Ayrıca, hello **uyarıları** dikey too250 uyarılarını görüntüleyebilir. Bu uyarı sayısı aşılırsa, tüm uyarıları hello varsayılan görünümünde görüntülenir. Hangi uyarılar görüntülenir alanları toocustomize aşağıdaki hello birleştirebilirsiniz:

* **Durum** – ya da görüntüleyebilirsiniz **etkin** veya **temizlenmiş** uyarıları. Temizlenmiş uyarıları da el ile bir yönetici tarafından temizlenmiş veya hello sistem yeni bilgilerle hello Uyarı koşulu güncelleştirilmediğinden programlı olarak işaretli sırada etkin uyarılar hala, sisteminizde tetiklenen.
* **Önem derecesi** – tüm önem düzeyleri (kritik, uyarı, bilgi) ya da yalnızca bir belirli önem derecesi, yalnızca kritik uyarıları gibi uyarıları görüntüleyebilirsiniz.
* **Kaynak** – tüm kaynaklardan gelen uyarıları görüntülemek veya hello hizmeti veya bir ya da tüm hello cihazlarını gelen hello uyarıları toothose sınırlandırın.
* **Zaman aralığı** – hello belirterek **gelen** ve **için** tarih ve zaman damgaları göz önünde bulundurmanız uyarılara hello ilgilendiğiniz zaman aralığı sırasında.

![Uyarılar listesinde](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="alerts-quick-reference"></a>Uyarıları hızlı başvuru

Aşağıdaki tablolar hello, ek bilgi ve öneriler yanı sıra kullanılabiliyorsa karşılaşabileceğiniz hello Microsoft Azure StorSimple uyarıları bazıları listeleyin. StorSimple cihaz uyarıları kategorileri aşağıdaki hello birine ayrılır:

* [Bulut bağlantı uyarıları](#cloud-connectivity-alerts)
* [Küme uyarıları](#cluster-alerts)
* [Olağanüstü durum kurtarma uyarıları](#disaster-recovery-alerts)
* [Donanım uyarıları](#hardware-alerts)
* [İş hatası uyarıları](#job-failure-alerts)
* [Yerel olarak sabitlenmiş birim uyarılarını](#locally-pinned-volume-alerts)
* [Ağ uyarıları](#networking-alerts)
* [Performans uyarıları](#performance-alerts)
* [Güvenlik Uyarıları](#security-alerts)
* [Destek Paketi uyarıları](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Bulut bağlantı uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Bağlantı çok <*bulut kimlik bilgisi adı*> oluşturulamıyor. |Toohello depolama hesabı bağlantı kurulamıyor. |Cihazınız ile bir bağlantı sorunu olabilir gibi görünüyor. Lütfen hello çalıştırın `Test-HcsmConnection` cmdlet'i, aygıt tooidentify StorSimple için Windows PowerShell arabirimini hello ve hello sorunu düzeltin. Hello ayarlarının doğru olup olmadığını hello uyarının gerçekleşmesine neden olan hello depolama hesabı hello kimlik bilgileriyle hello sorunu olabilir. Bu durumda, hello kullanarak `Test-HcsStorageAccountCredential` çözebilmek için bir sorun varsa cmdlet toodetermine.<ul><li>Ağ ayarlarınızı denetleyin.</li><li>Depolama hesabı kimlik bilgilerinizi denetleyin.</li></ul> |
| Bir sinyal cihazınızdan hello için son aldık değil <*numarası*> dakika. |Toodevice bağlanamıyor. |Bir bağlantı sorunu aygıtınızda gibi görünüyor. Lütfen hello kullanın `Test-HcsmConnection` cmdlet'i, aygıt tooidentify StorSimple için Windows PowerShell arabirimini hello ve hello sorununu düzeltin veya ağ yöneticinize başvurun. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>Bulut bağlantı başarısız olduğunda StorSimple davranışı

Üretimde çalışan StorSimple Cihazınızı için bulut bağlantı başarısız olursa ne olur?

StorSimple üretim Cihazınızda bulut bağlantı başarısız olursa, cihazın hello durumuna bağlı olarak hello aşağıdaki oluşabilir:

* **Aygıtınızdaki hello yerel veriler için**: süre için olacaktır hiçbir kesintisi ve okuma sunulan toobe devam edecek. Ancak, bekleyen GÇ Hello sayısını artırır ve bir sınırı aşan gibi hello okuma toofail başlayamadı.

    Merhaba veri miktarına bağlı olarak, Cihazınızda, hello yazma de toooccur hello için ilk birkaç saat sonra hello kesintisi hello bulut Bağlantısı'nda devam eder. Merhaba yazma sonra yavaşlayabilir ve hello bulut bağlantı birkaç saat boyunca kesintiye uğrarsa toofail sonunda başlatın. (Yoktur geçici depolama hello cihazda toobe toohello bulut gönderilen veriler için. Merhaba veri gönderildiğinde, bu alanı temizlenir. Bağlantı başarısız olursa, bu depolama alanındaki verileri toohello bulut gönderilen değil ve g/ç başarısız olur.)
* **Merhaba bulutta hello veriler için**: çoğu bulut bağlantı hataları için hata döndürülür. Merhaba bağlantı geri yüklendikten sonra hello IOs toobring hello birim çevrimiçi sahip hello kullanıcı sürdürülür. Nadir durumlarda, kullanıcı müdahalesi gerekli toobring geri hello birimden çevrimiçi hello Azure portal olabilir.
* **Devam eden bulut anlık görüntüleri için**: hello işlemi birkaç kez 4-5 saat içinde yeniden deneme ve hello bağlantı geri yüklenmez hello bulut anlık görüntüleri başarısız olur.

### <a name="cluster-alerts"></a>Küme uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Aygıt başarısız üzerinden çok <*aygıt adı*>. |Cihaz bakım modunda değil. |Tooentering veya mevcut Bakım modu üzerinden aygıt başarısız oldu. Bu normaldir ve Eylem gerekmiyor. Bu uyarı onaylanan sonra hello uyarıları sayfasından temizleyin. |
| Aygıt başarısız üzerinden çok <*aygıt adı*>. |Cihaz üretici yazılımını veya yazılım yalnızca güncelleştirildi. |Bir küme yük devretmesi tooan güncelleştirme nedeniyle oluştu. Bu normaldir ve Eylem gerekmiyor. Bu uyarı onaylanan sonra hello uyarıları sayfasından temizleyin. |
| Aygıt başarısız üzerinden çok <*aygıt adı*>. |Denetleyici kapatıldı veya yeniden. |Merhaba etkin denetleyicisi kapatıldı veya bir yönetici tarafından yeniden için cihaz üzerinde başarısız oldu. Eylem gerekmiyor. Bu uyarı onaylanan sonra hello uyarıları sayfasından temizleyin. |
| Aygıt başarısız üzerinden çok <*aygıt adı*>. |Planlanan yük devretme. |Planlanmış bir yük devretme olduğunu doğrulayın. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |
| Aygıt başarısız üzerinden çok <*aygıt adı*>. |Planlanmamış yük devretme. |StorSimple planlanmamış yük devretmeler tooautomatically bozulmayı yerleşik olarak bulunur. Bu uyarılar çok sayıda görürseniz, Microsoft Support başvurun. |
| Aygıt başarısız üzerinden çok <*aygıt adı*>. |Diğer/bilinmeyen neden. |Bu uyarılar çok sayıda görürseniz, Microsoft Support başvurun. Merhaba sorun çözüldükten sonra bu uyarı hello uyarıları sayfasından temizleyin. |
| Bir kritik aygıt hizmet durumu başarısız olarak bildirir. |DataPath Hizmeti hatası. |Yardım için Microsoft Support başvurun. |
| Ağ arabirimi için sanal IP adresi <*veri #*> durumu başarısız olarak bildirir. |Diğer/bilinmeyen neden. |Bazen geçici koşullar, bu uyarılar neden olabilir. Bu hello durumda ise, bu uyarıyı otomatik olarak bir süre sonra temizlenir. Merhaba sorun devam ederse, Microsoft Support başvurun. |
| Ağ arabirimi için sanal IP adresi <*veri #*> durumu başarısız olarak bildirir. |Arabirim adı: <*veri #*> IP adresi <IP address> hello ağ üzerinde yinelenen bir IP adresi algılandığından çevrimiçi duruma getirilemiyor. |Merhaba yinelenen IP adresi hello ağdan kaldırıldığından emin olmak veya farklı bir IP adresi ile Merhaba arabirimi yeniden yapılandırın. |

### <a name="disaster-recovery-alerts"></a>Olağanüstü durum kurtarma uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Kurtarma işlemlerinin tümü hello ayarlarını bu hizmet için geri yüklenemedi. Aygıt yapılandırma verilerini bazı cihazlar için tutarsız bir durumda değil. |Veri tutarsızlığı olağanüstü durum kurtarma işleminden sonra algılandı. |Merhaba hizmetinde şifrelenmiş veriler ile Merhaba aygıtta eşitlenmemiş. Merhaba aygıt yetkilendirmek <*aygıt adı*> StorSimple Aygıt Yöneticisi'ni toostart hello eşitleme işleminden. StorSimple toorun hello kullan Merhaba Windows PowerShell arabirimini `Restore-HcsmEncryptedServiceData` aygıtta <*aygıt adı*> cmdlet, hello eski parola bir giriş toothis cmdlet toorestore hello güvenlik profili sağlama. Merhaba çalıştırmak `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet tooupdate hello hizmet verileri şifreleme anahtarı. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |

### <a name="hardware-alerts"></a>Donanım uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Donanım bileşeni <*bileşen kimliği*> olarak durumu raporları <*durum*>. | |Bazen geçici koşullar, bu uyarılar neden olabilir. Öyleyse, bu uyarı bir süre sonra otomatik olarak temizlenir. Merhaba sorun devam ederse, Microsoft Support başvurun. |
| Pasif denetleyiciyi hatalı. |Merhaba Pasif (ikincil) denetleyicisi çalışmıyor. |Cihazınızı işlevseldir ancak denetleyicilerinizi birini düzgün çalışmıyor. Bu denetleyici yeniden başlatmayı deneyin. Merhaba sorun giderilmezse Microsoft Support başvurun. |

### <a name="job-failure-alerts"></a>İş hatası uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Yedeklemeyi <*kaynak birim grubu kimliği*> başarısız oldu. |Yedekleme işi başarısız oldu. |Bağlantı sorunları hello yedekleme işlemi başarıyla tamamlanmasını engelliyor. Hiçbir bağlantı sorunları varsa, yedeklemeler hello sayısı sınırına. Hello işlemi yeniden deneyin ve artık gerekli olmayan tüm yedeklemeler silin. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |
| Kopyalama <*yedekleme öğesi kimlikleri kaynak*> çok <*hedef birim seri numaraları*> başarısız oldu. |Kopyalama işi başarısız oldu. |Yedekleme hello yenileme hello yedekleme listesi tooverify hala geçerlidir. Merhaba yedekleme geçerliyse, bulut bağlantı sorunları hello kopyalama işlemi başarıyla tamamlanmasını engelliyor mümkündür. Hiçbir bağlantı sorunları varsa, hello depolama sınırına ulaşmış olabilirsiniz. Hello işlemi yeniden deneyin ve artık gerekli olmayan tüm yedeklemeler silin. Uygun eylemi tooresolve hello sorunu attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |
| Geri Yükleme <*yedekleme öğesi kimlikleri kaynak*> başarısız oldu. |Geri yükleme işi başarısız oldu. |Yedekleme hello yenileme hello yedekleme listesi tooverify hala geçerlidir. Merhaba yedekleme geçerliyse, bulut bağlantı sorunları hello geri yükleme işlemi başarıyla tamamlanmasını engelliyor mümkündür. Hiçbir bağlantı sorunları varsa, hello depolama sınırına ulaşmış olabilirsiniz. Hello işlemi yeniden deneyin ve artık gerekli olmayan tüm yedeklemeler silin. Uygun eylemi tooresolve hello sorunu attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |

### <a name="locally-pinned-volume-alerts"></a>Yerel olarak sabitlenmiş birim uyarılarını

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Yerel birim oluşturulmasını <*birim adı*> başarısız oldu. |Merhaba birim oluşturma işi başarısız oldu. <*Hata iletisi karşılık gelen toohello başarısız oldu, hata kodu*>. |Bağlantı sorunları hello alanı oluşturma işlemi başarıyla tamamlanmasını engelliyor. Yerel olarak sabitlenmiş birimlerin sıkı sağlanır ve katmanlı birimleri toohello bulut değişkenlere alanı oluşturma hello işlemi içerir. Hiçbir bağlantı sorunları varsa, hello cihazda yerel alan hello tüketmiş olabilir. Bu işlemi yeniden denemeden önce alanı hello aygıtta olup olmadığını belirler. |
| Yerel birim genişlemesi <*birim adı*> başarısız oldu. |Merhaba birim değişikliği işi başarısız oldu son çok <*hata iletisi karşılık gelen toohello başarısız oldu, hata kodu*>. |Bağlantı sorunları hello Birim genişletme işlemi başarıyla tamamlanmasını engelliyor. Yerel olarak sabitlenmiş birimlerin sıkı sağlanır ve katmanlı birimleri toohello bulut değişkenlere hello mevcut alanını genişletme hello işlemi içerir. Hiçbir bağlantı sorunları varsa, hello cihazda yerel alan hello tüketmiş olabilir. Bu işlemi yeniden denemeden önce alanı hello aygıtta olup olmadığını belirler. |
| Birim dönüştürülmesi <*birim adı*> başarısız oldu. |Merhaba toplu dönüştürme işi tooconvert hello birim türünden yerel olarak sabitlenmiş tootiered başarısız oldu. |Yerel olarak sabitlenmiş türü tootiered hello birimin dönüştürme tamamlanamadı. Merhaba işlemin başarıyla tamamlanmasını engelleyen bir bağlantı sorunu olmadığından emin olun. Bağlantı sorunlarını giderme için sorunları çok Git[hello Test HcsmConnection cmdlet ile ilgili sorunları giderme](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>yerel olarak sabitlenmiş hello birimden hello verilerin bazıları geçmiş bu yana toohello bulut hello dönüştürme sırasında hello özgün yerel olarak sabitlenmiş birim artık katmanlı birim işaretlendi. Merhaba sonuç katmanlı birim hala geri kazanılacak hello cihazı gelecekteki yerel birimleri için yerel alan bırakmalısınız.<br>Tüm bağlantı sorunlarını giderin, hello uyarı temizleyin ve tüm hello verileri kullanımına sunulur yerel olarak yeniden bu birimi geri toohello özgün yerel olarak sabitlenmiş bir birim türü tooensure dönüştürün. |
| Birim dönüştürülmesi <*birim adı*> başarısız oldu. |Merhaba toplu dönüştürme işi tooconvert hello birim türünden sabitlenmiş katmanlı toolocally başarısız oldu. |Katmanlı toolocally sabitlenmiş türüne hello birimin dönüştürme tamamlanamadı. Merhaba işlemin başarıyla tamamlanmasını engelleyen bir bağlantı sorunu olmadığından emin olun. Bağlantı sorunlarını giderme için sorunları çok Git[hello Test HcsmConnection cmdlet ile ilgili sorunları giderme](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>Merhaba özgün katmanlı birim hello dönüştürme işleminin bir parçası hello sıkı alanı hello cihazda bu birim için sağlanan sırada hello bulutta bulunan toohave veri devam ettikçe şimdi yerel olarak sabitlenmiş bir birim işaretlenmiş artık için gelecekteki yerel istenemiyor birimler.<br>Sıkı hello cihazda sağlanan bu birim geri toohello özgün katmanlı birim türü tooensure yerel alanı geri dönüştürme, Temizle hello uyarı ve bağlantı sorunları giderin. |
| Yerel alan tüketim yerel anlık görüntüleri için yaklaşan <*birim grubu adı*> |Hello yedekleme ilkesi için yerel anlık görüntüler yakında alanı kalmadı ve konak yazma hataları geçersiz kılınan tooavoid olması. |Bu yedekleme İlkesi grubuyla ilişkilendirilmiş hello birimlerdeki yüksek veri karmaşası yanında sık yerel anlık görüntüleri yerel alan hızla tüketilen hello aygıt toobe üzerinde neden oluyor. Artık gerekli olmayan tüm yerel anlık görüntüleri silin. Ayrıca, bu yedekleme İlkesi tootake daha az sık yerel anlık görüntüler için yerel anlık görüntü zamanlamalarınızı güncelleştirin ve bulut anlık görüntüleri düzenli olarak gerçekleştirilecek emin olun. Bu eylemleri alınmaz, bu anlık görüntüler için yerel alan yakında tükendi ve hello sistem otomatik olarak başarıyla işlenen toobe konak yazma işlemleri devam tooensure silin. |
| Yerel anlık görüntüleri <*birim grubu adı*> geçersiz hale getirildi. |Yerel anlık görüntüleri merhaba <*birim grubu adı*> geçersiz kılınan ve hello cihazda yerel alan hello aşan silinemiyor. |Merhaba gelecekteki oluşmaz tooensure Bu yedekleme ilkesi için hello yerel anlık görüntü zamanlama gözden geçirin ve artık gerekli olmayan tüm yerel anlık görüntüleri silin. Bu yedekleme İlkesi grubuyla ilişkilendirilmiş hello birimlerdeki yüksek veri karmaşası yanında sık yerel anlık görüntüleri yerel alan hızla tüketilen hello aygıt toobe üzerinde neden olabilir. |
| Geri Yükleme <*yedekleme öğesi kimlikleri kaynak*> başarısız oldu. |Merhaba geri yükleme işi başarısız oldu. |Yerel olarak sabitlenmiş ya da bu yedekleme İlkesi yedekleme hello yenileme hello yedekleme listesi tooverify yerel olarak sabitlenmiş ve katmanlı birimlerin bir karışımını hala geçerli ise. Merhaba yedekleme geçerliyse, bulut bağlantı sorunları hello geri yükleme işlemi başarıyla tamamlanmasını engelliyor mümkündür. Bu anlık görüntü grubunun parçası tüm kullanıcıların verileri indirilen toohello cihaz yoktur ve bu anlık görüntü grubundaki bir katmanlı ve yerel olarak sabitlenmiş birimleri karışımı varsa, birbirleri ile eşitlenmiş olmaz gibi geri yüklenmekte birimleri Hello yerel olarak sabitlenmiş. toosuccessfully hello geri yükleme işlemini, bu gruptaki çevrimdışı hello konaktaki hello birimlerinin almak ve hello geri yükleme işlemi yeniden deneyin. Geri yükleme işlemi sırasında hello gerçekleştirilen tüm değişiklikler toohello birim verilerini Not kaybolur. |

### <a name="networking-alerts"></a>Ağ uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| StorSimple hizmetleri başlayamadı. |DataPath hata |Merhaba sorun devam ederse, Microsoft Support başvurun. |
| Yinelenen IP adresi 'Data0 için' algılandı. | |Merhaba sistem '10.0.0.1' IP adresi için bir çakışma algıladı. Ağ kaynağına 'Data0' hello aygıtta Hello  *<device1>*  çevrimdışı. Bu IP adresi bu ağdaki herhangi bir varlık tarafından kullanılmaz emin olun. tootroubleshoot ağ sorunları, Git çok[hello Get-NetAdapter cmdlet ile ilgili sorunları giderme](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Bu sorunu çözme konusunda yardım almak için ağ yöneticinize başvurun. Merhaba sorun devam ederse, Microsoft Support başvurun. |
| IPv4 (veya IPv6) 'Data0' Çevrimdışı adresidir. | |IP adresi '10.0.0.1.' ile 'Data0' Hello ağ kaynağı ve önek uzunluğu '22' hello aygıtta  *<device1>*  çevrimdışı. Bu arabirime bağlı o hello anahtar bağlantı noktalarını toowhich işletimsel olduğundan emin olun. tootroubleshoot ağ sorunları, Git çok[hello Get-NetAdapter cmdlet ile ilgili sorunları giderme](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |
| Toohello kimlik doğrulama hizmeti bağlantısı kurulamadı. |DataPath hata |Merhaba URLthat kullanılan tooauthenticate erişilebilir değil. Güvenlik Duvarı kurallarınız hello StorSimple cihaz için belirtilen hello URL desenlerini eklediğinizden emin olun. Azure portalında URL desenlerini hakkında daha fazla bilgi için toohttps://aka.ms/ss-8000-network-reqs gidin. Azure Bulutu kullanıyorsanız, https://aka.ms/ss8000-gov-network-reqs toohello URL düzenleri gidin.|

### <a name="performance-alerts"></a>Performans uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Merhaba aygıt yük aştı <*eşik*>. |Beklenen yanıt süreleri daha yavaş çalışır. |Cihazınızı kullanımı ağır bir giriş/çıkış yük altında bildirir. Bu cihaz toonot çalışmanızı yanı sıra gerektiği neden olabilir. Toohello aygıt eklenmiş ve olup olmadığını tooanother aygıt ya da, artık gerekli olmayan taşınamıyor herhangi belirlemek hello iş yükleri gözden geçirin.| StorSimple hizmetleri başlayamadı. |DataPath hata |Merhaba sorun devam ederse, Microsoft Support başvurun. |ve hello geçerli durumu, çok gidin[kullanım Cihazınızı StorSimple cihaz Yöneticisi hizmeti toomonitor hello](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Güvenlik uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Microsoft Support oturumu başladı. |Üçüncü taraf destek oturum erişilir. |Lütfen bu erişim yetkisi onaylayın. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |
| Parola <*öğesi*> içinde sona erecek <*süre*>. |Parola geçerlilik süresi yaklaşıyor. |Parolanızı süresi dolmadan önce değiştirin. |
| Güvenlik yapılandırma bilgileri için eksik <*öğesi kimliği*>. | |Bu birim kapsayıcısı ile ilişkili birimi Hello kullanılan tooreplicate StorSimple yapılandırmanızı olamaz. verilerinizi güvenli bir şekilde depolanır tooensure hello birim kapsayıcısı ve hello birim kapsayıcısı ile ilişkili herhangi bir birimi silmek öneririz. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |
| <*sayı*> başarısız oturum açma denemesi <*öğesi kimliği*>. |Birden çok başarısız oturum açma girişimi. |Cihazınızı Saldırıya uğramış olabilir veya yetkili bir kullanıcı yanlış bir parola ile tooconnect deniyor.<ul><li>Yetkili kullanıcılar başvurun ve bu girişimler meşru bir kaynaktan olduğunu doğrulayın. Çok sayıda başarısız oturum açma denemesi toosee devam ederseniz, uzaktan yönetimi devre dışı bırakma ve ağ yöneticinize başvurarak göz önünde bulundurun. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin.</li><li>Anlık Görüntü Yöneticisi'ni örneklerinizi hello doğru parola ile yapılandırılıp yapılandırılmadığını denetleyin. Uygun eylemi attıktan sonra bu uyarıyı hello uyarıları sayfasından temizleyin.</li></ul>Daha fazla bilgi için çok Git[süresi dolmuş cihaz parolasını değiştirme](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Merhaba hizmet verileri şifreleme anahtarı değiştirilirken bir veya daha fazla hata oluştu. | |Merhaba hizmet verileri şifreleme anahtarı değiştirilirken oluşan hatalar vardı. Merhaba hata koşulları ele sonra hello çalıştırın `Invoke-HcsmServiceDataEncryptionKeyChange` hello StorSimple için Windows PowerShell arabirimi aygıt tooupdate hello hizmetinizi üzerinde cmdlet'i. Bu sorun devam ederse Microsoft desteğe başvurun. Merhaba sorunu çözdükten sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |

### <a name="support-package-alerts"></a>Destek Paketi uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Destek paketi oluşturma başarısız oldu. |StorSimple hello paketi oluşturamadı. |Bu işlemi yeniden deneyin. Merhaba sorun devam ederse, Microsoft Support başvurun. Merhaba sorunu çözdükten sonra bu uyarıyı hello uyarıları sayfasından temizleyin. |

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple hataları ve işletimsel bir aygıtı sorun giderme](storsimple-troubleshoot-operational-device.md).

