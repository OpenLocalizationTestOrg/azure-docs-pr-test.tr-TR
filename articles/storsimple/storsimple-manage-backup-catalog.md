---
title: "aaaManage, StorSimple yedekleme kataloğu | Microsoft Docs"
description: "Nasıl toouse hello StorSimple Yöneticisi hizmeti yedekleme kataloğu sayfa toolist, seçin ve bir birim için yedekleme kümelerini Sil açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Yedekleme kataloğu Hello StorSimple Yöneticisi hizmet toomanage kullanın
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya zamanlanmış yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.

Bu öğretici bir yedekleme toolist, seçin ve delete nasıl ayarlanacağını açıklar. toolearn nasıl toorestore yedekleme aygıtınızdan Git çok[Cihazınızı yedekleme kümesinden geri](storsimple-restore-from-backup-set.md). bir birim tooclone Git çok nasıl toolearn[bir StorSimple biriminin kopyalama](storsimple-clone-volume.md).

![Yedekleme kataloğu](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Merhaba **yedekleme kataloğu** sayfası, yedekleme kümesi seçiminiz sorgu toonarrow sağlar. Şu parametreler hello üzerinde temel alınır hello yedekleme kümelerini filtreleyebilirsiniz:

* **Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.
* **İlke veya birime yedekleme** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.
* **Başlangıç ve bitiş** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.

Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:

* **Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.
* **Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.
* **Oluşturma tarihi** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat. 
* **Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler. Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir. Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.
* **Başlatan** – hello yedeklemeleri başlatılabilir otomatik olarak bir zamanlamaya göre veya el ile bir kullanıcı tarafından. Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz. Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake el ile yedekleme.

## <a name="list-backup-sets-for-a-volume"></a>Liste yedekleme için bir birim ayarlar
Aşağıdaki adımları toolist hello bir birim için tüm hello yedeklemeler tamamlayın.

#### <a name="toolist-backup-sets"></a>toolist yedekleme kümeleri
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.
2. Filtre gibi Hello seçimleri:
   
   1. Merhaba uygun cihazı seçin.
   2. Merhaba aşağı açılan listesinde, bir birim tooview hello karşılık gelen hello yedeklemeleri seçin.
   3. Merhaba zaman aralığı belirtin.
   4. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute bu sorgu.
      
      Seçili hello birimle ilişkilendirilen hello yedeklemeler yedekleme kümelerini hello listesinde görünmesi gerekir.

## <a name="select-a-backup-set"></a>Bir yedekleme kümesi seçin
Bir birim veya yedekleme ilkesi için bir yedekleme kümesi adımları tooselect aşağıdaki hello tamamlayın.

#### <a name="tooselect-a-backup-set"></a>tooselect bir yedekleme kümesi
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.
2. Filtre gibi Hello seçimleri:
   
   1. Merhaba uygun cihazı seçin.
   2. Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.
   3. Merhaba zaman aralığı belirtin.
   4. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute bu sorgu.
      
      Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.
3. Seçin ve bir yedekleme kümesi'ni genişletin. Merhaba **geri** ve **silmek** seçenekler hello sayfasının hello altında görüntülenir. Seçtiğiniz hello yedekleme kümesinde aşağıdaki işlemlerden birini gerçekleştirebilirsiniz.

## <a name="delete-a-backup-set"></a>Bir yedekleme kümesi Sil
Kendisiyle ilişkili tooretain hello veriler artık istediklerinde yedekleme silin. Aşağıdaki adımları toodelete bir yedekleme kümesi hello gerçekleştirin.

#### <a name="toodelete-a-backup-set"></a>toodelete bir yedekleme kümesi
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu sekmesini**.
2. Filtre gibi Hello seçimleri:
   
   1. Merhaba uygun cihazı seçin.
   2. Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.
   3. Merhaba zaman aralığı belirtin.
   4. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute bu sorgu.
      
      Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.
3. Seçin ve bir yedekleme kümesi'ni genişletin. Merhaba **geri** ve **silmek** seçenekler hello sayfasının hello altında görüntülenir. **Sil**'e tıklayın.
4. Merhaba silme işlemi devam ederken ve başarıyla tamamlandığında size bildirilecek. Merhaba silme işlemi yapıldıktan sonra bu sayfada hello sorguyu yenileyin. Silinen hello yedekleme kümesi artık yedekleme kümelerini hello listesinde görünür.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[kullanın, bir yedekleme kümesi aygıtınızdan yedekleme kataloğu toorestore hello](storsimple-restore-from-backup-set.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

