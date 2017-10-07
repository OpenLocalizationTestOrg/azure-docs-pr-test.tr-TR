---
title: "aaaView ve StorSimple işlerini yönetme | Microsoft Docs"
description: "Merhaba StorSimple Yöneticisi hizmeti işleri sayfasında açıklar ve nasıl toouse, tootrack son, geçerli ve zamanlanmış yedekleme işleri."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a>Merhaba StorSimple Yöneticisi hizmet tooview kullanma ve StorSimple işleri yönetme
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Genel Bakış
Merhaba **işleri** sayfasını görüntülemek için tek bir merkezi portal sağlar ve cihazlarda başlatılmış işlerini yönetme bağlı tooyour StorSimple Yöneticisi hizmeti. Birden çok aygıt zamanlanmış, çalışan, tamamlanmış ve başarısız işleri görüntüleyebilirsiniz. Sonuçları bir tablo biçiminde sunulur. 

![İşler sayfası](./media/storsimple-manage-jobs/HCS_JobsPage.png)

Hızlı bir şekilde hello işleri, içinde alanları gibi filtreleyerek ilginizi çekiyor mu bulabilirsiniz:

* **Durum** – işleri çalıştırıyor olabilir, zamanlanan, başarısız, tamamlandı, iptal etme veya iptal edilmiş.
* **Tür** – oluşturulabilir bir zamanlanmış veya isteğe bağlı yedekleme sonucu (**ele yedekleme**), kopyalama, bir cihaz geri yükleme veya güncelleştirme işlemi.
* **Aygıtları** – işleri belirli bağlı cihaz tooyour'nda bir hizmeti başlatıldı.
* **Başlangıç ve bitiş** – işleri filtrelenmiş göre hello tarih ve saat aralığı olabilir.

Merhaba filtrelenen işler sonra öznitelikleri aşağıdaki hello hello temelinde tabloda verilmiştir:

* **Tür** – yedekleme, kopya, geri yükleme, yük devretme veya güncelleştirme.
* **Durum** – çalıştıran, zamanlanan, başarısız oldu, tamamlandı, iptal etme veya iptal edildi.
* **Varlık** – hello işleri bir birim, bir yedekleme İlkesi veya bir aygıt ile ilişkili olabilir. Zamanlanmış bir yedekleme işi bir yedekleme ilkesiyle ilişkili iken bir kopya işi bir birimi ile ilişkilidir. Bir aygıt iş olağanüstü durum kurtarma (DR) veya geri yükleme işleminin sonucu olarak oluşturulur.
* **Aygıt** – hello üzerinde hangi hello işi başlatıldı hello aygıt adı.
* **Started On** – hello zaman zaman hello işi başlatıldı.
* **İlerleme** – hello tamamlanma çalışan işin. Tamamlanmış bir iş için bu her zaman % 100 olmalıdır.

işlerini Hello listesi, her 30 saniyede yenilenir.

Bu sayfada iş ile ilgili eylemler aşağıdaki hello gerçekleştirebilirsiniz:

* İş ayrıntılarını görüntüleme
* Bir işi iptal etme

## <a name="view-job-details"></a>İş ayrıntılarını görüntüleme
Aşağıdaki adımları tooview hello herhangi bir işi ayrıntılarını hello gerçekleştirin.

#### <a name="tooview-job-details"></a>tooview iş ayrıntıları
1. Merhaba üzerinde **işleri** sayfasında, hello iş, ilgilendiğiniz uygun filtrelerle bir sorgu çalıştırarak görüntüleyebilirsiniz. Çalışan veya işi iptal tamamlandı için arama yapabilirsiniz.
2. Bir iş seçin.
3. Merhaba sayfasının Hello altında tıklatın **ayrıntıları**.
4. Merhaba, **yedekleme işi ayrıntılarını** iletişim kutusu, hello durumu, ayrıntıları, süresi istatistikleri ve veri istatistiklerini görüntüleyebilirsiniz.

## <a name="cancel-a-job"></a>Bir işi iptal etme
Aşağıdaki adımları toocancel çalışan bir işi hello gerçekleştirin.

### <a name="toocancel-a-job"></a>toocancel bir işi
1. Merhaba üzerinde **işleri** sayfasında, uygun filtrelerle bir sorgu çalıştırarak toocancel istediğiniz hello çalışan iş görüntüler.
2. Merhaba işi seçin.
3. Merhaba sayfasının Hello altında tıklatın **iptal**.
4. Onayınız istendiğinde **Evet**’e tıklayın.

Bu işi iptal edildi.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[, StorSimple yedekleme ilkelerini yönetme](storsimple-manage-backup-policies.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

