---
title: "aaaDeactivate ve StorSimple 8000 serisi aygıtı silme | Microsoft Docs"
description: "Açıklar nasıl tooremove StorSimple cihazı hizmetinden önce devre dışı bırakma ve silme."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Devre dışı bırakın ve bir StorSimple cihazı Sil

## <a name="overview"></a>Genel Bakış

Bu makalede nasıl toodeactivate ve bağlı tooa StorSimple cihaz Yöneticisi hizmeti bir StorSimple cihaz silin. Bu makalede Hello yönerge hello StorSimple bulut cihazları dahil olmak üzere tooStorSimple 8000 serisi cihazlar geçerlidir. Bir StorSimple sanal dizisi kullanıyorsanız, çok Git[devre dışı bırakma ve silme StorSimple sanal dizinin](storsimple-virtual-array-deactivate-and-delete-device.md).

Devre dışı bırakma hello aygıt hello karşılık gelen StorSimple cihaz Yöneticisi hizmeti arasında hello bağlantı sunucularının. (Örneğin, değiştirme veya Cihazınızı yükseltmek veya StorSimple artık kullanıyorsanız) hizmet dışına StorSimple cihazını tootake isteyebilir. Silebilmek için önce bu durumda, toodeactivate hello aygıt gerekir.

Bir aygıtı devre dışı bıraktığınızda, hello cihazda yerel olarak depolanan tüm verileri artık erişilebilir değil. Yalnızca hello bulutta depolanan hello cihaz ile ilişkili hello verileri kurtarılabilir.

> [!WARNING]
> Devre dışı bırakma kalıcı bir işlemdir ve geri alınamaz. Toofactory varsayılana değilse devre dışı bırakılan bir cihaz StorSimple cihaz Yöneticisi hizmeti hello ile kaydedilemedi.
>
> Merhaba Fabrika işlem siler, cihazda yerel olarak depolanan tüm hello veri sıfırlayın. Bu nedenle, bir aygıtı devre dışı bırakmadan önce tüm verilerinizi bir bulut anlık görüntüsünü gerekir. Bu bulut anlık görüntüsü toorecover sağlayan tüm verileri daha sonraki bir aşamada hello.

Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Bir cihazı devre dışı bırakmak ve hello veri silin.
* Bir aygıtı devre dışı bırakın ve hello verileri korur.

> [!NOTE]
> Bir StorSimple fiziksel cihazı veya Bulut uygulaması devre dışı bırakmadan önce durdurmak veya istemciler ve bu cihazda bağımlı konakları silin.


## <a name="deactivate-and-delete-data"></a>Devre dışı bırakın ve verileri silme

Merhaba aygıt tamamen silme ilgilendiğiniz ve tooretain hello verilerinin hello aygıtta istiyor musunuz, hello aşağıdaki adımları tamamlayın.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello cihaz ve delete hello veri

1. Bir aygıtı devre dışı bırakmadan önce tüm hello birim kapsayıcıları (ve hello birimleri) hello aygıtla ilişkilendirilen silmeniz gerekir. Yalnızca ilişkili hello yedeklemeleri sildikten sonra birim kapsayıcıları silebilirsiniz.

    > [!NOTE]
    > Bir StorSimple fiziksel cihazı veya Bulut uygulaması devre dışı bırakmadan önce silinmiş hello birim kapsayıcısı hello verileri gerçekten hello aygıttan silindiğinden emin olun. Merhaba bulut tüketim grafikleri izleyebilirsiniz ve ardından hello bulut kullanımı nedeniyle sildiğiniz hello yedeklemeleri bırakma gördüğünüzde, toodeactivate hello aygıt geçebilirsiniz. Önce hello aygıt devre dışı bırakırsanız bu açılan oluşur, veri hello depolama hesabında stranded ve ücretler tahakkuk hello.

