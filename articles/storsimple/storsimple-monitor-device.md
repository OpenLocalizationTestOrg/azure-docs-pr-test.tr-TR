---
title: "aaaMonitor StorSimple Cihazınızı | Microsoft Docs"
description: "Toouse nasıl hello StorSimple Yöneticisi hizmeti toomonitor g/ç performansı, kapasite kullanımı, ağ verimliliğini ve cihaz performans açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>StorSimple Cihazınızı Hello StorSimple Yöneticisi hizmet toomonitor kullanın
## <a name="overview"></a>Genel Bakış
StorSimple çözümünüzün içinde hello StorSimple Yöneticisi hizmeti toomonitor belirli cihazları kullanabilirsiniz. G/ç performansı, kapasite kullanımı, ağ verimliliğini ve cihaz performans ölçümleri göre özel grafikler oluşturabilirsiniz. 

tooview hello hello Klasik Azure portalı select hello StorSimple Yöneticisi hizmeti, belirli bir aygıt için bilgileri izleme. Merhaba tıklatın **İzleyici** sekmesini tıklatın ve ardından hello aygıtları listesinden seçin. Merhaba **İzleyici** sayfası aşağıdaki bilgilerle hello içerir.

## <a name="io-performance"></a>G/ç performansı
**G/ç performansı** parçaları ölçümleri ilgili okuma toohello sayısı ve hello ana bilgisayar sunucusu ve hello aygıt veya hello cihaz ve hello bulut Başlatıcı arabirimleri yazma işlemlerini ya da hello iSCSI arasında. Bu performans, belirli bir birimin, özel birim kapsayıcısı ve tüm birim kapsayıcıları için ölçülebilir.

Aşağıdaki Hello grafik hello g/ç hello Başlatıcı tooyour aygıtın tüm hello birimleri üretim cihaz için gösterir. çizilen hello ölçümleri salt okunurdur ve saniye başına baytların yazma, okuma ve yazma g/ç işlemleri, saniyede ve okuma ve gecikme yazma.

