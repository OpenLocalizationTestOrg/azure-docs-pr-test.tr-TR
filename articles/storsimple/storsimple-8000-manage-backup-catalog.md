---
title: "aaaManage, StorSimple yedekleme kataloğu | Microsoft Docs"
description: "Nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti yedekleme kataloğu sayfa toolist seçin ve yedekleme kümelerini Sil açıklanmaktadır."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Yedekleme kataloğu Hello StorSimple cihaz Yöneticisi hizmeti toomanage kullanın
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple cihaz Yöneticisi hizmeti **yedekleme kataloğu** dikey penceresinde el ile veya zamanlanmış yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.

Bu öğretici bir yedekleme toolist, seçin ve delete nasıl ayarlanacağını açıklar. toolearn nasıl toorestore yedekleme aygıtınızdan Git çok[Cihazınızı yedekleme kümesinden geri](storsimple-8000-restore-from-backup-set-u2.md). bir birim tooclone Git çok nasıl toolearn[bir StorSimple biriminin kopyalama](storsimple-8000-clone-volume-u2.md).

![Yedekleme kataloğu](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Merhaba **yedekleme kataloğu** dikey yedekleme kümesi seçiminiz sorgu toonarrow sağlar. Şu parametreler hello üzerinde temel alınır hello yedekleme kümelerini filtreleyebilirsiniz:

* **Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.
* **Yedekleme İlkesi veya birim** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.
* **Başlangıç ve bitiş** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.

Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:

* **Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.
* **Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.
* **Oluşturma tarihi** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat. 
* **Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler. Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir. Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.
* **Başlatan** – hello yedeklemeleri başlatılabilir otomatik olarak bir zamanlamaya göre veya el ile bir kullanıcı tarafından. Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz. Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake el ile yedekleme.

## <a name="list-backup-sets-for-a-backup-policy"></a>Liste yedekleme için bir yedekleme İlkesi ayarlar
Aşağıdaki adımları toolist hello tüm hello yedeklemeler için bir yedekleme İlkesi tamamlayın.

#### <a name="toolist-backup-sets"></a>toolist yedekleme kümeleri
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **yedekleme kataloğu**.

2. Filtre gibi Hello seçimleri:
   
   1. Merhaba zaman aralığı belirtin.
   2. Merhaba uygun cihazı seçin.
   3. Filtre ölçütü **yedekleme İlkesi** tooview hello karşılık gelen hello yedekler.
   3. Merhaba yedekleme İlkesi açılır listeden seçin **tüm** tüm hello seçili hello yedeklemelerin tooview aygıt.
   4. Tıklatın **Uygula** tooexecute bu sorgu.
      
      Seçili hello yedekleme ilkesiyle ilişkili hello yedeklemeler yedekleme kümelerini hello listesinde görünmesi gerekir.

      ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Bir yedekleme kümesi seçin
Bir birim veya yedekleme ilkesi için bir yedekleme kümesi adımları tooselect aşağıdaki hello tamamlayın.

#### <a name="tooselect-a-backup-set"></a>tooselect bir yedekleme kümesi
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **yedekleme kataloğu**.
2. Filtre gibi Hello seçimleri:
   
   1. Merhaba zaman aralığı belirtin. 
   2. Merhaba uygun cihazı seçin. 
   3. Birim veya yedekleme İlkesi tooselect istediğiniz hello yedekleme için filtre.
   4. Tıklatın **Uygula** tooexecute bu sorgu.
      
      Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.

      ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Seçin ve bir yedekleme kümesi'ni genişletin. Şimdi hello yedekleme kümelerini içerdiği hello birimlerle ayrıntılarıyla görebilirsiniz. Merhaba **geri** ve **silmek** hello yedekleme kümesi hello bağlam menüsünü (sağ tıklatma) aracılığıyla seçenekleri mevcuttur. Seçtiğiniz hello yedekleme kümesinde aşağıdaki işlemlerden birini gerçekleştirebilirsiniz.

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Bir yedekleme kümesi Sil
Kendisiyle ilişkili tooretain hello veriler artık istediklerinde yedekleme silin. Aşağıdaki adımları toodelete bir yedekleme kümesi hello gerçekleştirin.

#### <a name="toodelete-a-backup-set"></a>toodelete bir yedekleme kümesi
 Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **yedekleme kataloğu**.
2. Filtre gibi Hello seçimleri:
   
   1. Merhaba zaman aralığı belirtin. 
   2. Merhaba uygun cihazı seçin. 
   3. Birim veya yedekleme İlkesi tooselect istediğiniz hello yedekleme için filtre.
   4. Tıklatın **Uygula** tooexecute bu sorgu.
      
      Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.

      ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Seçin ve bir yedekleme kümesi'ni genişletin. Şimdi hello yedekleme kümelerini içerdiği hello birimlerle ayrıntılarıyla görebilirsiniz. Merhaba **geri** ve **silmek** hello yedekleme kümesi hello bağlam menüsünü (sağ tıklatma) aracılığıyla seçenekleri mevcuttur. Seçili hello yedekleme kümesi sağ tıklayın ve hello bağlam menüsünden seçin **silmek**.

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Onayınız istendiğinde hello görüntülenen bilgileri gözden geçirin ve tıklayın **silmek**. Merhaba seçili yedekleme kalıcı olarak silinir.

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Merhaba silme işlemi devam ederken ve başarıyla tamamlandığında size bildirilecek. Merhaba silme işlemi yapıldıktan sonra bu sayfada hello sorguyu yenileyin. Silinen hello yedekleme kümesi artık yedekleme kümelerini hello listesinde görünür.

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[kullanın, bir yedekleme kümesi aygıtınızdan yedekleme kataloğu toorestore hello](storsimple-8000-restore-from-backup-set-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

