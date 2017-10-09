---
title: "aaaDeactivate ve StorSimple cihazı silmek | Microsoft Docs"
description: "Açıklar nasıl tooremove StorSimple cihazı hizmetinden önce devre dışı bırakma ve silme."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Devre dışı bırakın ve StorSimple Yöneticisi hizmeti üzerinden bir StorSimple 8000 serisi aygıtı silme
## <a name="overview"></a>Genel Bakış
(Örneğin, değiştirme veya Cihazınızı yükseltmek veya StorSimple artık kullanıyorsanız) hizmet dışına StorSimple cihazını tootake isteyebilir. Merhaba Durum buysa, silebilmek için önce toodeactivate hello aygıt gerekir. Devre dışı bırakma hello bağlantı hello karşılık gelen StorSimple Yöneticisi hizmeti ile Merhaba aygıt arasında sunucularının. Bu öğretici açıklar nasıl tooremove önce devre dışı bırakma ve silme hizmetinden StorSimple cihazı. 

Bir aygıtı devre dışı bıraktığınızda, hello cihazda yerel olarak depolanan tüm verileri artık erişilebilir olacaktır. Yalnızca hello bulutta depolanan hello cihaz ile ilişkili hello verileri kurtarılabilir.  

> [!WARNING]
> Devre dışı bırakma kalıcı bir işlemdir ve geri alınamaz. İlk toohello varsayılan fabrika ayarlarına sıfırlama olmadıkça hello StorSimple Yöneticisi hizmetiyle devre dışı bırakılan bir cihaz kaydedilemez. 
> 
> Merhaba Fabrika işlem siler, cihazda yerel olarak depolanan tüm hello veri sıfırlayın. Bu nedenle, bir cihazın devre dışı bırakmadan önce tüm verilerinizi bir bulut anlık görüntüsünü gereklidir. Bu, toorecover sağlayacak tüm verileri daha sonraki bir aşamada hello.
> 
> 

Bu öğretici açıklar nasıl yapılır:

* Bir aygıtı devre dışı bırakın ve hello verilerini sil
* Bir aygıtı devre dışı bırakın ve hello verileri tut

Ayrıca açıklar nasıl devre dışı bırakma ve silme StorSimple sanal cihazlar üzerinde çalışır.

> [!NOTE]
> StorSimple fiziksel veya sanal aygıt devre dışı bırakmadan önce toostop emin olun veya istemciler ve bu cihazda bağımlı konakları silin.
> 
> 

## <a name="deactivate-and-delete-data"></a>Devre dışı bırakın ve verileri silme
Merhaba aygıt tamamen silme ilgilendiğiniz ve tooretain hello verilerinin hello aygıtta istiyor musunuz, hello aşağıdaki adımları tamamlayın.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello cihaz ve delete hello veri
1. Önceki toodeactivating bir aygıt, tüm hello birim kapsayıcıları (ve hello birimleri) hello aygıtla ilişkilendirilen silmeniz gerekir. Yalnızca ilişkili hello yedeklemeleri sildikten sonra birim kapsayıcıları silebilirsiniz.
2. Merhaba cihaz aşağıdaki gibi devre dışı bırakın:
   
   1. Merhaba StorSimple Yöneticisi hizmeti üzerinde **aygıtları** sayfası, select hello aygıt toodeactivate istiyor ve, hello hello sayfanın en altında tıklatın **etkinliğini**.
   2. Bir onay iletisi görüntülenir. Tıklatın **Evet** toocontinue. Merhaba devre dışı bırakma işlemi başlatılır ve birkaç dakika toocomplete alın.
3. Devre dışı bırakma sonra hello aygıt tamamen silebilirsiniz. Bir cihazı silme hello aygıtları bağlı toohello hizmet listesinden kaldırır. Merhaba hizmeti artık silinen hello aygıt yönetebilirsiniz. Aşağıdaki adımları toodelete hello aygıt hello kullan:
   
   1. Merhaba StorSimple Yöneticisi hizmeti üzerinde **aygıtları** sayfasında, toodelete istediğiniz devre dışı bırakılan bir cihaz seçin.
   2. Merhaba sayfasında Hello altta tıklatın **silmek**.
   3. Onayınız istenir. Tıklatın **Evet** toocontinue.
      
      Silinen hello aygıt toobe birkaç dakika sürebilir.

## <a name="deactivate-and-retain-data"></a>Devre dışı bırakın ve verileri tut
Merhaba cihaz silme ilginizi çekiyor mu ancak tooretain hello veri istiyorsanız hello aşağıdaki adımları tamamlayın.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>bir aygıt toodeactivate ve hello verileri tut
1. Merhaba aygıt devre dışı bırakın. Tüm birim kapsayıcıları hello ve hello aygıt hello anlık görüntüleri kalır.
   
   1. Merhaba StorSimple Yöneticisi hizmeti üzerinde **aygıtları** sayfası, select hello aygıt toodeactivate istiyor ve, hello hello sayfanın en altında tıklatın **etkinliğini**.
   2. Bir onay iletisi görüntülenir. Tıklatın **Evet** toocontinue. Merhaba devre dışı bırakma işlemi başlatılır ve birkaç dakika toocomplete alın.
2. Şimdi hello birim kapsayıcıları ve ilişkili hello anlık görüntüleri başarısız olabilir. Yordamlar için çok Git[StorSimple cihazınız için yük devretme ve olağanüstü durum kurtarma](storsimple-device-failover-disaster-recovery.md).
3. Devre dışı bırakma ve yük devretme hello aygıt tamamen silebilirsiniz. Bir cihazı silme hello aygıtları bağlı toohello hizmet listesinden kaldırır. Merhaba hizmeti artık silinen hello aygıt yönetebilirsiniz. Aşağıdaki adımları toodelete hello aygıt hello tamamlayın:
   
   1. Merhaba StorSimple Yöneticisi hizmeti üzerinde **aygıtları** sayfasında, toodelete istediğiniz devre dışı bırakılan bir cihaz seçin.
   2. Merhaba sayfasında Hello altta tıklatın **silmek**.
   3. Onayınız istenir. Tıklatın **Evet** toocontinue.
      
      Silinen hello aygıt toobe birkaç dakika sürebilir.

## <a name="deactivate-and-delete-a-virtual-device"></a>Devre dışı bırakın ve sanal cihazı Sil
StorSimple sanal cihaz için devre dışı bırakma hello sanal makine kaldırır. Merhaba sanal makine ve hazırlandığında oluşturulan hello kaynakları sonra silebilirsiniz. Merhaba sanal cihazı devre dışı bırakıldıktan sonra olamaz tooits önceki durumuna geri. 

Aşağıdaki eylemler hello sonuçlarında devre dışı bırakma:

* Merhaba StorSimple sanal cihaz kaldırılır.
* Merhaba OSDisk ve hello StorSimple sanal cihaz için oluşturulan veri diskleri kaldırılır.
* Merhaba barındırılan hizmeti ve sağlama işlemi sırasında oluşturulan sanal ağ korunur. Bu varlıklar kullanmıyorsanız, bunları el ile silmeniz gerekir.
* Merhaba StorSimple sanal cihaz tarafından oluşturulan bulut anlık görüntüleri korunur.

## <a name="next-steps"></a>Sonraki adımlar
* toorestore Merhaba devre dışı bırakılan cihaz toofactory Varsayılanları, çok Git[hello aygıt toofactory varsayılan ayarlara](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Teknik destek için [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).
* toolearn toouse hello StorSimple Yöneticisi hizmeti, Git çok nasıl hakkında daha fazla bilgi[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md). 

