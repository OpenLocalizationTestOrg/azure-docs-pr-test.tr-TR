---
title: "aaaView ve Microsoft Azure StorSimple sanal dizinin Uyarıları yönetme | Microsoft Docs"
description: "StorSimple sanal dizi uyarı koşulları ve önem derecesi ve nasıl toouse hello StorSimple Yöneticisi hizmet toomanage uyarıları açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Merhaba StorSimple sanal dizinin için Aygıt Yöneticisi'ni StorSimple toomanage uyarıları

## <a name="overview"></a>Genel Bakış

Merhaba StorSimple cihaz Yöneticisi hizmeti Hello uyarıları özelliği, tooreview için bir yol sağlar ve gerçek zamanlı olarak uyarıları ilgili tooStorSimple sanal diziler temizleyin. Merhaba üzerinde hello uyarılar kullanabilirsiniz **hizmet özeti** dikey toocentrally StorSimple sanal dizileriniz hello sistem durumu sorunlarını izlemek ve hello genel Microsoft Azure StorSimple çözümünüzle.

Bu öğretici önem düzeyleri tooconfigure uyarı bildirimleri, genel uyarı koşullar uyarı nasıl ve ne açıklar tooview ve izleme uyarıları. Ayrıca, tooquickly etkinleştirmek tabloları belirtilen uyarıyı bulmak ve uygun şekilde yanıt uyarı hızlı başvuru içerir.

