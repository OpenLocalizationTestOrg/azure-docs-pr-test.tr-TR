---
title: "aaaView ve StorSimple sanal dizinin işlerini yönetme | Microsoft Docs"
description: "Merhaba StorSimple cihaz Yöneticisi hizmeti işleri sayfasında açıklar ve nasıl toouse onu hello StorSimple sanal dizinin tootrack yeni ve geçerli işleri."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Merhaba StorSimple sanal dizinin Hello StorSimple cihaz Yöneticisi hizmet tooview işleri kullanın
## <a name="overview"></a>Genel Bakış
Merhaba **işleri** dikey görüntüleme ve bağlı tooyour StorSimple cihaz Yöneticisi hizmeti olan sanal dizileri başlatılan işlerini yönetmek için tek bir merkezi portal sağlar. Birden çok sanal cihazda çalışan, tamamlanmış ve başarısız işleri görüntüleyebilirsiniz. Sonuçları bir tablo biçiminde sunulur.

![İşlerini dikey penceresi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

Hızlı bir şekilde hello işleri, içinde alanları gibi filtreleyerek ilginizi çekiyor mu bulabilirsiniz:

* **Zaman aralığı** – işleri filtrelenmiş göre hello tarih ve saat aralığı olabilir.
* **Aygıtları** – işleri bağlı belirli cihaz tooyour hizmette başlattı. Merhaba filtrelenen işler sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:
  
  * **Ad** – hello iş adı olabilir **tüm**, **yedekleme**, **kopya**, **yük devri**, **güncelleştirmelerini yükleme** , veya **güncelleştirmelerini yükleme**.
  * **Durum** – işleri olabilir **tüm**, **devam eden**, **başarılı**, veya **başarısız**, veya **iptal edildi**.
  * **Varlık** – hello işleri birim, paylaşım veya cihaz ile ilişkili olabilir.
  * **Aygıt** – hello üzerinde hangi hello işi başlatıldı hello aygıt adı.
  * **Tarihinde başlayan** – hello zaman zaman hello işi başlatıldı.
  * **Süre** – hello süresince hangi hello işinde çalıştırıldı.
* **Durum** – tüm, çalışan, tamamlandı ya da başarısız işleri için arama yapabilirsiniz.
* **İş türünü** – hello iş türü tümü, yedekleme, geri yükleme, yük devretme olması, güncelleştirmeleri karşıdan veya güncelleştirmeleri yükleyin.

işlerini Hello listesi, her 30 saniyede yenilenir.

## <a name="view-job-details"></a>İş ayrıntılarını görüntüleme
Aşağıdaki adımları tooview hello herhangi bir işi ayrıntılarını hello gerçekleştirin.

#### <a name="tooview-job-details"></a>tooview iş ayrıntıları
1. Merhaba üzerinde **işleri** dikey penceresinde, görüntü hello iş, ilgilendiğiniz uygun filtreleri ile çalışan bir sorgu. Tamamlanan veya çalışan işleri arama yapabilirsiniz.
2. Bir işi hello tablo işleri listeden seçin.
   
    ![İş dikey penceresi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. Merhaba sayfasının Hello altında tıklatın **ayrıntıları**.
4. Merhaba, **ayrıntıları** iletişim kutusu, durumu, Ayrıntılar ve süresi istatistikleri görüntüleyebilirsiniz. Merhaba aşağıda gösterilmiştir hello örneği **yedekleme işi ayrıntılarını** iletişim kutusu.
   
    ![İş ayrıntıları](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Merhaba sanal makine hello hiper yöneticide duraklatıldığında işi hataları
Bir iş olduğunda StorSimple sanal dizinin ve hello aygıt (hiper yöneticide sağlanan sanal makine) ilerleme 15 dakikadan daha duraklatılır, hello işi başarısız. Bu tooyour StorSimple sanal dizinin zaman hello Microsoft Azure zaman ile eşitlenmemiş yapılıyor. 

Aşağıdaki hata hello görürsünüz: "cihaz zamanınızı hello Microsoft Azure süresi 15 dakikadan fazla ile eşitlenmedi. Merhaba hiper yönetici ve hello aygıt saatleri bir NTP sunucusu ile eşitlendiğinden emin olmak. Bağlantı sorunu olmadığından olduğunu doğrulayın. tootroubleshoot bağlantı sorunları, Çalıştır tanılama testleri hello yerel Web'den UI sanal cihazınızın."

Bu hatalar toobackup, geri yükleme, güncelleştirme ve yük devretme işlemlerini uygulayın. Hyper-V, sanal makine sağlandıktan, hello makine sonunda zaman, hiper yönetici ile eşitler. Bu gerçekleştikten sonra işi yeniden başlatın.

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl toouse hello yerel web kullanıcı Arabirimi tooadminister StorSimple sanal dizinizi öğrenin](storsimple-ova-web-ui-admin.md).

