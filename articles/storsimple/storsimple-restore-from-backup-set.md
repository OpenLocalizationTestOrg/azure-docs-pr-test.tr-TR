---
title: aaaRestore yedekten bir StorSimple biriminin | Microsoft Docs
description: "Nasıl toouse hello StorSimple Yöneticisi hizmeti yedekleme kataloğu sayfa toorestore bir StorSimple biriminin bir yedekleme kümesinden açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Bir yedeklemek kümesinden StorSimple birimini geri
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Genel Bakış
Merhaba **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.

 ![Yedekleme kataloğu sayfası](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

Bu öğretici açıklar nasıl toouse hello **yedekleme kataloğu** sayfa toorestore bir yedekleme kümesi aygıtınızdan üzerindeki bir birimi.

## <a name="how-toouse-hello-backup-catalog"></a>Nasıl toouse hello yedekleme kataloğu
Merhaba **yedekleme kataloğu** sayfası, yedekleme kümesi seçiminiz toonarrow yardımcı olan bir sorgu sağlar. Şu parametreler hello üzerinde temel alınan hello yedekleme kümelerini filtreleyebilirsiniz:

* **Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.
* **Yedekleme İlkesi** veya **birim** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.
* **Gelen** ve **için** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.

Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:

* **Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.
* **Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.
* **Oluşturulan** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat. 
* **Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler. Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir. Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.
* **Tarafından başlatılan** – hello yedeklemeleri otomatik olarak tooa zamanlamaya göre başlatılabilir veya bir kullanıcı tarafından el ile. (Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz. Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake etkileşimli bir yedek.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Nasıl toorestore, StorSimple birim bir yedekten
Merhaba kullanabilirsiniz **yedekleme kataloğu** toorestore StorSimple biriminiz belirli bir yedekten sayfa. 

> [!WARNING]
> Bir yedekten geri yükleme hello var olan birimler hello yedekten yerini alır. Bu hello hello yedeğin alındığı sonra yazıldı herhangi bir veri kaybına neden olabilir.
> 
> 

Bir birime geri başlatmadan önce hello birimin çevrimdışı olduğundan emin olun. Tootake hello birimde çevrimdışı hello konak önce gerekir ve cihaz hello. Merhaba adımları [bir birim çevrimdışına](storsimple-manage-volumes.md#take-a-volume-offline). Bir yedekleme kümesinden adımları toorestore bir birim aşağıdaki hello gerçekleştirin.

### <a name="toorestore-from-a-backup-set"></a>bir yedekleme kümesinden toorestore
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.
   
    ![Yedekleme kataloğu](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Bir yedekleme kümesi aşağıdaki gibi seçin:
   
   1. Merhaba uygun cihazı seçin.
   2. Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.
   3. Merhaba zaman aralığı belirtin.
   4. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute bu sorgu.
      
      Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.
3. Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin. Geri yüklemeden önce bu birimleri hello ana bilgisayar ve aygıt çevrimdışına alınması gerekir. Merhaba adımları [bir birim çevrimdışına](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Merhaba aygıtta çevrimdışı hello birimleri olabilmesi hello birimlerde çevrimdışı hello konak ilk olarak, gerçekleştirdiğinizden emin olun. Merhaba konakta çevrimdışı hello birimleri almazsanız, büyük olasılıkla toodata bozulmasına yol açabilir.
   > 
   > 
4. Bir yedekleme kümesi seçin. Tıklatın **geri** hello sayfanın hello sonundaki.
5. Onayınız istenir. 
   
    ![Onay sayfası](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Merhaba geri yükleme bilgileri gözden geçirin ve hello onay simgesine ![onay simgesi](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Bu hello erişerek görüntüleyebileceğiniz bir geri yükleme işi başlatır **işleri** sayfası. 
7. Merhaba geri yükleme tamamlandıktan sonra birimlerinizi Merhaba içeriğine hello yedekleme birimlerden değiştirilir olduğunu doğrulayabilirsiniz.

![Video var](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video var**

toowatch nasıl hello kopya kullanın ve geri yükleme StorSimple silinmiş toorecover dosyalarında özellikleri gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[yönetmek StorSimple birimlerini](storsimple-manage-volumes.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

