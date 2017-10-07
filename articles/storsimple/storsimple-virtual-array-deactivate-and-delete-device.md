---
title: aaaDeactivate ve Microsoft Azure StorSimple sanal dizinin silme | Microsoft Docs
description: "Açıklar nasıl tooremove StorSimple cihazı hizmetinden önce devre dışı bırakma ve silme."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Devre dışı bırakın ve bir StorSimple sanal dizi Sil

## <a name="overview"></a>Genel Bakış

StorSimple sanal dizinin devre dışı bıraktığınızda, hello cihaz ve hello karşılık gelen StorSimple cihaz Yöneticisi hizmeti arasındaki hello bağlantıyı kesmek. Bu öğretici açıklar nasıl yapılır:

* Bir cihazı devre dışı 
* Devre dışı bırakılmış bir aygıtı silme

Bu makalede Hello bilgiler tooStorSimple sanal diziler yalnızca geçerlidir. 8000 serisi hakkında daha fazla bilgi için toohow çok gidin[bir cihazı silmek veya devre dışı bırakma](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Zaman toodeactivate?

Devre dışı bırakma kalıcı bir işlemdir ve geri alınamaz. Merhaba StorSimple cihaz Yöneticisi hizmeti ile yeniden devre dışı bırakılmış bir aygıt kaydedilemiyor. Toodeactivate ihtiyacınız ve senaryoları aşağıdaki hello StorSimple sanal dizisinde silin:

* **Planlanan yük devretme** : Cihazınızı çevrimiçi olduğundan ve Cihazınızı toofail planlayın. Tooupgrade tooa büyük cihaz planlıyorsanız, Cihazınızı toofail gerekebilir. Merhaba veri sahipliği aktarılır ve hello yük devretme işlemi tamamlandıktan sonra hello kaynak cihaz otomatik olarak silinir.
* **Planlanmamış yük devretme** : Cihazınızı çevrimdışıysa ve hello aygıt üzerinden toofail gerekir. Bu senaryo, aşağı birincil Cihazınızı hello veri merkezinde bir kesinti olduğunda ve bir olağanüstü durum sırasında ortaya çıkabilir. Merhaba aygıt tooa ikincil aygıt üzerinden toofail planlayın. Merhaba veri sahipliği aktarılır ve hello yük devretme işlemi tamamlandıktan sonra hello kaynak cihaz otomatik olarak silinir.
* **Yetkisini** : toodecommission hello aygıt istiyor. Bu toofirst gerektirir hello aygıt devre dışı bırakın ve ardından silin. Bir aygıtı devre dışı bıraktığınızda, yerel olarak depolanan tüm verileri artık erişemez. Merhaba bulutta depolanan erişim ve kurtarma hello veriler yalnızca kullanabilirsiniz. Tookeep hello aygıt verilerini sonra devre dışı bırakmayı planlıyorsanız, bir cihazın devre dışı bırakmadan önce tüm verilerinizin bulut anlık görüntüsü almanız gerekir. Bu bulut anlık görüntüsü toorecover sağlayan tüm verileri daha sonraki bir aşamada hello.

## <a name="deactivate-a-device"></a>Bir cihazı devre dışı

toodeactivate Cihazınızı hello aşağıdaki adımları gerçekleştirin.

#### <a name="toodeactivate-hello-device"></a>toodeactivate hello cihaz

1. Hizmetiniz, çok Git**Yönetim > aygıtları**. Merhaba, **aygıtları** dikey penceresinde, tıklatın ve select hello aygıt toodeactivate istiyor.
   
    ![Aygıt toodeactivate seçin](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. İçinde **cihaz Pano** dikey penceresinde tıklatın **... Daha fazla** ve hello listesinden **etkinliğini**.
   
    ![Tıklatın devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. Merhaba, **etkinliğini** dikey penceresinde, tür hello aygıt adı ve ardından **etkinliğini**. 
   
    ![Onayla devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Merhaba işlemi başlar devre dışı bırakın ve birkaç dakika toocomplete alır.
   
    ![Devam eden devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Devre dışı bırakma sonra cihazların Merhaba listesini yeniler.
   
    ![Tam devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Bu cihaz artık silebilirsiniz.

## <a name="delete-hello-device"></a>Merhaba aygıtı silme

Bir aygıtın toobe ilk devre dışı bırakılan toodelete onu. Bir cihazı silme hello aygıtları bağlı toohello hizmet listesinden kaldırır. Merhaba hizmeti artık silinen hello aygıt yönetebilirsiniz. Merhaba veri Hello cihaz ile ilişkili ancak hello bulutta kalır. Bu veriler, ardından ücretler tahakkuk.

toodelete hello aygıt hello aşağıdaki adımları gerçekleştirin.

#### <a name="toodelete-hello-device"></a>toodelete hello cihaz

1. StorSimple Aygıt Yöneticisi'nde çok Git**Yönetim > aygıtları**. Merhaba, **aygıtları** dikey penceresinde toodelete istediğiniz devre dışı bırakılan bir cihaz seçin.
2. Merhaba, **cihaz Pano** dikey penceresinde tıklatın **... Daha fazla** ve ardından **silmek**.
   
   ![Aygıt toodelete seçin](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. Merhaba, **silmek** dikey penceresinde, tür hello adını aygıt tooconfirm hello silme ve ardından **silmek**. Silme hello aygıt hello aygıtla ilişkilendirilen hello bulut verilerini silmez. 
   
   ![Silmeyi onayla](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. Merhaba silme işlemi başlatır ve birkaç dakika toocomplete alır.
   
   ![Silme sürüyor](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Merhaba cihaz silindikten sonra cihazların Merhaba güncelleştirilmiş listesini görüntüleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* Hakkında bilgi için üzerinde toofail Git çok[yük devretme ve olağanüstü durum kurtarma, StorSimple sanal dizinin](storsimple-virtual-array-failover-dr.md).

* toolearn toouse hello StorSimple cihaz Yöneticisi hizmeti, Git çok nasıl hakkında daha fazla bilgi[kullanın, StorSimple sanal dizinizi StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-virtual-array-manager-service-administration.md). 

