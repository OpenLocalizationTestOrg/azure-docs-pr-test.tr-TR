---
title: aaaManage StorSimple yedekleme ilkelerinizi | Microsoft Docs
description: "Merhaba StorSimple Yöneticisi hizmet toocreate kullanın ve el ile yedekleme, yedekleme zamanlamaları ve yedekleme bekletme yönetmek nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a>Merhaba StorSimple Yöneticisi hizmeti toomanage yedekleme ilkeleri (güncelleştirme 2) kullanın
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse hello StorSimple Yöneticisi hizmeti açıklanmaktadır **yedekleme ilkeleri** sayfa toocontrol yedekleme işlemleri ve yedekleme bekletme StorSimple birimlerinizi için. Ayrıca açıklanır nasıl toocomplete el ile yedekleme.

Bir birim yedeklediğinizde, yerel bir anlık görüntüsü veya bir bulut anlık görüntüsü toocreate seçebilirsiniz. Yerel olarak sabitlenmiş bir birim yedekleme yapıyorsanız, bir bulut anlık görüntüsü belirtilmesi önerilir. Çok sayıda karmaşası çok sahip bir veri kümesi ile birlikte yerel olarak sabitlenmiş bir birim yerel anlık görüntüleri alma hızla yerel alana çalıştırabilir durumda neden olur. Yerel anlık görüntüleri tootake seçerseniz, daha az günlük anlık görüntüleri tooback hello en son durumunu almak için günde bir korumak ve bunları silin öneririz.

Yerel olarak sabitlenmiş bir birim bir bulut anlık görüntüsünü, burada, yinelenenleri kaldırılmış sıkıştırılmış ve yalnızca değiştirilen hello veri toohello bulut kopyalayın. 

## <a name="hello-backup-policies-page"></a>Merhaba yedekleme ilkeleri sayfası
Merhaba **yedekleme ilkeleri** sayfası sağlar toomanage yedekleme ilkeleri ve zamanlama yerel ve bulut anlık görüntüleri. (Yedekleme kullanılan tooconfigure yedekleme zamanlamaları ve yedekleme bekletme birimlerin bir koleksiyon için ilkelerdir.) Yedekleme ilkeleri tootake birden çok birim görüntüsünü aynı anda etkinleştirin. Bu, bir yedekleme İlkesi tarafından oluşturulan hello yedekler kilitlenme tutarlı kopyaları olacağı anlamına gelir. Merhaba **yedekleme ilkeleri** sayfası hello yedekleme ilkeleri, kendi türleri, ilişkili hello birimleri, korunur yedeklemeleri hello sayısını listeler ve bu ilkeler hello seçeneği tooenable.

Merhaba **yedekleme ilkeleri** sayfası aynı zamanda toofilter hello varolan yedekleme ilkeleri tarafından bir veya daha fazla alanları izleyen Merhaba, sağlar:

* **İlke adı** – hello hello ilkesiyle ilişkili ad. Merhaba farklı ilkeleri türleri şunlardır:
  
  * Zamanlanmış ilkeleri hello kullanıcı tarafından açıkça oluşturulur.
  * Bu birimi seçeneği için Hello varsayılan yedekleme hello birim oluşturma sırasında etkinleştirildiğinde oluşturulan otomatik ilkeleri. Bu ilkeler olarak adlandırılır *VolumeName*_Default nerede *VolumeName* hello hello Klasik Azure portalı hello kullanıcı tarafından yapılandırılan StorSimple biriminin toohello adını gösterir. 22:30 aygıt zamanında başlayan günlük bulut anlık görüntüleri Hello otomatik ilkeleri sonuçlanır.
  * Başlangıçta hello StorSimple Snapshot Manager oluşturulan ilkeleri içe. Bu hello ilkeleri alındığı hello StorSimple Snapshot Manager konak açıklayan bir etiket vardır.
* **Birimleri** – hello hello ilkesiyle ilişkili birimler. Yedekleme oluşturulduğunda bir yedekleme ilkesiyle ilişkili tüm hello birimler birlikte gruplandırılır.
* **Son başarılı yedekleme** – başlangıç tarihi ve Bu ilkeyle alınan hello son başarılı yedekleme.
* **Sonraki yedekleme** – başlangıç tarihi ve bu ilke tarafından başlatılan hello sonraki zamanlanmış yedekleme.
* **Zamanlamalar** – hello hello yedekleme ilkeyle ilişkilendirilmiş zamanlamaları sayısı.

Bu sayfadan gerçekleştirebileceğiniz sık kullanılan hello işlemleri şunlardır:

* Yedekleme ilkesi ekleme 
* Ekleyin veya bir zamanlama değiştirin 
* Bir yedekleme ilkesi silme 
* El ile yedekleyin 
* Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma 

## <a name="add-a-backup-policy"></a>Yedekleme ilkesi ekleme
Bir yedekleme İlkesi tooautomatically zamanlama Yedeklemelerinizin ekleyin. Hello Azure Klasik portalı tooadd StorSimple cihazınız için bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin. Hello İlkesi ekledikten sonra bir zamanlama tanımlayabilirsiniz (bkz [Ekle ya da bir zamanlamayı değiştirmek](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

![Video var](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video var**

toowatch nasıl toocreate yerel veya Bulut yedekleme İlkesi, gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Ekleyin veya bir zamanlama değiştirin
Ekleyin veya ekli tooan varolan yedekleme İlkesi, StorSimple Cihazınızda bir zamanlama değiştirin. Bir zamanlamayı değiştirmek veya hello hello Azure Klasik portalı tooadd adımlarını izleyerek gerçekleştirebilirsiniz.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a>Bir yedekleme ilkesi silme
StorSimple Cihazınızda hello Azure Klasik portalı toodelete bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>El ile yedekleyin
Tek bir birim için hello Azure Klasik portalı toocreate isteğe bağlı (el ile) yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma
Hello Azure Klasik portalı toocreate birden çok birimleri ve zamanlamaları sahip özel bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