![Başlatıcı toodevice g/ç performansı](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Hello için aynı aygıt hello g/ç işlemleri çizilen hello cihaz toohello bulut hello verileri için tüm birim kapsayıcıları hello için. Bu aygıtta hello veri hello doğrusal katmanında yalnızca ve hiçbir şey toohello bulut geçmiş. Aygıt toohello buluttan gerçekleşen hiçbir okuma-yazma işlemleri vardır. Bu nedenle, hello yükselmeleri hello grafikte hello sinyal hello cihaz ve hello hizmeti arasındaki denetleneceği zaman toohello sıklığı karşılık gelen bir aralığı 5 dakika altındadır. 

![Aygıt toocloud g/ç performansı](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Merhaba aynı aygıt, bir bulut anlık görüntüsü 2: 00'dan başlayarak hacim verileri alındığı için. Bu veri akışının hello aygıt toohello buluttan ile sonuçlandı. Okuma-yazma işlemleri toohello bulut bu süre içinde sunulduğunu. Merhaba GÇ grafik bir yoğun hello karşılık gelen çeşitli ölçümleri gösterir hello anlık görüntü ne zaman alındığı toohello zaman. 

![Bulut anlık görüntüsü sonra cihaz toocloud için g/ç performansı](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Kapasite kullanımı
**Kapasite kullanımı** parçaları ölçümleri ilgili toohello hello birimleri, birim kapsayıcıları veya aygıt tarafından kullanılan veri depolama alanı miktarı. Birincil depolama, bulut depolama veya aygıt depolama kapasitesi kullanımını hello dayalı raporlar oluşturabilirsiniz. Kapasite kullanımı, belirli bir birimin, özel birim kapsayıcısı veya tüm birim kapsayıcıları ölçülebilir.

Merhaba birincil, Bulut ve cihaz depolama kapasitesi şu şekilde açıklanabilir:

### <a name="primary-storage-capacity-utilization"></a>Birincil depolama kapasitesi kullanımı
Bu grafikler hello hello veri yinelenenleri kaldırılmış ve sıkıştırılmış önce tooStorSimple birimleri yazılan veri miktarını gösterir. Tüm birimleri veya tek bir birim için hello birincil depolama alanı kullanımı görüntüleyebilirsiniz.

Bu her iki durumda da hello birincil depolama birimi kapasite kullanımı grafikleri her hello ayrı birimleri ve hello birincil veri toplama karşı tüm birimler için görüntülediğinizde hello iki sayı arasında bir uyuşmazlık olabilir. Merhaba toplam birincil veri tüm birimlerde toohello toplamının hello birincil veri hello tek tek birimlerin ekleyemezsiniz. Bu son olabilir hello aşağıdaki tooone:

* **Tüm birimler için dahil edilen veri anlık görüntü**: yalnızca Sürüm güncelleştirme 3'ten önceki çalıştırıyorsanız bu davranış görülür. Tüm hello birimler için gösterilen hello birincil veri hello her birim için birincil veri hello ve hello anlık görüntü verilerini toplamıdır. belirli bir birim için gösterilen hello birincil veri tooonly hello hello birimde tahsis edilen veri miktarını karşılık gelir (ve hello karşılık gelen birim anlık görüntü verilerini dahil etmez).
  
    Bu ayrıca eşitlik aşağıdaki hello tarafından açıklanabilir:
  
    *Birincil veri (tüm birimler) = (birincil veri (birim i) + (birim i) anlık görüntü veri boyutu) toplamı*
  
    *WHERE, birincil veri (birim i) tahsis birincil veri toovolume boyutunu = t*
  
    Merhaba anlık görüntüleri hello hizmeti aracılığıyla sildiyseniz hello silme işlemini zaman uyumsuz olarak hello arka planda gerçekleştirilir. Merhaba toplu veri boyutu toobe hello anlık görüntü silme güncelleştirilmiş biraz zaman alabilir. 
  
    Güncelleştirme 3 veya sonraki sürümünü çalıştıran, hello anlık görüntü verilerini hello toplu veri bulunmaz. Ve hello birincil kullanımı aşağıdaki gibi hesaplanır:
  
    * Birincil veri (tüm birimler) = TOPLA (birincil veri (birim i)
  
    *WHERE, birincil veri (birim i) tahsis birincil veri toovolume boyutunu = t*
* **İzleme devre dışı olan birimler dahil tüm birimleri**: kendisi için izlemeyi devre dışı olduğundan, Cihazınızda birimleri varsa, izleme verilerini tek tek bu birimler için hello hello grafiklerde kullanılamaz. Ancak, hello veri hello grafikte tüm birimler için kendileri için izlemeyi devre dışı hello birimlerini içerir. 
* **Birimler dahil tüm birimler için Canlı ilişkili yedeklemelerinizi ile silinmiş**: anlık görüntü verilerini içeren birimler silinir, ancak ilişkili hello anlık görüntüleri hala mevcut durumunda bir uyuşmazlık görebilirsiniz.
* **Tüm birimler için dahil silinmiş**: Bu silinen olsa bile bazı durumlarda, eski birimlerin var olabilir. silme Hello etkisi değil görülen ve hello aygıt alt kullanılabilir kapasite gösterebilir. Bu birimler toocontact Microsoft Support tooremove gerekir.

Merhaba aşağıdaki grafikleri hello birincil depolama kapasitesi kullanımı önce StorSimple cihazını ve bulut anlık görüntü alındıktan sonra gösterir. Bir bulut anlık görüntü yalnızca birim verilerini olarak hello birincil depolama değiştirmemelisiniz. Gördüğünüz gibi bir bulut anlık sonucunda hello birincil kapasite kullanımı fark hello grafik gösterir. Merhaba bulut anlık görüntüsü yaklaşık 2:00 pm cihazdaki başlangıcı.

![Bulut anlık görüntüsü önce birincil kapasite kullanımı](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Bulut anlık görüntüsü sonra birincil kapasite kullanımı](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Çalıştırıyorsanız, güncelleştirme 2 veya üzeri, hello birincil depolama kapasitesi kullanımı bağımsız bir birim, tüm birimleri, tüm katmanlı birimlerin ve tüm yerel olarak sabitlenmiş birimleri tarafından aşağıda gösterildiği gibi ayırmak. Tüm tarafından yerel olarak sabitlenmiş birimlerin sağlayacak çiğnemekten tooquickly onaylaması hello yerel katmanı ne kadarının kullanılan.

![Tüm yerel olarak sabitlenmiş birimler için birincil kapasite kullanımı](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Bulut depolama kapasitesi kullanımı
Bu grafikler hello kullanılan bulut depolama alanı miktarını gösterir. Bu veri yinelenenleri kaldırılmış ve sıkıştırılmış. Bu miktar, tüm birincil biriminde yansıtılan değil ve gerekli veya eski bekletme amacıyla tutulur verileri içerebilen bulut anlık görüntüleri içerir. Merhaba numarası tam olmaz ancak hello birincil ve hello veri azaltma hakkında bir fikir oranı, bulut depolama tüketim rakamları tooget karşılaştırabilirsiniz. Merhaba aşağıdaki grafikleri hello bulut depolama kapasitesi kullanımı önce StorSimple cihazını ve bulut anlık görüntü alındıktan sonra gösterir. Merhaba bulut anlık görüntüsü yaklaşık 2:00 pm cihazdaki başlangıcı ve hello bulut kapasite kullanımı görüntüsü hello aynı görebilirsiniz 5,73 MB too4.04 GB ' artırma süresi.

![Bulut anlık görüntüsü önce bulut kapasite kullanımı](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Bulut anlık görüntüsü sonra bulut kapasite kullanımı](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Cihaz depolama kapasitesi kullanımı
Bu grafikler hello SSD doğrusal katmanı içerdiğinden olacağı birden çok birincil depolama alanı kullanımı hello cihaz için hello toplam kullanımını gösterir. Bu katman, bir cihazın diğer katmanları hello üzerinde mevcut da veri miktarı içerir. Yeni veri geldiğinde, hello eski verileri (aynı zamanda, yinelenenleri kaldırılmış sıkıştırılmış ve) taşınan toohello HDD katmanı ve daha sonra toohello bulut böylece hello kapasite hello SSD doğrusal katmanındaki geçiş sırasında.

Merhaba veri toobe başlatıncaya kadar zaman içinde birincil kapasite kullanımı ve cihaz kapasite kullanımı büyük olasılıkla birlikte artıracaktır katmanlı toohello bulut. Bu noktada, hello aygıt kapasite kullanımı büyük olasılıkla tooplateau başlar, ancak daha fazla veri yazıldığı hello birincil kapasite kullanımını artırır.

Merhaba aşağıdaki grafikleri hello birincil depolama kapasitesi kullanımı önce StorSimple cihazını ve bulut anlık görüntü alındıktan sonra gösterir. Merhaba bulut anlık görüntüsü 2: 00'da ve o anda azalan hello aygıt kapasite kullanımı başlandı. Merhaba cihaz depolama kapasitesi kullanımı 11.58 GB too7.48 GB ' kapandı. Bu büyük olasılıkla hello hello doğrusal SSD katmanına sıkıştırılmamış veri yinelenenleri kaldırılmış, sıkıştırılmış ve hello HDD katmanı taşındı gösterir. Merhaba aygıt büyük miktarda veri hello SSD ve HDD katmanları zaten varsa, bu azaltma göremeyebilirsiniz unutmayın. Bu örnekte, çok küçük miktarda veri hello aygıtın vardır.

![Bulut anlık görüntüsü önce aygıt kapasite kullanımı](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Bulut anlık görüntüsü sonra cihaz kapasite kullanımı](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Ağ verimliliği
**Ağ verimliliği** hello iSCSI başlatıcısı ağ arabirimlerinden hello ana bilgisayar sunucusu ve hello cihaz ve hello aygıt hello bulut arasında aktarılan parçaları ölçümleri ilgili toohello veri miktarını. Bu ölçüm, Cihazınızda her hello iSCSI ağ arabirimleri için izleyebilirsiniz.

grafikler Göster hello ağ verimliliği hello veri 0 ve veri 4, her iki 1 GbE ağ arabirimleri aygıtınızda aşağıdaki hello. Bu örnekte, veri 0 bulut-veri 4 iSCSI etkin iken etkinleştirildi. Gelen ve giden trafik StorSimple cihazınız için hello hem hello görebilirsiniz. Merhaba düz satır 3:24 pm başlayarak hello grafikte biz yalnızca her 5 dakikada bir veri toplamak ve yoksayılmalıdır toohello olgu owing. 

![Data4 için bir ağ verimliliği](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Data4 için bir ağ verimliliği](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Cihaz performansı
**Cihaz performans** parçaları ölçümleri Cihazınızı toohello performansını ilgili. Merhaba aşağıdaki grafikte bir aygıt için hello CPU kullanımı istatistiklerini üretimde gösterir.

![Cihaz için CPU kullanımı](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[hello StorSimple Yöneticisi hizmet cihaz Panosu kullanmak](storsimple-device-dashboard.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

