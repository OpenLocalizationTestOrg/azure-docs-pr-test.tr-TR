---
title: "aaaStorSimple yük devretme, 8000 serisi cihazlar için olağanüstü durum kurtarma | Microsoft Docs"
description: "Bilgi nasıl toofail StorSimple cihaz toohello üzerinden aynı aygıt."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>StorSimple fiziksel cihazı toosame Cihazınızı başarısız

## <a name="overview"></a>Genel Bakış

Bir olağanüstü durum varsa Bu öğretici bir StorSimple 8000 serisi fiziksel aygıt tooitself hello adımları gerekli toofail açıklar. StorSimple hello aygıt yük devretme özelliği toomigrate veri kaynağı fiziksel CİHAZDAN hello datacenter tooanother fiziksel cihazın kullanır. Bu öğreticide Hello yönerge tooStorSimple 8000 serisi fiziksel cihazlar yazılım sürümleri güncelleştirme 3 ve sonraki sürümleri çalıştıran geçerlidir.

cihaz yük devretme ve bir olağanüstü durum gelen kullanılan toorecover nedir hakkında daha fazla toolearn Git çok[StorSimple 8000 serisi cihazlar için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).

bir fiziksel aygıt tooanother fiziksel aygıt üzerinden toofail Git çok[toohello aynı başarısız StorSimple fiziksel cihazı](storsimple-8000-device-failover-physical-device.md). bir StorSimple fiziksel cihazı tooa StorSimple bulut uygulaması üzerinden toofail Git çok[tooa StorSimple bulut uygulaması başarısız](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Ön koşullar

- Cihaz yük devretme için hello konuları gözden geçirdiğinizden emin olun. Daha fazla bilgi için çok Git[aygıt yük devretme için ortak konuları](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Adımları toofail toohello üzerinden aynı aygıt

Merhaba toohello toofail gerekiyorsa aşağıdaki adımları gerçekleştirin aynı aygıt.

1. Tüm hello birimleri bulut anlık görüntülerini kullanarak Cihazınızı alın. Daha fazla bilgi için çok Git[Aygıt Yöneticisi'ni StorSimple hizmeti toocreate yedeklemeleri](storsimple-8000-manage-backup-policies-u2.md).
2. Cihaz toofactory Varsayılanları sıfırlayın. İzleyin hello ayrıntılı yönergeleri [nasıl tooreset StorSimple cihaz toofactory varsayılan ayarları](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Toohello StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**. Merhaba, **aygıtları** dikey penceresinde hello eski aygıt Göster olarak **çevrimdışı**.

    ![Kaynak aygıt çevrimdışı](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Cihazınızı yapılandırmak ve StorSimple cihaz Yöneticisi hizmetiniz ile yeniden kaydedin. Merhaba yeni kayıtlı cihaz olarak göstermelidir **yukarı tooset hazır**. Merhaba aygıt hello yeni cihaz için hello eski aygıt ile sayısal tooindicate hello aygıt ancak eklenmiş. aynı sıfırlama toofactory varsayılan oldu ve yeniden kayıtlı hello adıdır.

    ![Yeni kaydedilen cihaz hazır tooset ayarlama](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Merhaba yeni cihaz hello cihaz kurulumunu tamamlayın. Daha fazla bilgi için çok Git[4. adım: minimum cihaz kurulumunu Tamamla](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). Merhaba üzerinde **aygıtları** dikey penceresinde hello aygıt hello durumunu değiştirir çok**çevrimiçi**.

   > [!IMPORTANT]
   > **Merhaba en düşük yapılandırmayı ilk tamamlamak ya da, DR başarısız olabilir.**

    ![Yeni kaydedilen cihaz çevrimiçi](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Merhaba eski aygıt (çevrimdışı durumu) seçin ve hello Komut çubuğundaki **yük devri**. Merhaba, **yük devri** dikey penceresinde hello kaynağı olarak eski aygıt seçin ve hello yeni cihaz kayıtlı gibi hello hedef aygıt belirtin.

    ![Yük devretme özeti](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Ayrıntılı yönergeler için çok başvuran[tooanother fiziksel aygıt üzerinden başarısız](#fail-over-to-another-physical-device).

7. Bir aygıt geri yükleme iş hello izleyebilirsiniz oluşturulur **işleri** dikey.

8. Merhaba iş başarıyla tamamlandıktan sonra erişim hello yeni cihaz ve toohello gidin **birim kapsayıcıları** dikey. Merhaba eski aygıttan tüm hello birim kapsayıcıları toohello yeni cihaz geçirildiğini doğrulayın.

   ![Birim kapsayıcıları geçişi](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Merhaba yük devretme işlemi tamamlandıktan sonra devre dışı bırakıp hello portalından hello eski aygıt silme. Merhaba eski aygıt (çevrimdışı), sağ seçin ve ardından **etkinliğini**. Merhaba aygıt devre dışı bırakıldıktan sonra hello cihazın hello durumu güncelleştirilir.

     ![Kaynak aygıt devre dışı](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Select hello aygıt, sağ tıklatın ve ardından devre dışı **silmek**. Bu hello aygıt cihazların Merhaba listeden siler.

    ![Kaynak aygıt silindi](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Sonraki adımlar

* Bir yük devretme gerçekleştirdikten sonra çok gerekebilir[StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).
* Hizmet nasıl toouse hello StorSimple cihaz Yöneticisi hakkında daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

