---
title: "aaaMonitor StorSimple 8000 serisi Cihazınızı | Microsoft Docs"
description: "Toouse hello StorSimple Aygıt Yöneticisi'ni nasıl hizmet toomonitor kullanımı, g/ç performans ve kapasite kullanımı açıklanmaktadır."
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>StorSimple Cihazınızı Hello StorSimple cihaz Yöneticisi hizmeti toomonitor kullanın
## <a name="overview"></a>Genel Bakış
StorSimple çözümünüzün içinde hello StorSimple cihaz Yöneticisi hizmeti toomonitor belirli cihazları kullanabilirsiniz. G/ç performansı, kapasite kullanımı, ağ verimliliğini ve cihaz performans ölçümleri göre özel grafikler oluşturma ve bu toohello Pano sabitleyin. Daha fazla bilgi için çok Git[portal panonuzu özelleştirebilir](/articles/azure-portal/azure-portal-dashboards.md).

tooview hello izleme bilgilerini hello Azure portal'ın belirli bir aygıt için hello StorSimple cihaz Yöneticisi hizmeti seçin. Hello aygıtların, listeden Cihazınızı seçin ve çok gidin**İzleyici**. Merhaba ardından gördüğünüz **kapasite**, **kullanım**, ve **performans** hello seçili cihaz için grafik.

## <a name="capacity"></a>Kapasite
**Kapasite** parçaları hello sağlanan alan ve hello aygıtta kalan hello alan. Kapasite kalan Merhaba, ardından yerel olarak sabitlenmiş veya katmanlı olarak görüntülenir.

sağlanan hello ve kapasite kalan daha fazla ayrıntılarıyla katmanlı ve yerel olarak sabitlenmiş birimleri tarafından. Her birim için kapasite hello sağlanan ve kapasite hello aygıtta kalan hello görüntülenir.

