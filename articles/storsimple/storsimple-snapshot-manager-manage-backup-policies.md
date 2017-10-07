---
title: "aaaStorSimple anlık görüntü Yöneticisi'ni yedekleme ilkeleri | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini toocreate hello ve zamanlanmış yedeklemeler denetleyen hello yedekleme ilkelerini yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>StorSimple Snapshot Manager toocreate kullanın ve yedekleme ilkelerini yönetme
## <a name="overview"></a>Genel Bakış
Bir yedekleme İlkesi birim verilerini yerel olarak veya hello bulut yedekleme için bir zamanlama oluşturur. Bir yedekleme ilkesi oluşturduğunuzda, bir bekletme ilkesi de belirtebilirsiniz. (En fazla 64 anlık görüntüleri tutabilirsiniz.) Yedekleme ilkeleri hakkında daha fazla bilgi için bkz: [yedekleme türleri](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) içinde [StorSimple 8000 serisi: karma bulut çözümünün](storsimple-overview.md).

Bu öğretici açıklar nasıl yapılır:

* Bir yedekleme İlkesi Oluştur
* Yedekleme ilkesini Düzenle
* Bir yedekleme ilkesi silme

## <a name="create-a-backup-policy"></a>Bir yedekleme İlkesi Oluştur
Aşağıdaki yordam toocreate yeni bir yedekleme İlkesi hello kullanın.

#### <a name="toocreate-a-backup-policy"></a>toocreate bir yedekleme İlkesi
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde, sağ **yedekleme ilkeleri**, tıklatıp **yedekleme İlkesi Oluştur**.

    ![Bir yedekleme İlkesi Oluştur](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Merhaba **bir ilke oluşturmak** iletişim kutusu görüntülenir.

    ![Bir ilke - Genel sekmesi oluştur](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Merhaba üzerinde **genel** sekmesi, aşağıdaki bilgilerle tam hello:

   1. Merhaba, **adı** metin kutusuna hello ilkesi için bir ad yazın.
   2. Merhaba, **birim grubu** metin kutusunda, tür hello hello ilkeyle ilişkilendirilmiş hello birim grubu adını.
   3. Şunlardan birini seçin **yerel anlık görüntü** veya **bulut anlık görüntü**.
   4. Anlık görüntü tooretain Hello sayısını seçin. Seçerseniz **tüm**, 64 anlık görüntüleri tutulur (Merhaba en fazla).
4. Merhaba tıklatın **zamanlama** sekmesi.

    ![Bir ilke - zamanlama sekmesi oluştur](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Merhaba üzerinde **zamanlama** sekmesi, aşağıdaki bilgilerle tam hello:

   1. Merhaba tıklatın **etkinleştirmek** onay kutusunu tooschedule hello sonraki yedekleme.
   2. Altında **ayarları**seçin **bir kez**, **günlük**, **haftalık**, veya **aylık**.
   3. Merhaba, **Başlat** metin kutusuna hello takvim simgesini tıklatın ve bir başlangıç tarihi seçin.
   4. Altında **Gelişmiş ayarları**, isteğe bağlı yineleme zamanlamaları ve bitiş tarihi ayarlayabilirsiniz.
   5. **Tamam** düğmesine tıklayın.

Bir yedekleme ilkesi oluşturduktan sonra aşağıdaki bilgilerle hello hello görünür **sonuçları** bölmesi:

* **Ad** – hello yedekleme ilkesi adı.
* **Tür** – yerel anlık görüntü veya Bulut anlık görüntüsü.
* **Birim grubu** – hello hello ilkeyle ilişkilendirilmiş birim grubu.
* **Bekletme** – hello anlık görüntü sayısı tutulur; hello en fazla 64.
* **Oluşturulan** – Bu ilke oluşturulduysa başlangıç tarihi.
* **Etkin** – hello İlkesi şu anda etkin olup olmadığını: **True** yürürlükte; olduğunu gösterir **False** etkin olmadığını gösterir.

## <a name="edit-a-backup-policy"></a>Yedekleme ilkesini Düzenle
Aşağıdaki yordam tooedit mevcut bir yedekleme İlkesi hello kullanın.

#### <a name="tooedit-a-backup-policy"></a>tooedit bir yedekleme İlkesi
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello tıklatın **yedekleme ilkeleri** düğümü. Tüm hello yedekleme ilkeleri hello görünür **sonuçları** bölmesi.
3. Tooedit istediğiniz ve ardından hello ilkesine sağ **Düzenle**.

    ![Yedekleme ilkesini Düzenle](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Ne zaman hello **bir ilke oluşturmak** penceresi görüntülenir, değişikliklerinizi girin ve ardından **Tamam**.

## <a name="delete-a-backup-policy"></a>Bir yedekleme ilkesi silme
Aşağıdaki yordam toodelete bir yedekleme İlkesi hello kullanın.

#### <a name="toodelete-a-backup-policy"></a>toodelete bir yedekleme İlkesi
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello tıklatın **yedekleme ilkeleri** düğümü. Tüm hello yedekleme ilkeleri hello görünür **sonuçları** bölmesi.
3. Toodelete istediğiniz ve ardından yedekleme ilkesini hello sağ **silmek**.
4. Merhaba onaylama iletisi göründüğünde tıklayın **Evet**.

    ![Yedek İlkesi onayını Sil](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooview kullanma ve yedekleme işlerini yönetme](storsimple-snapshot-manager-manage-backup-jobs.md).
