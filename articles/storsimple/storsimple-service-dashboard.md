---
title: "aaaStorSimple Yöneticisi hizmet panosunu | Microsoft Docs"
description: "Merhaba StorSimple Yöneticisi hizmet panosunu tanımlar ve açıklar nasıl toouse, StorSimple çözümünüzün toomonitor hello durumu."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Merhaba StorSimple Yöneticisi hizmet panosunu kullanma
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Yöneticisi hizmeti Pano sayfası bağlı toohello StorSimple Yöneticisi hizmeti, sistem yöneticisinin dikkat etmeniz gereken olanlar vurgulama tüm hello cihazlar Özet görünümünü sağlar. Bu öğretici hello Pano sayfası tanıtır, hello Pano içeriği ve işlevi açıklanmaktadır ve bu sayfadan gerçekleştirebileceğiniz hello görevleri açıklar.

![Hizmet panosu](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

Merhaba StorSimple Yöneticisi hizmet panosunu bilgisinden hello görüntüler:

* Merhaba, **grafik** alanı görebilir hello ilgili ölçümleri aygıtlarınız için grafik. (Yerel olarak sabitlenmiş ve katmanlı) hello birincil depolama görüntüleyebilirsiniz tüm hello aygıtların yanı sıra bir süre boyunca aygıtlarının kullandığı hello bulut depolama arasında kullanılır. Merhaba sağ üst köşesinde hello grafik toospecify 1 hafta, ay 1, 3 ay ya da 1 yıllık ölçek Hello denetimleri kullanın.
* Merhaba **kullanıma genel bakış** hello sağlanabilen ve tüm cihazları göreli toohello toplam depolama alanı tarafından kullanılabilir cihazlara kullanılan birincil depolama gösterir. **Sağlanan** toohello hazırlanmış ve kullanım için ayrılan while depolama miktarını başvuruyor **kullanılan** toousage birimlerin bağlı toohello cihazların Merhaba başlatıcılar tarafından görüntülenen şekilde başvuruyor.
* Merhaba **uyarıları** alanı uyarı önem derecesine göre gruplandırılmış tüm hello aygıtlar arasında anlık görüntüsünü tüm hello etkin uyarıları sağlar. Merhaba önem düzeyi tıklatıldığında açılır hello **uyarıları** sayfası, kapsamlı tooshow bu uyarıları. Merhaba üzerinde **uyarıları** sayfasında, bir bireysel uyarı tooview ek ayrıntılar önerilen eylemleri de dahil olmak üzere Bu uyarıyla ilgili tıklatabilirsiniz. Merhaba sorunu çözerseniz hello uyarı işaretini kaldırabilirsiniz.
* Merhaba **işleri** alanı bağlanan cihazlara anlık görüntüsü en son işlerin sağlar tooyour hizmet. Olanlar hello toorun sonraki 24 saat zamanlanmış veya devam eden, son 24 saat hello başarısız olanlar işleri adresindeki toolook kullanan bağlantıları vardır.
* Merhaba **Hızlı Bakış** alanı hizmet durumu, cihazların bağlı toohello hizmeti, hello hizmetinin konumunu ve hello hizmetiyle ilişkili hello aboneliğinizin ayrıntılarını sayısı gibi yararlı bilgileri sağlar. Bir bağlantı toohello işlemleri günlük yoktur. Merhaba bağlantı toosee tüm tamamlanan StorSimple Yöneticisi hizmet işlemleri listesini tıklatın.

Merhaba StorSimple Yöneticisi hizmeti Pano sayfası tooinitiate hello görevleri aşağıdaki kullanabilirsiniz:

* Merhaba hizmet kayıt anahtarını yeniden oluşturmak veya görüntüleyin.
* Merhaba hizmet verileri şifreleme anahtarı değiştirin.
* Merhaba işlem günlüklerini görüntüleyin.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Görüntülemek veya hello hizmet kayıt anahtarını yeniden oluşturma
Merhaba hizmet kayıt anahtarını kullanılan tooregister bir Microsoft Azure StorSimple cihaz hello StorSimple Yöneticisi hizmetiyle, böylelikle Hello aygıtı hello diğer yönetim işlemleri için Klasik Azure portalında görünür. başlangıç anahtarı hello ilk aygıtta oluşturulur ve hello aygıtlarınızı kalanıyla paylaşılan.

Tıklatarak **kayıt anahtarı** (Merhaba hello sayfanın alt kısmında) açılır hello **hizmet kayıt anahtarını** iletişim kutusu, ya da kopyalama hello geçerli hizmet kayıt anahtarı toohello Pano yapabileceğiniz veya Merhaba hizmet kayıt anahtarını yeniden oluşturun.

Başlangıç anahtarı yeniden oluşturuluyor önceden kayıtlı cihazları etkilemez: hello anahtarı yeniden sonra hello hizmetine kayıtlı hello aygıtları etkiler.

Görüntüleme ve hello hizmet kayıt anahtarı, Git çok oluşturma hakkında daha fazla bilgi için[hello hizmet kayıt anahtarını Al](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>Değişiklik hello hizmet verileri şifreleme anahtarı
Hizmet veri şifreleme anahtarları kullanılan tooencrypt gizli müşteri, StorSimple Yöneticisi hizmet toohello StorSimple Cihazınızı gönderilen depolama hesabının kimlik bilgilerini gibi verilerdir. BT kuruluşunuzun hello depolama cihazlarında bir anahtar döndürme ilkesi varsa toochange bu anahtarlar düzenli aralıklarla gerekir. Merhaba anahtar değiştirme işlemi bağlı olarak biraz farklı olabilir bir tek veya birden çok cihazı hello StorSimple Yöneticisi hizmeti tarafından yönetilen yoktur.

Değişen hello hizmet verileri şifreleme anahtarı 3 adımlı bir işlemdir:

1. Merhaba Klasik Azure portalı kullanarak bir aygıtı toochange hello hizmet verileri şifreleme anahtarı yetkilendirin.
2. StorSimple için Windows PowerShell kullanarak hello hizmet verileri şifreleme anahtarı değişikliği başlatır.
3. Birden çok StorSimple cihazınız varsa, hello hizmet verileri şifreleme anahtarı hello üzerindeki diğer cihazlar güncelleştirin.

Merhaba aşağıdaki adımlarda hello hizmet verileri şifreleme anahtarı için hello geçiş işlemi açıklanmıştır.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Merhaba işlem günlüklerini görüntüle
Merhaba işlem günlükleri bağlantı hello kullanılabilir tıklayarak hello işlem günlükleri görüntüleyebilirsiniz **Hızlı Bakış** hello panonun bölmesi. Bu toohello yönetim sürecek Hizmetler Sayfası, burada filtre ve hello bkz belirli tooyour StorSimple Yöneticisi hizmeti günlüğe kaydeder.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple cihazını sorun giderme](storsimple-troubleshoot-operational-device.md).
* Hakkında daha fazla çok bilgi[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

