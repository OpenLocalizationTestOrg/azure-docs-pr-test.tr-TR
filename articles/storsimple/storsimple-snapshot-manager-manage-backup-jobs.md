---
title: "aaaStorSimple anlık görüntü Yöneticisi'ni yedekleme işleri | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini tooview hello ve zamanlanmış, çalışmakta ve tamamlanan yedekleme işlerini yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>StorSimple Snapshot Manager tooview kullanma ve yedekleme işlerini yönetme

## <a name="overview"></a>Genel Bakış
Merhaba **işleri** hello düğümünde **kapsam** bölmesinde gösterilir hello **zamanlanmış**, **son 24 saat**, ve **çalıştıran**yedekleme etkileşimli olarak veya yapılandırılmış bir ilke tarafından başlatılan görev. 

Bu öğretici hello nasıl kullanabileceğinizi açıklar **işleri** zamanlanmış, son ve şu anda çalışan yedekleme işleri hakkında düğümü toodisplay bilgi. (Merhaba listesi işler ve ilgili bilgiler görüntülenir hello **sonuçları** bölmesinde.) Ayrıca, listelenen işini sağ tıklatın ve kullanılabilir eylemler listeleyen bir bağlam menüsü bakın.

## <a name="view-scheduled-jobs"></a>Zamanlanan işleri görüntüleyin
Aşağıdaki yordam tooview zamanlanmış yedekleme işlerini hello kullanın.

#### <a name="tooview-scheduled-jobs"></a>Zamanlanmış tooview işleri
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın. 
2. Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **zamanlanmış**. Merhaba aşağıdaki bilgiler görüntülenir hello **sonuçları** bölmesi:
   
   * **Ad** – hello hello zamanlanmış anlık görüntü adı
   * **Sonraki çalıştırma** – hello tarih ve saat hello sonraki zamanlanmış anlık görüntüsünün
   * **Son çalıştırma** – hello tarih ve saat hello en son zamanlanmış anlık görüntü
     
     > [!NOTE]
     > Tek seferlik yalnızca anlık görüntüler için hello **sonraki çalıştırmaya** ve **son çalıştırma** aynı hello olacaktır.
     
     ![Zamanlanmış yedekleme işleri](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. belirli bir iş üzerinde tooperform ek eylemleri sağ hello hello iş adı **sonuçları** bölmesinde ve hello menü seçeneklerini seçin.

## <a name="view-recent-jobs"></a>Son işleri görüntüle
Aşağıdaki yordam tooview yedekleme hello kullanın ve hello son 24 saat tamamlandığını işleri geri yükleyin.

#### <a name="tooview-recent-jobs"></a>tooview en son işlerin
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **son 24 saat**. Merhaba **sonuçları** bölmesi hello yedekleme işlerini son 24 saat (64 işleri tooa maksimum) gösterir. Merhaba aşağıdaki bilgiler görüntülenir hello **sonuçları** bağlı olarak hello bölmesini **Görünüm** belirlediğiniz seçenekleri:
   
   * **Ad** – hello hello zamanlanmış anlık görüntü adı.
   * **Başlatılan** – hello tarih ve zaman hello anlık görüntü başladığı zaman.
   * **Durdurulmuş** – hello tarih ve zaman hello anlık görüntüsü tamamlandı veya sonlandırıldı zaman.
   * **Geçen** – hello hello arasındaki süre miktarı **başlatıldı** ve **durduruldu** kez.
   * **Durum** – hello yakın zamanda tamamlandı hello iş durumu. **Başarı** hello Yedekleme başarıyla oluşturulduğunu gösterir. **Başarısız** o hello işi başarıyla çalışmadı gösterir.
   * **Bilgi** – hello hello başarısızlık nedeni.
   * **Bayt (MB) işlenen** – hello miktarını (MB) işlenmiş hello birim grubu verileri. 
     
     ![Son 24 saat hello çalışan işler](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. belirli bir iş üzerinde tooperform ek eylemleri sağ hello hello iş adı **sonuçları** bölmesinde ve hello menü seçeneklerini seçin.
   
    ![Bir işi Sil](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Şu anda çalışan işleri görüntüleyin
Şu anda çalışan yordamı tooview işleri aşağıdaki hello kullanın.

#### <a name="tooview-currently-running-jobs"></a>şu anda çalışan işi tooview
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **çalıştıran**. Merhaba bağlı olarak **Görünüm** belirttiğiniz bilgisinden hello görünür hello seçenekleri **sonuçları** bölmesi:
   
   * **Ad** – hello hello zamanlanmış anlık görüntü adı.
   * **Başlatılan** – hello tarih ve zaman hello anlık görüntü başladığı zaman.
   * **Denetim noktası** – hello hello yedekleme geçerli eylem.
   * **Durum** – hello tamamlanma yüzdesi.
   * **Geçen** – hello hello yedekleme başlamasından bu yana geçen süre miktarı. 
   * **Ortalama verimi (MB)** – işlenen veri toothat (MB) işlenmesi için geçen toplam süre, toplam bayt oranı.
   * **Bayt (MB) işlenen** – toplam bayt (MB) işlenen veri.
   * **(MB) yazılan bayt** – toplam bayt (MB) yazılan veri. Merhaba veri yanı sıra hello meta verileri içerir ve bu nedenle hello bayt işlenen genellikle daha büyük.
     
     ![Şu anda çalışan işler](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. belirli bir iş üzerinde tooperform ek eylemleri sağ hello hello iş adı **sonuçları** bölmesinde ve hello menü seçeneklerini seçin.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).
* Nasıl çok öğrenin[StorSimple Snapshot Manager toomanage hello yedekleme Kataloğu'nu](storsimple-snapshot-manager-manage-backup-catalog.md).