2. Merhaba cihaz aşağıdaki gibi devre dışı bırakın:
   
   1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**. Merhaba, **aygıtları** dikey penceresinde, toodeactivate, sağ tıklatın ve ardından istediğiniz select hello cihaz **etkinliğini**.

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Merhaba, **etkinliğini** dikey penceresinde hello aygıt adı tooconfirm yazın ve ardından **etkinliğini**. Merhaba işlemi başlar devre dışı bırakın ve birkaç dakika toocomplete alır.

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Devre dışı bırakma sonra hello aygıt tamamen silebilirsiniz. Bir cihazı silme hello aygıtları bağlı toohello hizmet listesinden kaldırır. Merhaba hizmeti artık silinen hello aygıt yönetebilirsiniz. Aşağıdaki adımları toodelete hello aygıt hello kullan:
   
   1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**. Merhaba, **aygıtları** dikey penceresinde, toodelete, sağ tıklatın ve ardından istediğiniz etkinliği seçin hello cihaz **silmek**.

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Merhaba, **silmek** dikey penceresinde hello aygıt adı tooconfirm yazın ve ardından **silmek**. Merhaba silme işlemi birkaç dakika toocomplete alır.

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Merhaba silme işlemi başarıyla tamamlandıktan sonra size bildirilir. Merhaba aygıt listesini tooreflect hello silme de güncelleştirir.

## <a name="deactivate-and-retain-data"></a>Devre dışı bırakın ve verileri tut

Merhaba cihaz silme ilginizi çekiyor mu ancak tooretain hello veri istiyorsanız hello aşağıdaki adımları tamamlayın:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>bir aygıt toodeactivate ve hello verileri tut
1. Merhaba aygıt devre dışı bırakın. Tüm birim kapsayıcıları hello ve hello aygıt hello anlık görüntüleri korunur.
   
   1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**. Merhaba, **aygıtları** dikey penceresinde, toodeactivate, sağ tıklatın ve ardından istediğiniz select hello cihaz **etkinliğini**.

         ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Merhaba, **etkinliğini** dikey penceresinde hello aygıt adı tooconfirm yazın ve ardından **etkinliğini**. Merhaba işlemi başlar devre dışı bırakın ve birkaç dakika toocomplete alır.

         ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Şimdi hello birim kapsayıcıları ve ilişkili hello anlık görüntüleri başarısız olabilir. Yordamlar için çok Git[StorSimple cihazınız için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).
3. Devre dışı bırakma ve yük devretme hello aygıt tamamen silebilirsiniz. Bir cihazı silme hello aygıtları bağlı toohello hizmet listesinden kaldırır. Merhaba hizmeti artık silinen hello aygıt yönetebilirsiniz. toodelete hello aygıt, aşağıdaki adımları tam hello:
   
   1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**. Merhaba, **aygıtları** dikey penceresinde, toodelete, sağ tıklatın ve ardından istediğiniz etkinliği seçin hello cihaz **silmek**.

       ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Merhaba, **silmek** dikey penceresinde hello aygıt adı tooconfirm yazın ve ardından **silmek**. Merhaba silme işlemi birkaç dakika toocomplete alır.

       ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Merhaba silme işlemi başarıyla tamamlandıktan sonra size bildirilir. Merhaba aygıt listesini tooreflect hello silme de güncelleştirir.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Devre dışı bırakın ve bir bulut uygulaması Sil

Bir StorSimple bulut uygulaması için devre dışı bırakma hello portalından kaldırır ve hello sanal makine ve hazırlandığında oluşturulan hello kaynakları siler. Merhaba bulut uygulaması devre dışı bırakıldıktan sonra olamaz tooits önceki durumuna geri.

![StorSimple bulut uygulaması devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Aşağıdaki eylemler hello sonuçlarında devre dışı bırakma:

* Merhaba StorSimple bulut uygulaması hello hizmetinden kaldırılır.
* Merhaba StorSimple bulut uygulaması için Hello sanal makine silinir.
* Merhaba işletim sistemi diski ve StorSimple bulut uygulaması hello için oluşturulan veri diskleri kaldırılır.
* Merhaba barındırılan hizmet ve sağlama işlemi sırasında oluşturulan sanal ağ korunur. Bu varlıklar kullanmıyorsanız, bunları el ile silmeniz gerekir.
* Merhaba StorSimple bulut uygulaması tarafından oluşturulan bulut anlık görüntüleri korunur.

Merhaba bulut uygulaması devre dışı bırakıldıktan sonra cihazların Merhaba listesinden silebilirsiniz. Select hello aygıt, sağ tıklatın ve ardından devre dışı **silmek**. Merhaba cihaz silinir ve aygıtları güncelleştirmelerinin listesini hello sonra StorSimple size bildirir.

## <a name="next-steps"></a>Sonraki adımlar

* toorestore Merhaba devre dışı bırakılan cihaz toofactory Varsayılanları, çok Git[hello aygıt toofactory varsayılan ayarlara](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Teknik destek için [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).
* toolearn toouse hello StorSimple cihaz Yöneticisi hizmeti, Git çok nasıl hakkında daha fazla bilgi[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

