---
title: "aaaStorSimple yük devretme, olağanüstü durum kurtarma tooa StorSimple 8000 serisi fiziksel aygıt | Microsoft Docs"
description: "Bilgi nasıl toofail, StorSimple 8000 serisi fiziksel aygıt tooanother fiziksel aygıt üzerinden."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Tooa StorSimple 8000 serisi fiziksel aygıt üzerinden başarısız

## <a name="overview"></a>Genel Bakış

Bir olağanüstü durum varsa Bu öğretici bir StorSimple 8000 serisi fiziksel aygıt tooanother StorSimple fiziksel cihazı hello adımları gerekli toofail açıklar. StorSimple hello aygıt yük devretme özelliği toomigrate veri kaynağı fiziksel CİHAZDAN hello datacenter tooanother fiziksel cihazın kullanır. Bu öğreticide Hello yönerge tooStorSimple 8000 serisi fiziksel cihazlar yazılım sürümleri güncelleştirme 3 ve sonraki sürümleri çalıştıran geçerlidir.

cihaz yük devretme ve bir olağanüstü durum gelen kullanılan toorecover nedir hakkında daha fazla toolearn Git çok[StorSimple 8000 serisi cihazlar için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).

bir StorSimple fiziksel cihazı tooa StorSimple bulut uygulaması üzerinden toofail Git çok[tooa StorSimple bulut uygulaması başarısız](storsimple-8000-device-failover-cloud-appliance.md). bir fiziksel aygıt tooitself üzerinden toofail Git çok[toohello aynı başarısız StorSimple fiziksel cihazı](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Ön koşullar

- Cihaz yük devretme için hello konuları gözden geçirdiğinizden emin olun. Daha fazla bilgi için çok Git[aygıt yük devretme için ortak konuları](storsimple-8000-device-failover-disaster-recovery.md).

- Merhaba veri merkezinde dağıtılan bir StorSimple 8000 serisi fiziksel bir aygıtı olması gerekir. Hello aygıt güncelleştirme 3 veya sonraki yazılım sürümü çalıştırması gerekir. Daha fazla bilgi için çok Git[şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Adımları toofail tooa fiziksel aygıt üzerinden

Aşağıdaki adımları toorestore hello aygıt tooa hedef fiziksel cihazınız gerçekleştirin.

1. Bu hello birim kapsayıcısı üzerinde toofail istediğiniz bulut anlık görüntüleri ilişkili doğrulayın. Daha fazla bilgi için çok Git[Aygıt Yöneticisi'ni StorSimple hizmeti toocreate yedeklemeleri](storsimple-8000-manage-backup-policies-u2.md).
2. Tooyour StorSimple Aygıt Yöneticisi'ni gidin ve ardından **aygıtları**. Merhaba, **aygıtları** dikey penceresinde, hizmetiniz ile bağlı cihazlar gidin toohello listesi.
    ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Seçin ve kaynak Cihazınızı tıklayın. Merhaba kaynak aygıt üzerinden toofail istediğiniz hello birim kapsayıcıları sahiptir. Çok Git**ayarlar > birim kapsayıcıları**.
4. Tooanother aygıt üzerinden toofail istediğiniz bir birim kapsayıcısı seçin. Merhaba birim kapsayıcı toodisplay hello birimlerin listesini bu kapsayıcıdaki'ı tıklatın. Bir birim, sağ tıklatın ve tıklatın seçin **Çevrimdışına Al** tootake hello çevrimdışı birim. Merhaba birim kapsayıcısındaki tüm hello birimleri için bu işlemi yineleyin.
5. Önceki adımı yineleyin hello tüm birim kapsayıcıları hello için tooanother aygıt üzerinden toofail istersiniz.
6. Toohello dönün **aygıtları** dikey. Merhaba Komut çubuğundaki **yük devri**.
    ![Üzerinden başarısız'ı tıklatın](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. Merhaba, **yük devri** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:
   
   1. Tıklatın **kaynak**. Bulut anlık görüntüleri ile ilişkili birimi ile Merhaba birim kapsayıcıları görüntülenir. Yalnızca görüntülenen Merhaba kapsayıcılara yük devretme için uygundur. Birim kapsayıcıları Hello listesinde toofail üzerinden istediğiniz hello birim kapsayıcıları seçin. **Yalnızca ilişkili bulut anlık görüntüleri ile birim kapsayıcıları hello ve çevrimdışı birimler görüntülenir.**

       ![Kaynak seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Tıklatın **hedef**. Merhaba önceki adımda seçtiğiniz hello birim kapsayıcıları için bir hedef cihaz hello aşağı açılan listesinden kullanılabilir aygıtları seçin. Yeterli kapasitesi tooaccommodate kaynak birim kapsayıcıları yalnızca hello cihazları hello listesinde görüntülenir.

        ![Hedef seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Son olarak, tüm hello yük devretme ayarlarda gözden **Özet**. Hello ayarlarını gözden geçirdikten sonra seçilen birim kapsayıcıları hello birimlerinde çevrimdışı hello onay kutusunu gösteren seçin. **Tamam** düğmesine tıklayın.

       ![Yük devretme ayarlarını gözden geçirin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple bir yük devretme işi oluşturur. Merhaba iş bildirim toomonitor hello yük devretme işini hello aracılığıyla tıklatın **işleri** dikey.

    Üzerinden başarısız hello birim kapsayıcısı yerel birim varsa, tek tek geri yükleme işleri hello kapsayıcıdaki her yerel birimi (değil için katmanlı birimleri) konusuna bakın. Bu geri yükleme işleri oldukça bazı zaman toocomplete sürebilir. Bu hello yük devretme işine önceki tamamlanabilir olasıdır. Yalnızca hello geri yükleme işi tamamlandıktan sonra bu birimler yerel GARANTİLERİN sahip olur.

    ![İzleyici yük devretme işine](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Merhaba yük devretme tamamlandıktan sonra toohello Git **aygıtları** dikey.
   
   1. Merhaba yük devretme işlemi için hello hedef cihaz olarak kullanılan hello cihazı seçin.

       ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Toohello Git **birim kapsayıcıları** dikey. Merhaba birimleri hello eski aygıttan yanı sıra tüm hello birim kapsayıcıları listelenmelidir.

       ![Görünüm hedef birim kapsayıcıları](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Sonraki adımlar

* Bir yük devretme gerçekleştirdikten sonra çok gerekebilir[StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).
* Hizmet nasıl toouse hello StorSimple cihaz Yöneticisi hakkında daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

