---
title: aaaManage StorSimple 8000 serisi yedekleme ilkeleri | Microsoft Docs
description: "Merhaba StorSimple cihaz Yöneticisi hizmeti toocreate kullanın ve el ile yedekleme, yedekleme zamanlamaları ve yedekleme bekletme StorSimple 8000 serisi aygıtta yönetmek nasıl açıklanmaktadır."
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
ms.workload: TBD
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Azure portal toomanage yedekleme ilkelerini Hello StorSimple cihaz Yöneticisi hizmetini kullanma


## <a name="overview"></a>Genel Bakış

Bu öğretici nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti açıklanmaktadır **yedekleme İlkesi** dikey toocontrol yedekleme işlemleri ve yedekleme bekletme StorSimple birimlerinizi için. Ayrıca açıklanır nasıl toocomplete el ile yedekleme.

Bir birim yedeklediğinizde, yerel bir anlık görüntüsü veya bir bulut anlık görüntüsü toocreate seçebilirsiniz. Yerel olarak sabitlenmiş bir birim yedekleme yapıyorsanız, bir bulut anlık görüntüsü belirtilmesi önerilir. Çok sayıda karmaşası çok sahip bir veri kümesi ile birlikte yerel olarak sabitlenmiş bir birim yerel anlık görüntüleri alma hızla yerel alana çalıştırabilir durumda neden olur. Yerel anlık görüntüleri tootake seçerseniz, daha az günlük anlık görüntüleri tooback hello en son durumunu almak için günde bir korumak ve bunları silin öneririz.

Yerel olarak sabitlenmiş bir birim bir bulut anlık görüntüsünü, burada, yinelenenleri kaldırılmış sıkıştırılmış ve yalnızca değiştirilen hello veri toohello bulut kopyalayın.

## <a name="hello-backup-policy-blade"></a>Merhaba yedekleme İlkesi dikey penceresi

Merhaba **yedekleme İlkesi** StorSimple cihazınız için dikey verir toomanage yedekleme ilkeleri ve zamanlama yerel ve bulut anlık görüntüleri. Yedekleme ilkeleri kullanılan tooconfigure yedekleme zamanlamaları ve yedekleme bekletme birimlerin bir koleksiyon için ' dir. Yedekleme ilkeleri tootake birden çok birim görüntüsünü aynı anda etkinleştirin. Bu, bir yedekleme İlkesi tarafından oluşturulan hello yedekler kilitlenme tutarlı kopyaları olacağı anlamına gelir.

Merhaba yedekleme ilkeleri sekmeli liste Ayrıca, toofilter hello varolan yedekleme ilkeleri tarafından bir veya daha fazla alanları izleyen hello sağlar:

* **İlke adı** – hello hello ilkesiyle ilişkili ad. Merhaba farklı ilkeleri türleri şunlardır:

  * Zamanlanmış ilkeleri hello kullanıcı tarafından açıkça oluşturulur.
  * Başlangıçta hello StorSimple Snapshot Manager oluşturulan ilkeleri içe. Bu hello ilkeleri alındığı hello StorSimple Snapshot Manager konak açıklayan bir etiket vardır.

  > [!NOTE]
  > Otomatik veya varsayılan yedekleme ilkeleri artık hello birim oluşturma sırasında etkinleştirilir.

* **Son başarılı yedekleme** – başlangıç tarihi ve Bu ilkeyle alınan hello son başarılı yedekleme.

* **Sonraki yedekleme** – başlangıç tarihi ve bu ilke tarafından başlatılan hello sonraki zamanlanmış yedekleme.

* **Birimleri** – hello hello ilkesiyle ilişkili birimler. Yedekleme oluşturulduğunda bir yedekleme ilkesiyle ilişkili tüm hello birimler birlikte gruplandırılır.

* **Zamanlamalar** – hello hello yedekleme ilkeyle ilişkilendirilmiş zamanlamaları sayısı.

Yedekleme ilkelerine gerçekleştirebileceğiniz sık kullanılan hello işlemleri şunlardır:

* Yedekleme ilkesi ekleme
* Ekleyin veya bir zamanlama değiştirin
* Bir birim Ekle Kaldır
* Bir yedekleme ilkesi silme
* El ile yedekleyin

## <a name="add-a-backup-policy"></a>Yedekleme ilkesi ekleme

Bir yedekleme İlkesi tooautomatically zamanlama Yedeklemelerinizin ekleyin. Bir birim ilk oluşturduğunuzda, biriminiz ile ilişkili varsayılan yedekleme ilkesi bulunmamaktadır. Bir yedekleme İlkesi tooprotect birim verilerini atayın ve tooadd gerekir.

Hello Azure portal tooadd StorSimple cihazınız için bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin. Hello İlkesi ekledikten sonra bir zamanlama tanımlayabilirsiniz (bkz [Ekle ya da bir zamanlamayı değiştirmek](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Ekleyin veya bir zamanlama değiştirin

Ekleyin veya ekli tooan varolan yedekleme İlkesi, StorSimple Cihazınızda bir zamanlama değiştirin. Bir zamanlamayı değiştirmek veya hello hello Azure portal tooadd adımlarını izleyerek gerçekleştirebilirsiniz.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Bir birim Ekle Kaldır

Ekleyebilir veya tooa yedekleme İlkesi, StorSimple Cihazınızda atanmış bir birim kaldırabilirsiniz. Bir birimi kaldırmak veya hello hello Azure portal tooadd adımlarını izleyerek gerçekleştirebilirsiniz.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Bir yedekleme ilkesi silme

StorSimple Cihazınızda hello Azure portal toodelete bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>El ile yedekleyin

Tek bir birim için hello Azure portal toocreate isteğe bağlı (el ile) yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).

