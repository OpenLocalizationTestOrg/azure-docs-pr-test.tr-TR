---
title: "aaaMicrosoft Azure StorSimple sanal dizinin yedekleme Öğreticisi | Microsoft Docs"
description: "StorSimple sanal dizinin yukarı tooback nasıl paylaşımları ve birimler açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Paylaşımlar veya birimler, StorSimple sanal dizisinde yedekle

## <a name="overview"></a>Genel Bakış

Merhaba StorSimple sanal dizinin bir dosya sunucusu veya bir iSCSI sunucusu yapılandırılmış bir karma bulut depolama şirket içi sanal cihazdır. Merhaba sanal dizinin hello kullanıcı toocreate hello cihazda zamanlanmış ve el ile yedeklerini tüm hello paylaşımları veya birimler izin verir. Dosya sunucusu olarak yapılandırıldığında, öğe düzeyinde kurtarma de sağlar. Bu öğretici nasıl toocreate zamanlanmış ve el ile yedekleme açıklar ve öğe düzeyinde kurtarma toorestore sanal dizisindeki silinmiş bir dosyayı gerçekleştirin.

Bu öğretici toohello StorSimple sanal diziler yalnızca geçerlidir. 8000 serisi hakkında daha fazla bilgi için çok gidin[8000 serisi aygıtı için bir yedekleme oluşturmak](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Paylaşımları ve birimler yedekleme

Yedeklemeleri zaman noktası korumasını sağlar, kurtarılabilirliği iyileştirmeye ve paylaşımları ve birimler için geri yükleme sürelerini en aza. StorSimple Cihazınızda iki yolla paylaşımı veya birimi yedekleyebilirsiniz: **zamanlanmış** veya **el ile**. Merhaba yöntemlerin her biri aşağıdaki bölümlerde hello ele alınmıştır.

## <a name="change-hello-backup-start-time"></a>Merhaba yedekleme başlangıç saatini değiştir

> [!NOTE]
> Bu sürümde, zamanlanmış yedeklemeler, her gün belirtilen zamanda çalışan ve tüm hello paylaşımlar veya birimler hello aygıtta yedekler varsayılan bir ilke tarafından oluşturulur. Şu olası toocreate özel ilkeler zamanlanmış yedeklemeler için şu anda değil.


StorSimple sanal dizinizi (22:30) günün belirli bir zamanda başlatır ve tüm hello paylaşımlar veya birimler hello aygıtta günde bir kez yedekler varsayılan yedekleme ilkesine sahip. Hangi hello yedekleme başlatır, ancak hello sıklığı ve hello (hangi yedeklemeleri tooretain hello sayısını belirtir) bekletme değiştirilemez hello zaman değiştirebilirsiniz. Bu yedeklemeler sırasında tüm sanal aygıt hello desteklenir. Bu olası hello aygıt hello performansını etkileyebilir ve hello cihazda dağıtılan hello iş yükleri etkiler. Bu nedenle, bu yedeklemeler için yoğun olmayan saatler zamanlamanızı öneririz.

 toochange hello varsayılan yedekleme başlangıç zamanı, başlangıç adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>toochange hello için başlangıç saatini hello varsayılan yedekleme İlkesi

1. Çok Git**aygıtları**. StorSimple cihaz Yöneticisi hizmetiniz ile kayıtlı cihazların Merhaba listesi görüntülenir. 
   
    ![toodevices gidin](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Seçin ve aygıtınızı tıklatın. Merhaba **ayarları** dikey penceresinde görüntülenir. Çok Git**Yönet > Yedekleme ilkeleri**.
   
    ![Cihazınızı seçin](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. Merhaba, **yedekleme ilkeleri** dikey penceresinde hello varsayılan başlangıç zamanı, 22:30. Aygıt saat diliminde hello yeni başlangıç saati hello günlük zamanlama için belirtebilirsiniz.
   
    ![toobackup ilkeleri gidin](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. **Kaydet** düğmesine tıklayın.

### <a name="take-a-manual-backup"></a>El ile yedekleyin

Ayrıca tooscheduled yedeklemeler, herhangi bir zamanda el ile (isteğe bağlı) yedekleme aygıtı veri alabilir.

#### <a name="toocreate-a-manual-backup"></a>toocreate el ile yedekleme

1. Çok Git**aygıtları**. Cihazınızı seçin ve sağ **...**  en sağdaki hello hello Seçili satırda. Merhaba bağlam menüsünden seçin **yedek alın**.
   
    ![tootake yedekleme gidin](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. Merhaba, **yedek alın** dikey penceresinde tıklatın **yedek alın**. Bu işlem hello dosya sunucusundaki tüm hello paylaşımları veya iSCSI sunucunuzdaki tüm hello birimleri yedekleyin. 
   
    ![Başlangıç yedekleme](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Bir talep üzerine yedekleme başlatılır ve bir yedekleme işi başlatıldığını görebilirsiniz.
   
    ![Başlangıç yedekleme](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Merhaba iş başarıyla tamamlandıktan sonra yeniden bildirilir. Merhaba Yedekleme işleminin ardından başlatır.
   
    ![Yedekleme işi oluşturuldu](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. tootrack hello ilerlemesini hello iş ayrıntılarına bakın ve hello yedeklemeler hello bildirim'ı tıklatın. Bu, çok sürer **iş ayrıntıları**.
   
     ![yedekleme işi ayrıntıları](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Merhaba Yedekleme tamamlandıktan sonra çok Git**Yönetim > Yedekleme kataloğu**. Cihazınızda bir bulut anlık görüntüsü tüm hello paylaşımları (veya birimleri) görürsünüz.
   
    ![Tamamlanan yedekleme](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Var olan yedekleri görüntüleyin
tooview hello var olan yedekleri, hello Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin.

#### <a name="tooview-existing-backups"></a>tooview var olan yedekleri

1. Çok Git**aygıtları** dikey. Seçin ve aygıtınızı tıklatın. Merhaba, **ayarları** dikey penceresinde çok Git**Yönetim > Yedekleme kataloğu**.
   
    ![Toobackup katalog gidin](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Filtreleme için kullanılan ölçüt toobe aşağıdaki hello belirtin:
   
    - **Zaman aralığı** – olabilir **son 1 saat**, **son 24 saat**, **son 7 gün**, **son 30 gündeki**, **geçen yıl** , ve **özel tarih**.
    
    - **Aygıtları** – dosya sunucularında veya iSCSI sunucuları, StorSimple cihaz Yöneticisi hizmetine kayıtlı hello listeden seçin.
   
    - **Başlatılan** – otomatik olarak **zamanlanmış** (göre bir yedekleme İlkesi) veya **el ile** (sizin tarafınızdan) başlatıldı.
   
    ![Filtre yedekleri](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. **Uygula**'ya tıklayın. Merhaba filtrelenmiş listesi yedeklemeleri hello görüntülenir **yedekleme kataloğu** dikey. Not yalnızca 100 yedekleme öğeleri belirli bir zamanda görüntülenebilir.
   
    ![Güncelleştirilmiş yedekleme kataloğu](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).

