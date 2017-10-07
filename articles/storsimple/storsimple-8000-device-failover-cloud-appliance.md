---
title: "aaaStorSimple yük devretme, olağanüstü durum kurtarma tooa StorSimple bulut uygulaması | Microsoft Docs"
description: "Nasıl toofail, StorSimple 8000 serisi fiziksel aygıt tooa üzerinden bulut Gereci öğrenin."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>StorSimple bulut uygulaması tooyour başarısız

## <a name="overview"></a>Genel Bakış

Bir olağanüstü durum varsa Bu öğretici bir StorSimple 8000 serisi fiziksel aygıt tooa StorSimple bulut uygulaması hello adımları gerekli toofail açıklar. StorSimple hello datacenter tooa bulut uygulaması Azure'da çalışan bir kaynak fiziksel cihazdaki hello aygıt yük devretme özelliği toomigrate verileri kullanır. Bu öğreticide Hello yönerge tooStorSimple 8000 serisi fiziksel cihazlar ve yazılım sürümlerini güncelleştirme 3 ve sonraki sürümleri çalıştıran bulut uygulamaları geçerlidir.

cihaz yük devretme ve bir olağanüstü durum gelen kullanılan toorecover nedir hakkında daha fazla toolearn Git çok[StorSimple 8000 serisi cihazlar için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).

StorSimple fiziksel cihazı tooanother fiziksel bir aygıtı, üzerinden toofail Git çok[tooa StorSimple fiziksel cihazı başarısız](storsimple-8000-device-failover-physical-device.md). bir aygıt tooitself üzerinden toofail Git çok[toohello aynı başarısız StorSimple fiziksel cihazı](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Ön koşullar

- Cihaz yük devretme için hello konuları gözden geçirdiğinizden emin olun. Daha fazla bilgi için çok Git[aygıt yük devretme için ortak konuları](storsimple-8000-device-failover-disaster-recovery.md).

- Bir StorSimple bulut oluşturulur ve bu yordamı çalıştırmadan önce yapılandırılmış Gereci olması gerekir. DR Merhaba, çalışan 3 yazılım sürümü güncelleştirme ya da daha sonra bir 8020 bulut uygulaması için kullanmayı düşünün. Merhaba 8020 modeli 64 TB vardır ve Premium depolama kullanır. Daha fazla bilgi için çok Git[dağıtma ve StorSimple bulut uygulaması yönetmek](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Adımları toofail tooa bulut uygulaması üzerinden

Aşağıdaki adımları toorestore hello aygıt tooa hedef StorSimple bulut uygulaması hello gerçekleştirin.

1.  Bu hello birim kapsayıcısı üzerinde toofail istediğiniz bulut anlık görüntüleri ilişkili doğrulayın. Daha fazla bilgi için çok Git[Aygıt Yöneticisi'ni StorSimple hizmeti toocreate yedeklemeleri](storsimple-8000-manage-backup-policies-u2.md).
2. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**. Merhaba, **aygıtları** dikey penceresinde, hizmetiniz ile bağlı cihazlar gidin toohello listesi.
    ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Seçin ve kaynak Cihazınızı tıklayın. Merhaba kaynak aygıt üzerinden toofail istediğiniz hello birim kapsayıcıları sahiptir. Çok Git**ayarlar > birim kapsayıcıları**.

    ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Tooanother aygıt üzerinden toofail istediğiniz bir birim kapsayıcısı seçin. Merhaba birim kapsayıcı toodisplay hello birimlerin listesini bu kapsayıcıdaki'ı tıklatın. Bir birim, sağ tıklatın ve tıklatın seçin **Çevrimdışına Al** tootake hello çevrimdışı birim.

    ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Merhaba birim kapsayıcısındaki tüm hello birimleri için bu işlemi yineleyin.

     ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Önceki adımı yineleyin hello tüm birim kapsayıcıları hello için tooanother aygıt üzerinden toofail istersiniz.

7. Toohello dönün **aygıtları** dikey. Merhaba Komut çubuğundaki **yük devri**.

    ![Üzerinden başarısız'ı tıklatın](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. Merhaba, **yük devri** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:
   
    1. Tıklatın **kaynak**. Üzerinden Hello birim kapsayıcıları toofail seçin. **Yalnızca ilişkili bulut anlık görüntüleri ile birim kapsayıcıları hello ve çevrimdışı birimler görüntülenir.**
        ![Kaynak seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Tıklatın **hedef**. Bir hedef bulut uygulaması hello açılır listeden kullanılabilir aygıtları seçin. **Yeterli kapasitesi tooaccommodate kaynak birim kapsayıcıları yalnızca hello cihazları hello listesinde görüntülenir.**

        ![Hedef seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Merhaba yük devretme ayarları altında gözden **Özet** ve hello onay kutusu seçili birim kapsayıcıları hello birimlerinde çevrimdışı belirten seçin. 

        ![Yük devretme ayarlarını gözden geçirin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Bir yük devretme iş oluşturulur. toomonitor hello yük devretme iş, hello iş bildirime tıklayın.

    ![İzleyici yük devretme işine](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Toohello Hello yük devretme tamamlandıktan sonra geri dönün **aygıtları** dikey.

    1. Merhaba hedef olarak hello yük devretme için kullanılan hello cihazı seçin.

       ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Tıklatın **birim kapsayıcıları**. Merhaba birimleri hello eski aygıttan yanı sıra tüm hello birim kapsayıcıları listelenmelidir.

       Üzerinden başarısız hello birim kapsayıcısı yerel olarak sabitlenmiş birimleri, bu birimlerin katmanlı birimler olarak yük devredildi. Yerel olarak sabitlenmiş birimlerin bir StorSimple bulut uygulaması üzerinde desteklenmez.

       ![Görünüm hedef birim kapsayıcıları](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Sonraki adımlar

* Bir yük devretme gerçekleştirdikten sonra çok gerekebilir[StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).

* Hizmet nasıl toouse hello StorSimple cihaz Yöneticisi hakkında daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