![G/ç kapasitesi](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Kullanım
**Kullanım** parçaları ölçümleri ilgili toohello hello birimleri, birim kapsayıcıları veya aygıt tarafından kullanılan veri depolama alanı miktarı. Birincil depolama, bulut depolama veya aygıt depolama kapasitesi kullanımını hello dayalı raporlar oluşturabilirsiniz. Kapasite kullanımı, belirli bir birimin, özel birim kapsayıcısı veya tüm birim kapsayıcıları ölçülebilir.
Varsayılan olarak, son 24 saat için hello kullanım bildirilir. Merhaba grafik toochange hello süresi hangi hello seçerek kullanım bildirilen düzenleyebilirsiniz:
* Son 24 saat
* Son 7 gün
* Son 30 gün
* Son 90 gün
* Geçen yıl


Merhaba birincil, Bulut ve kullanılan yerel depolama gibi açıklanabilir:

### <a name="primary-storage-usage"></a>Birincil depolama kullanımı
Bu grafikler hello hello veri yinelenenleri kaldırılmış ve sıkıştırılmış önce tooStorSimple birimleri yazılan veri miktarını gösterir. Birim kapsayıcısı içinde veya tek bir birim için tüm birimleri tarafından kullanılan birincil depolama hello görüntüleyebilirsiniz. kullanılan birincil depolama hello daha fazla yerel olarak sabitlenmiş depolama kullanılan birincil katmanlı depolama tarafından kullanılan ve birincil ayrılmıştır.

Merhaba aşağıdaki grafikleri önce StorSimple cihazını ve bulut anlık görüntü alındıktan sonra için kullanılan birincil depolama hello gösterir. Bir bulut anlık görüntü yalnızca birim verilerini olarak hello birincil depolama değiştirmemelisiniz. Gördüğünüz gibi bir bulut anlık sonucu olarak kullanılan hello birincil katmanlı veya yerel olarak sabitlenmiş depolama fark hello grafik gösterir. Merhaba bulut anlık görüntüsü yaklaşık 11:50 pm cihazdaki başlangıcı.

![Bulut anlık görüntüsü sonra birincil kapasite kullanımı](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

(Katmanlı veya yerel olarak sabitlenmiş) hangi birimlerin hello bağlı ana bilgisayar tooyour StorSimple cihazında GÇ Şimdi Çalıştır, birincil katmanlı depolama artış görürsünüz ya da kullanılan depolama alanı bağlı olarak birincil yerel olarak sabitlenmiş hello veri yazma. Burada, StorSimple cihazını hello birincil depolama kullanımı grafiklerde bulunmaktadır. Bu aygıtta hello StorSimple ana bilgisayar hizmet veren başlatılan hello aygıtta katmanlı birim üzerinde yaklaşık 2: 30'e yazar. Merhaba yoğun hello Yazma Bayt/sn hello ana bilgisayarında çalışan toohello GÇ karşılık gelen cinsinden görebilirsiniz.

![Birimler üzerinde çalışan GÇ katmanlı performansı](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Olmadığından yerel olarak sabitlenmiş hello birincil kullanım değişmeden kalır ancak geçti yukarı kullanıldığında, hello birincil katmanlı depolama bakarsanız hiçbir yazma toohello yerel olarak sabitlenmiş birimleri hello aygıtta sundu.

![G/ç çalıştırırken katmanlı birimlerin birincil kapasite kullanımı](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Çalıştırıyorsanız, güncelleştirme 3 veya sonraki, hello birincil depolama kapasitesi kullanımını tek bir birim, tüm birimleri, tüm katmanlı birimlerin ve tüm yerel olarak sabitlenmiş birimleri tarafından aşağıda gösterildiği gibi ayırmak. Tüm tarafından yerel olarak sabitlenmiş birimlerin sağlayacak çiğnemekten tooquickly onaylaması hello yerel katmanı ne kadarının kullanılan.

![Tüm katmanlı birimlerin birincil kapasite kullanımı](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Tüm yerel olarak sabitlenmiş birimler için birincil kapasite kullanımı](./media/storsimple-8000-monitor-device/monitor-usage4.png)

Daha fazla hello listesinde hello birimlerin her birinde tıklatın ve hello karşılık gelen kullanımına bakın.

![Tüm yerel olarak sabitlenmiş birimler için birincil kapasite kullanımı](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Bulut depolama kullanımı
Bu grafikler hello kullanılan bulut depolama alanı miktarını gösterir. Bu veri yinelenenleri kaldırılmış ve sıkıştırılmış. Bu miktar, tüm birincil biriminde yansıtılan değil ve gerekli veya eski bekletme amacıyla tutulur verileri içerebilen bulut anlık görüntüleri içerir. Merhaba numarası tam olmaz ancak hello birincil ve hello veri azaltma hakkında bir fikir oranı, bulut depolama tüketim rakamları tooget karşılaştırabilirsiniz.

bir bulut anlık görüntüsü durumdayken hello aşağıdaki grafikleri hello bulut depolama StorSimple cihazını kullanımını gösterir.

* Merhaba bulut anlık görüntüsü yaklaşık 11:50:00 cihazdaki tarihinde başladı ve hello bulut anlık görüntüsü önce görebilirsiniz kullanılan bulut depolama alanı yoktu. 
* Bir kez hello bulut anlık görüntüsü tamamlandı, hello bulut depolama alanı kullanımı 0,89 GB görüntüsü. 
* Merhaba bulut anlık görüntüsü devam ederken, bulunmaktadır ayrıca karşılık gelen yoğun hello g/ç aygıtı toocloud gelen.

    ![Bulut anlık görüntüsü önce bulut depolama alanı kullanımı](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Bulut anlık görüntüsü sonra bulut depolama alanı kullanımı](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![GÇ bir bulut anlık görüntüsü sırasında aygıt toocloud verilerini](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Yerel depolama kullanımı
Bu grafikler hello SSD doğrusal katmanı içerdiğinden olacağı birden çok birincil depolama kullanımı hello cihaz için hello toplam kullanımını gösterir. Bu katman, bir cihazın diğer katmanları hello üzerinde mevcut da veri miktarı içerir. Yeni veri geldiğinde, hello eski verileri (aynı zamanda, yinelenenleri kaldırılmış sıkıştırılmış ve) taşınan toohello HDD katmanı ve daha sonra toohello bulut böylece hello kapasite hello SSD doğrusal katmanındaki geçiş sırasında.

Zaman içinde toohello bulut hello veri toobe başlatıncaya kadar kullanılan kullanılan ve yerel depolama büyük olasılıkla birlikte artıracaktır birincil depolama katmanlı. Bu noktada, kullanılan hello yerel depolama büyük olasılıkla tooplateau başlar, ancak daha fazla veri yazıldığı kullanılan birincil depolama hello artıracaktır.

Merhaba aşağıdaki grafikleri bir bulut anlık görüntüsü durumdayken bir StorSimple cihaz için kullanılan birincil depolama hello gösterir. Merhaba bulut anlık görüntüsü 11: 50'de ve o anda azalan hello yerel depolama başlandı. kullanılan hello yerel depolama alanı 1.445 GB too1.09 GB ' kapandı. Bu büyük olasılıkla hello hello doğrusal SSD katmanına sıkıştırılmamış veri yinelenenleri kaldırılmış, sıkıştırılmış ve hello HDD katmanı taşındı gösterir. Merhaba aygıt büyük miktarda veri hello SSD ve HDD katmanları zaten varsa, bu azaltma göremeyebilirsiniz unutmayın. Bu örnekte, çok küçük miktarda veri hello aygıtın vardır.

![Bulut anlık görüntüsü sonra yerel depolama alanı kullanımı](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Performans
**Performans** parçaları ölçümleri ilgili okuma toohello sayısı ve hello ana bilgisayar sunucusu ve hello aygıt veya hello cihaz ve hello bulut Başlatıcı arabirimleri yazma işlemlerini ya da hello iSCSI arasında. Bu performans, belirli bir birimin, özel birim kapsayıcısı ve tüm birim kapsayıcıları için ölçülebilir. Performans, çeşitli ağ arabirimleri, Cihazınızda CPU kullanımı ve hello için ağ verimliliği de içerir.

### <a name="io-performance-for-initiator-toodevice"></a>Başlatıcı toodevice için g/ç performansı
Aşağıdaki Hello grafik hello g/ç hello Başlatıcı tooyour aygıtın tüm hello birimleri üretim cihaz için gösterir. çizilen hello ölçümleri salt okunurdur ve saniye başına baytların yazma. Ayrıca okuma, yazma ve bekleyen GÇ grafik ya da okuma ve yazma gecikmeleri.

![Başlatıcı toodevice için g/ç performansı](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>Aygıt toocloud için g/ç performansı
Hello için aynı aygıt hello g/ç işlemleri çizilen hello cihaz toohello bulut hello verileri için tüm birim kapsayıcıları hello için. Bu aygıtta hello veri hello doğrusal katmanında yalnızca ve hiçbir şey toohello bulut geçmiş. Aygıt toohello buluttan gerçekleşen hiçbir okuma-yazma işlemleri vardır. Bu nedenle, hello yükselmeleri hello grafikte hello sinyal hello cihaz ve hello hizmeti arasındaki denetleneceği zaman toohello sıklığı karşılık gelen bir aralığı 5 dakika altındadır.

Merhaba aynı aygıt, bir bulut anlık görüntüsü 11: 50'de başlangıç hacim verileri alındığı için. Bu veri akışının hello aygıt toohello buluttan ile sonuçlandı. Yazma toohello bulut bu süre içinde sunulduğunu. Merhaba GÇ grafik bir en yüksek olduğunda hello anlık görüntü alındıktan hello Yazma Bayt/sn karşılık gelen toohello zaman içinde gösterir.

![GÇ bir bulut anlık görüntüsü sırasında aygıt toocloud verilerini](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Cihaz ağ arabirimleri için ağ verimliliği
**Ağ verimliliği** hello iSCSI başlatıcısı ağ arabirimlerinden hello ana bilgisayar sunucusu ve hello cihaz ve hello aygıt hello bulut arasında aktarılan parçaları ölçümleri ilgili toohello veri miktarını. Bu ölçüm, Cihazınızda her hello iSCSI ağ arabirimleri için izleyebilirsiniz.

Her iki bulut etkin (varsayılan) oluştu, Cihazınızda GbE ağ Hello hello veri 0, 1 1 için grafikleri Göster hello ağ verimliliği aşağıdaki ve iSCSI etkin. Bu aygıtta üzerinde 14 Haziran yaklaşık 9 pm konumunda, veri (hangi noktaları tootiering olan zaman hiçbir bulut anlık görüntüleri sırasında gerçekleştirilen hello mekanizması toomove hello veri hello bulutunu) toohello bulut sunulmasını GÇ'de sonuçlandı hello buluta katmanlı. Yoktur karşılık gelen yoğun hello ağ işleme grafiğinde hello aynı anda ve çoğu hello ağ trafiği için giden toohello bulut.

![Data 0 için ağ verimliliği](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Biz hello Data 1 arabirimi üretilen iş grafiği bakarsanız, başka bir 1 GbE ağ, yalnızca iSCSI etkin arabirimi, sonra bu sürenin neredeyse hiçbir ağ trafiğini vardı.

![Veri 1 için bir ağ verimliliği](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>Cihaz için CPU kullanımı
**CPU kullanımı** parçaları ölçümleri aygıtınızda kullanılan toohello CPU ilgili. Merhaba aşağıdaki grafikte bir aygıt için hello CPU kullanımı istatistiklerini üretimde gösterir.

![Cihaz için CPU kullanımı](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[hello StorSimple Aygıt Yöneticisi'ni hizmet cihaz Panosu kullanmak](storsimple-device-dashboard.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-manager-service-administration.md).