![Uyarılar sayfası](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Uyarı ayarlarını yapılandırma

Merhaba uyarı koşulların her StorSimple sanal dizileriniz için e-posta ile bildirimde toobe isteyip istemediğinizi seçebilirsiniz. Ayrıca, hello e-posta adreslerini girerek diğer uyarı bildirimi alıcılarını tanımlayabilirsiniz **ek e-posta alıcılarını** kutusu, noktalı virgülle ayrılmış.

> [!NOTE]
> En fazla 20 e-posta adreslerini sanal dizi başına girebilirsiniz.


Bir sanal dizini e-posta bildirimi etkinleştirdikten sonra hello bildirim listesi üyeleri kritik uyarı her oluştuğunda bir e-posta iletisi alır. Merhaba iletileri, gelen gönderilecek  *storsimple-alerts-noreply@mail.windowsazure.com*  ve hello Uyarı koşulu anlatmaktadır. Alıcılar tıklatabilirsiniz **Unsubscribe** tooremove kendilerini hello e-posta bildirim listesinde.

#### <a name="tooenable-email-notification-for-alerts"></a>Uyarılar için e-posta bildirimleri tooenable

1. Hizmet ve hello tooyour StorSimple Aygıt Yöneticisi'ni Git **Yönetim** bölümünde, seçin ve'ı tıklatın **aygıtları**. Görüntülenen cihaz hello listesini seçin ve aygıtınızı tıklatın.
   
    ![Uyarı ayarlarını](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Merhaba açılır **ayarları** dikey. Merhaba, **aygıt ayarları** bölümünde, select **genel**. Merhaba açılır **genel ayarları** dikey.
   
    ![Uyarı bildirim yapılandırması](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. Merhaba, **genel ayarları** dikey penceresinde çok Git**uyarı ayarları** bölümünde ve hello aşağıdakileri ayarlayın:
   
   1. Merhaba, **e-posta bildirimi etkinleştir** alan, select **Evet**.
   2. Merhaba, **hizmet yöneticilerinin e-posta** alan, select **Evet** toohave hello Hizmet Yöneticisi istiyor ve tüm ortak Yöneticiler hello uyarı bildirimleri alma.
   3. Merhaba, **ek e-posta alıcılarını** alanında, hello hello uyarı bildirimleri alması gereken diğer tüm alıcıların e-posta adreslerini girin. Merhaba biçiminde adlarını girin  *someone@somewhere.com* . Noktalı virgül tooseparate hello e-posta adresi kullanın. Maksimum sanal aygıt başına 20 e-posta adresi yapılandırabilirsiniz.
      
       ![Uyarı bildirim yapılandırması](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. bir test e-posta bildirimi toosend tıklatın **test e-postası gönderme**. Merhaba test bildirimi iletir gibi hello StorSimple cihaz Yöneticisi hizmeti durum iletilerini görüntüler.
      
       ![Gönderilen bildirim e-posta uyarıları test](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Merhaba test ederseniz bildirim iletisi gönderilemiyor, hello StorSimple cihaz Yöneticisi hizmeti uygun bir mesaj görüntüler. Tıklatın **Tamam**, birkaç dakika bekleyin ve sonra toosend sınama bildirim iletisini yeniden deneyin.
      > 
      > 
   5. Merhaba sayfasının Hello altında tıklatın **kaydetmek** toosave yapılandırmanızı. Onayınız istendiğinde **Evet**’e tıklayın.
      
      ![Gönderilen bildirim e-posta uyarıları test](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Sık karşılaşılan uyarı koşulları

StorSimple sanal dizinizi yanıt tooa çeşitli koşullar uyarılar oluşturur. Merhaba, en yaygın tür uyarı koşulu hello şunlardır:

* **Bağlantı sorunları** – Bu uyarılar veri aktarma zorluk olduğunda oluşur. İletişim sorunları, veri tooand aktarımı sırasında gerçekleşebilir, hello Azure depolama hesabı ya da son toolack hello sanal cihazlar ve hello StorSimple cihaz Yöneticisi hizmeti arasındaki bağlantı. İletişim sorunları hatanın çok fazla sayıda noktası olmadığından hello en zor toofix bazılarıdır. Her zaman ilk sorun giderme Gelişmiş üzerinde toomore devam etmeden önce ağ bağlantısı ve Internet erişimi kullanılabilir olduğunu doğrulamanız gerekir. Bağlantı noktaları ve güvenlik duvarı ayarları hakkında daha fazla bilgi için çok Git[StorSimple sanal dizinin sistem gereksinimleri](storsimple-ova-system-requirements.md). Sorun giderme ile ilgili daha fazla yardım için çok gidin[hello Bağlantıyı Sına cmdlet ile ilgili sorunları giderme](storsimple-troubleshoot-deployment.md).
* **Performans sorunlarını** – sisteminizi ağır bir yük altında olduğu zaman gibi en iyi şekilde gerçekleştirirken değil, bu uyarılar nedeniyle oluşur.

Ayrıca, uyarıları ilgili toosecurity, güncelleştirmeleri veya iş hataları görebilirsiniz.

## <a name="alert-severity-levels"></a>Uyarı önem düzeyleri

Uyarıları farklı önem düzeyleri vardır, hello hello etkisine bağlı olarak uyarı durumu sahip ve bir yanıt toohello uyarısı gereksinimini hello. Merhaba önem düzeyleri şunlardır:

* **Kritik** – bu uyarı hello başarılı sisteminizin performansını etkileyen yanıt tooa içinde bir durumdur. Merhaba StorSimple hizmeti kesintiye uğramaz gerekli tooensure bir eylemdir.
* **Uyarı** – bu koşul çözümlenen varsa kritik duruma gelebilir. Merhaba durum araştırmak ve herhangi bir eylem gerekli tooclear hello sorun olması gerekir.
* **Bilgi** – bu uyarı sisteminizi yönetme ve izleme de yararlı olabilecek bilgiler içerir.

## <a name="view-and-track-alerts"></a>Görünüm ve izleme uyarıları

Merhaba StorSimple cihaz Yöneticisi hizmeti Özet dikey bir bakışta uyarı önem düzeyine göre düzenlenmiş cihazlarınızda sanal hello sayısını sağlar.

![Uyarılar Panosu](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Merhaba önem düzeyi tooopen hello tıklatın **uyarıları** dikey. Bu önem düzeyi eşleşen hello uyarıları Hello sonuçları içerir.

![Uyarılar raporu tooalert türü kapsamı](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Merhaba listesi tooget ek ayrıntıları hello hello uyarı bildirildi, son zamanı hello aygıtta hello uyarı ve hello önerilen eylem tooresolve hello uyarı oluşumları hello sayısı dahil olmak üzere hello uyarı için bir uyarıyı tıklatın.

![Uyarılar listesinde ve ayrıntıları](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Toosend hello bilgi tooMicrosoft destek gerekiyorsa hello uyarı ayrıntılarını tooa metin dosyalarını kopyalayabilirsiniz. Hello öneri takip edip hello Uyarı koşulu şirket içi çözümledikten sonra hello uyarı hello listeden temizlemeniz gerekir. Merhaba uyarı hello listeden seçin ve ardından **Temizle**. birden çok uyarı, select her uyarı, tooclear tıklatın hello dışında herhangi bir sütun **uyarı** sütun ve ardından **Temizle** seçtikten sonra tüm uyarıları toobe temizlenmiş hello.

Tıkladığınızda **Temizle**, hello fırsat tooprovide açıklamaları hello uyarı hakkında sahip olur ve tooresolve sürdü hello adımları hello sorun. 

![Uyarı açıklamaları](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Başka bir olay yeni bilgilerle tetikleniyorsa, bazı olaylar hello sistem tarafından temizlenir. 

## <a name="sort-and-review-alerts"></a>Sıralama ve İnceleme uyarıları

Merhaba **uyarıları** dikey too250 uyarılarını görüntüleyebilir. Bu uyarı sayısı aşılırsa, tüm uyarıları hello varsayılan görünümünde görüntülenir. Hangi uyarılar görüntülenir alanları toocustomize aşağıdaki hello birleştirebilirsiniz:

* **Durum** – ya da görüntüleyebilirsiniz **etkin** veya **temizlenmiş** uyarıları. Temizlenmiş uyarıları da el ile bir yönetici tarafından temizlenmiş veya hello sistem yeni bilgilerle hello Uyarı koşulu güncelleştirilmediğinden programlı olarak işaretli sırada etkin uyarılar hala, sisteminizde tetiklenen.
* **Önem derecesi** – tüm önem düzeyleri (kritik, uyarı, bilgi) ya da yalnızca bir belirli önem derecesi, yalnızca kritik uyarıları gibi uyarıları görüntüleyebilirsiniz.
* **Kaynak** – tüm kaynaklardan gelen uyarıları görüntülemek veya hello hizmeti veya bir gelen hello uyarıları toothose sınırlandırmak veya tüm sanal cihazların Merhaba.
* **Zaman aralığı** – hello belirterek **gelen** ve **için** tarih ve zaman damgaları göz önünde bulundurmanız uyarılara hello ilgilendiğiniz zaman aralığı sırasında.

## <a name="alerts-quick-reference"></a>Uyarıları hızlı başvuru

Aşağıdaki tablolar hello, ek bilgi ve öneriler yanı sıra kullanılabiliyorsa karşılaşabileceğiniz hello StorSimple uyarıları bazıları listeleyin. StorSimple sanal dizinin uyarıları kategorileri aşağıdaki hello birine ayrılır:

* [Bulut bağlantı uyarıları](#cloud-connectivity-alerts)
* [Yapılandırma uyarılarını](#configuration-alerts)
* [İş hatası uyarıları](#job-failure-alerts)
* [Performans uyarıları](#performance-alerts)
* [Güvenlik Uyarıları](#security-alerts)
* [Güncelleştirme uyarıları](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Bulut bağlantı uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Aygıt  *<device name>*  olan toohello bulut bağlanmadı. |cihaz adlı hello toohello bulut bağlanamıyor. |Toohello bulut bağlanamadı. Bu son olabilir hello aşağıdaki tooone:<ul><li>Cihazınızı hello ağ ayarları ile ilgili bir sorun olabilir.</li><li>Merhaba depolama hesabı kimlik bilgileri ile ilgili bir sorun olabilir.</li></ul>Bağlantı sorunlarını giderme hakkında daha fazla bilgi için toohello Git [yerel web kullanıcı Arabirimi](storsimple-ova-web-ui-admin.md) hello cihazın. |

### <a name="configuration-alerts"></a>Yapılandırma uyarılarını

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Şirket içi sanal aygıt yapılandırmasını desteklenmiyor. |Yavaş performans. |Merhaba geçerli yapılandırma, performans düşüşüne neden olabilir. Sunucunuz hello en düşük yapılandırma gereksinimlerini karşıladığından emin olun. Daha fazla bilgi için çok Git[StorSimple sanal dizinin gereksinimleri](storsimple-ova-system-requirements.md). |
| Sağlanan disk alanı yetersiz kullanmakta olduğunuz <*aygıt adı*>. |Disk alanı uyarısı. |Size sağlanan disk alanı azalıyor. toofree alanı, iş yüklerini tooanother birimi veya paylaşımı taşıma veya veri silme göz önünde bulundurun. |

### <a name="job-failure-alerts"></a>İş hatası uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Yedeklemeyi <*aygıt adı*> işlemi tamamlanamadı. |Yedekleme iş başarısız oldu. |Bir yedekleme oluşturulamadı. Merhaba aşağıdakilerden birini göz önünde bulundurun:<ul><li>Bağlantı sorunları hello yedekleme işlemi başarıyla tamamlanmasını engelliyor. Bağlantı sorunu olmadığından emin olun. Bağlantı sorunlarını giderme hakkında daha fazla bilgi için toohello Git [yerel web kullanıcı Arabirimi](storsimple-ova-web-ui-admin.md) sanal cihazınız için.</li><li>Merhaba kullanılabilir depolama sınırına ulaştınız. toofree alanı, artık gerekli olmayan tüm yedeklemelerinin silme göz önünde bulundurun.</li></ul> Merhaba sorunları gidermek, hello uyarı temizleyin ve hello işlemi yeniden deneyin. |
| Kopyalama <*aygıt adı*> işlemi tamamlanamadı. |İş hatası kopyalayın. |Bir kopya oluşturulamadı. Merhaba aşağıdakilerden birini göz önünde bulundurun:<ul><li>Yedekleme listenizin geçerli olmayabilir. Hala geçerli olduğu hello listesi tooverify yenileyin.</li><li>Bağlantı sorunları hello kopyalama işlemi başarıyla tamamlanmasını engelliyor. Bağlantı sorunu olmadığından emin olun.</li><li>Merhaba kullanılabilir depolama sınırına ulaştınız. toofree alanı, artık gerekli olmayan tüm yedeklemelerinin silme göz önünde bulundurun.</li></ul>Merhaba sorunları gidermek, hello uyarı temizleyin ve hello işlemi yeniden deneyin. |

### <a name="performance-alerts"></a>Performans uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Veri aktarımı beklenmeyen gecikme yaşıyor. |Yavaş veri aktarın. |Bir depolama birimi hizmeti hello ölçeklenebilirlik hedefleri aşan azaltma hataları oluşur. Merhaba depolama hizmeti yapar bu tooensure, tek bir istemci ya da Kiracı hello hizmeti diğer hello gider kullanabilir. Azure depolama hesabınızın sorunlarını giderme hakkında daha fazla bilgi için çok Git[izleme, tanılama ve Microsoft Azure Storage sorun giderme](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Yerel ayırma disk alanı azalıyor <*aygıt adı*>. |Yavaş yanıt süresi. |% 10'hello toplam için sağlanan boyutu <*aygıt adı*> ayrılmış hello üzerinde yetersiz alan ayrılmış artık yerel aygıt ve üzerinde hello olduğunuzda. Merhaba iş yüküne <*aygıt adı*> yüksek bir üretiyor karmaşası veya oranını yakın zamanda geçirilmiş büyük miktarda veri. Bu performansın düşmesine neden olabilir. Aşağıdakilerden birini göz önünde bulundurun Eylemler tooresolve bu hello:<ul><li>Merhaba bulut bant genişliği toothis cihaz artırın.</li><li>Azaltın veya iş yükleri tooanother birimi veya paylaşımı taşıyın.</li></ul> |

### <a name="security-alerts"></a>Güvenlik uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Parola <*aygıt adı*> içinde sona erecek <*numarası*> gün. |Parola uyarı. |Parolanızı içinde sona erecek < numarası < gün. Parolanızı değiştirmeyi düşünün. Daha fazla bilgi için çok Git[değişiklik hello StorSimple sanal dizinin cihaz Yöneticisi parolası](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Güncelleştirme uyarıları

| Uyarı metni | Olay | Daha fazla bilgi / önerilen eylemleri |
|:--- |:--- |:--- |
| Yeni güncelleştirmeler cihazınız için kullanılabilir. |Güncelleştirmeleri toohello StorSimple sanal dizinin kullanılabilir. |Merhaba yeni güncelleştirmeleri yükleyebilirsiniz **Bakım** sayfası. |
| Yeni güncelleştirmeleri taraması değil <*aygıt adı*>. |Hata güncelleştirin. |Yeni güncelleştirmeler yüklenirken bir hata oluştu. Merhaba güncelleştirmeleri el ile yükleyebilirsiniz. Merhaba sorun devam ederse, iletişim [Microsoft Support](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Sonraki adımlar

* [StorSimple sanal dizinin Hello hakkında bilgi edinin](storsimple-ova-overview.md).

