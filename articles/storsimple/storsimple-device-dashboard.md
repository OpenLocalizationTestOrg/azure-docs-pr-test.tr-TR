---
title: "aaaUse hello StorSimple Yöneticisi cihaz Pano | Microsoft Docs"
description: "Merhaba StorSimple Yöneticisi hizmet cihaz Panosu açıklar ve nasıl toouse, tooview storage ölçümleri ve bağlı başlatıcıları ve Bul hello seri numarasını ve IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Merhaba cihaz Pano StorSimple Yöneticisi hizmetini kullanma  

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Yöneticisi cihaz Pano bilgi belirli bir StorSimple cihazı için genel bir bakış sunar, buna karşılık toohello servis panoyu tüm Microsoft Azure StorSimple çözümünüzde dahil hello cihazlarını hakkında bilgi verir.

![Cihaz Pano sayfası](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

Başlangıç Panosu, aşağıdaki bilgilerle hello içerir:

* **Grafik alanı** – hello ilgili depolama ölçümleri hello Pano hello üstündeki hello grafik alanında görebilirsiniz. Bu grafikte görüntülemek hello toplam birincil depolama (ana bilgisayar tooyour aygıt tarafından yazılan veri miktarı hello) için Ölçümler ve toplam hello bulut bir süre boyunca cihazınız tarafından tüketilen depolama.
  
     Bu bağlamda *birincil depolama* toohello toplam hello ana bilgisayar tarafından yazılan veri miktarını gösterir ve birim türüne göre ayrılabilir: *birincil katmanlı depolama* her ikisini de içeren yerel olarak depolanan verileri ve verileri Katmanlı toohello bulut; *birincil yerel olarak sabitlenmiş depolama* yerel olarak depolanan yalnızca verileri içerir. *Bulut depolama*, üzerinde diğer yandan Merhaba, hello toplam hello bulutta depolanan veri miktarını ölçüsüdür. Bu, katmanlı veri ve yedeklemeler içerir. Birincil depolama hello hello veri yinelenenleri kaldırılmış ve sıkıştırılmış önce kullanılan depolama alanı miktarını gösterir ancak hello bulutta depolanan veriler yinelenenleri kaldırılmış ve sıkıştırılmış, unutmayın. (Bu iki sayının tooget hello sıkıştırma oranı hakkında bir fikir karşılaştırabilirsiniz.) Hem birincil hem de için ve bulut depolama, hello gösterilen tutarlar yapılandırdığınız sıklığı izleme hello üzerinde tabanlı olacaktır. Bir hafta sıklığı seçerseniz, örneğin, ardından hello grafik veri her günü için hello önceki hafta gösterir.
  
     Merhaba grafiği aşağıdaki gibi yapılandırabilirsiniz:
  
  * toosee hello süre, select hello tüketilen bulut depolama alanı miktarını **bulut depolama kullanılan** seçeneği. select hello hello konak tarafından yazılmış toosee hello toplam depolama **birincil KATMANLI depolama kullanılan** ve **birincil yerel olarak SABİTLENMİŞ depolama kullanılan** seçenekleri. Merhaba çizimde, her iki seçenek seçilir; Bu nedenle, hem bulut hem de birincil depolama için depolama tutarlar hello grafik gösterir. Tüm birincil depolama önceki tooinstalling güncelleştirme 2 kullanılan Not hello tarafından gösterilen **birincil KATMANLI depolama kullanılan** satır.
  * Merhaba açılır menü hello sağ üst köşesinde hello grafik toospecify 1 hafta, ay 1, 3 aylık veya 1 yıllık dönem kullanın. Üst düzey grafik hello Not günde yalnızca bir kez yenilendiğini ve bu nedenle yansıtılacaktır önceki günün toplamları hello.
    
    Daha fazla bilgi için bkz: [kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet toomonitor hello](storsimple-monitor-device.md).
* **Kullanıma genel bakış** – hello **kullanıma genel bakış** alanı, birincil depolama hello miktarını kullanıldığında, sağlanan depolama ve hello maksimum depolama kapasitesi, cihazınız için başlangıç miktarı görebilirsiniz. Bu kullanım sayıları toohello en fazla kullanılabilir olan depolama miktarını karşılaştırarak tooobtain ek depolama alanı gerekiyorsa bir bakışta görebilirsiniz. Bu genel bakışta 15 dakikada bir güncelleştirilir ve güncelleştirme sıklığı hello fark nedeniyle olandan farklı numaraları günlük güncelleştirilen hello grafik alanında yukarıdaki gösterilen gösterebilir unutmayın. Daha fazla bilgi için bkz: [kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet toomonitor hello](storsimple-monitor-device.md).
* **Uyarıları** – hello **uyarıları** alanı hello uyarıları, cihazınız için genel bir bakış içerir. Uyarıları önem derecesine göre gruplandırılır ve bir sayısı her önem düzeyinin uyarılara hello sayısının sağlanır. Önem derecesi hello kapsamlı bir görünümünü açar hello uyarısına tıklandığında sekmesini tooshow yalnızca bu önem düzeyi bu cihaz için uyarıları hello uyarır.
* **İşlerini** – hello **işleri** son iş etkinliğinin sonucunu hello alanı gösterir. Bu, hello sistem beklendiği gibi çalışıyor veya tootake düzeltme eylemi gerektiğini size bildirmek güvence altına almak. son tamamlanan işler hakkında daha fazla bilgi toosee tıklatın **işleri başarılı hello son 24 saat**.
* Merhaba **Hızlı Bakış** hello hello Pano sağında bir alanı cihaz modeli, seri numarası, durumu, açıklama ve birimlerin sayısı gibi yararlı bilgileri sağlar.

Ayrıca, yük devretme yapılandırma ve hello aygıt panosundan bağlı başlatıcıları görüntüleyin.

Bu sayfada gerçekleştirilebilir hello ortak görevler şunlardır:

* Bağlı başlatıcıları görüntüleyin
* Merhaba cihaz seri numarasını Bul
* Merhaba aygıt hedef IQN Bul

## <a name="view-connected-initiators"></a>Bağlı başlatıcıları görüntüleyin
Merhaba tıklatarak bağlı tooyour aygıt olduğundan hello iSCSI başlatıcıları görüntüleyebilirsiniz **görünüm bağlı başlatıcıları** hello sağlanan bağlantı **Hızlı Bakış** aygıt panosunun alanı. Bu sayfa tablo tooyour aygıt başarıyla bağlandıysanız hello başlatıcıları listesini sağlar. Her bir başlatıcısını görebilirsiniz:

* Merhaba iSCSI tam adını (IQN) hello Başlatıcı bağlı.
* Bu bağlı başlatıcı veren hello erişim denetimi kaydı (ACR) Hello adı.
* Başlangıç IP adresi hello Başlatıcı bağlı.
* Merhaba ağ arabirimleri, hello Başlatıcı bağlı tooon depolama aygıtı değil. Bu verileri 0 tooDATA 5 aralığında değişebilir.
* Bağlı başlatıcı hello tüm hello birimleri toohello ACR yapılandırmasına göre tooaccess izin verilir.

Bu listedeki beklenmeyen başlatıcıları bakın veya hello olanları beklenen görüyor musunuz ACR yapılandırmanızı gözden geçirin. En fazla 512 başlatıcıları tooyour aygıt bağlanabilir.

## <a name="find-hello-device-serial-number"></a>Merhaba cihaz seri numarasını Bul
Merhaba cihazda Microsoft çok yollu g/ç (MPIO) yapılandırdığınızda hello cihaz seri numarasını gerekebilir. Aşağıdaki adımları toofind hello cihaz seri numarasını hello gerçekleştirin.

#### <a name="toofind-hello-device-serial-number"></a>toofind hello cihaz seri numarası
1. Çok gidin**aygıtları** > **Pano**.
2. Merhaba sağ bölmesinde hello panonun hello bulun **Hızlı Bakış** alanı.
3. Aşağı kaydırın ve hello seri numarasını bulun.

## <a name="find-hello-device-target-iqn"></a>Merhaba aygıt hedef IQN Bul
StorSimple Cihazınızda hello karşılıklı kimlik doğrulama protokolü (CHAP) yapılandırdığınızda hello aygıt hedef IQN gerekebilir. Aşağıdaki adımları toofind hello aygıt hedef IQN hello gerçekleştirin.

### <a name="toofind-hello-device-target-iqn"></a>toofind hello aygıt hedef IQN
1. Çok gidin**aygıtları** > **Pano**.
2. Merhaba sağ bölmesinde hello panonun hello bulun **Hızlı Bakış** alanı.
3. Aşağı kaydırın ve hello hedef IQN bulun.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba hakkında daha fazla bilgi [StorSimple Yöneticisi hizmet panosunu](storsimple-service-dashboard.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

