---
title: "aaaView ve StorSimple 8000 serisi işleri yönetme | Microsoft Docs"
description: "Merhaba StorSimple cihaz Yöneticisi hizmeti işler dikey penceresinde açıklar ve nasıl toouse, tootrack son, geçerli ve zamanlanmış yedekleme işleri."
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti tooview kullanma ve işleri (güncelleştirme 3 ve üzeri) yönetme

## <a name="overview"></a>Genel Bakış
Merhaba **işleri** dikey penceresini görüntülemek için tek bir merkezi portal sağlar ve cihazlarda başlatılmış işlerini yönetme bağlı tooyour StorSimple cihaz Yöneticisi hizmeti. Birden çok aygıt zamanlanmış, çalışan, tamamlandı, iptal edilmiş ve başarısız işleri görüntüleyebilirsiniz. Sonuçları bir tablo biçiminde sunulur.

![İşlerini dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

Hızlı bir şekilde hello işleri, içinde alanları gibi filtreleyerek ilginizi çekiyor mu bulabilirsiniz:

* **Durum** – işleri, başarılı, sürüyor, iptal edilmiş, başarısız, iptal etme veya ile başarılı oldu, hata olabilir.
* **Zaman aralığı** – işleri filtrelenmiş göre hello tarih ve saat aralığı olabilir. Merhaba 1 saat, son 30 gün, önceki yıl veya özel tarihi geçmiş 7 gün 24 saat geçmiş geçmiş aralıktır.
* **Tür** – zamanlanmış yedekleme, el ile yedekleme, geri yükleme yedekleme hello iş türü olabilir kopyalama birimi, birim kapsayıcıları başarısız, yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, güncelleştirmeleri yüklemek, destek günlükleri toplamak ve bulut uygulaması oluşturma.
* **Aygıtları** – işleri belirli bağlı cihaz tooyour'nda bir hizmeti başlatıldı.
  
Merhaba filtrelenen işler sonra öznitelikleri aşağıdaki hello hello temelinde tabloda verilmiştir:
  
* **Ad** – zamanlanmış yedekleme, yedekleme, geri yükleme yedekleme, kopya birim, başarısız birim kapsayıcıları el ile yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, güncelleştirmeleri yüklemek, destek günlükleri toplamak veya Bulut uygulaması oluşturun.
* **Durum** – çalışan, tamamlandı, iptal edilmiş, başarısız, iptal etme veya hatalarla tamamlandı.
* **Varlık** – hello işleri bir birim, bir yedekleme İlkesi veya bir aygıt ile ilişkili olabilir. Örneğin, zamanlanmış bir yedekleme işi bir yedekleme ilkesiyle ilişkili iken bir kopya iş bir birimi ile ilişkilidir. Bir aygıt iş olağanüstü durum kurtarma (DR) veya geri yükleme işleminin sonucu olarak oluşturulur.
* **Aygıt** – hello üzerinde hangi hello işi başlatıldı hello aygıt adı.
* **Tarihinde başlayan** – hello zaman zaman hello işi başlatıldı.
* **Süre** – hello süresi gerekli toocomplete hello işi.

işlerini Hello listesi, her 30 saniyede yenilenir.

Bu sayfada iş ile ilgili eylemler aşağıdaki hello gerçekleştirebilirsiniz:

* İş ayrıntılarını görüntüleme
* Bir işi iptal etme

## <a name="view-job-details"></a>İş ayrıntılarını görüntüleme
Aşağıdaki adımları tooview hello herhangi bir işi ayrıntılarını hello gerçekleştirin.

#### <a name="tooview-job-details"></a>tooview iş ayrıntıları
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **işleri**.

2. Merhaba, **işleri** dikey penceresinde, görüntü hello iş, ilgilendiğiniz uygun filtreleri ile çalışan bir sorgu. Çalışan veya işi iptal tamamlandı için arama yapabilirsiniz.

    ![İş dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Seçin ve bir iş'i tıklatın.

    ![İş dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. Merhaba iş ayrıntıları dikey penceresinde hello durumu, ayrıntıları, süresi istatistikleri ve veri istatistiklerini görüntüleyebilirsiniz.
   
    ![İş ayrıntıları](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Bir işi iptal etme
Aşağıdaki adımları toocancel çalışan bir işi hello gerçekleştirin.

> [!NOTE]
> Bir birim toochange hello birim türü değiştirme veya bir birim genişletme gibi bazı işleri iptal edilemez.


### <a name="toocancel-a-job"></a>toocancel bir işi
1. Merhaba üzerinde **işleri** sayfasında, uygun filtrelerle bir sorgu çalıştırarak toocancel istediğiniz hello çalışan iş görüntüler. Merhaba işi seçin.

2. Merhaba Seçili iş tooinvoke hello bağlam menüsünde sağ tıklatın ve **iptal**.

    ![İş ayrıntıları](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Onayınız istendiğinde **Evet**’e tıklayın. Bu işi iptal edildi.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[, StorSimple yedekleme ilkelerini yönetme](storsimple-8000-manage-backup-policies-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

