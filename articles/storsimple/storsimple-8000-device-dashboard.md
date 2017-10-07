---
title: "aaaUse StorSimple 8000 serisi aygıt Özet | Microsoft Docs"
description: "Merhaba StorSimple cihaz Yöneticisi Hizmeti aygıt Özet açıklar ve nasıl toouse, tooview storage ölçümleri ve bağlı başlatıcıları ve Bul hello seri numarasını ve IQN."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Merhaba cihaz StorSimple Aygıt Yöneticisi'ni hizmetinde Özet kullanın

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple cihaz Özet dikey bilgi belirli bir StorSimple cihazı için genel bir bakış sunar, buna karşılık toohello servis Özet dikey, Microsoft Azure StorSimple çözümünüzde dahil tüm hello cihazlar hakkında bilgi verir.

Merhaba aygıt Özet dikey pencere, sistem yöneticisinin dikkat etmeniz gereken bu cihaz sorunları vurgulayan ile belirli bir StorSimple Aygıt Yöneticisi, kayıtlı bir StorSimple 8000 serisi aygıt Özet görünümünü sağlar. Bu öğretici hello aygıt Özet dikey tanıtır, hello içerik ve işlevi açıklanmaktadır ve bu dikey pencereden gerçekleştirebileceğiniz hello görevleri açıklar.

Merhaba aygıt Özet dikey penceresinde aşağıdaki bilgilerle hello görüntüler:

![Cihaz Özet dikey penceresi](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Yönetim Komut çubuğu

Merhaba StorSimple cihaz dikey penceresinde hello seçenekleri StorSimple Cihazınızı yönetmek için bkz. Merhaba üstte hello dikey ve hello sol tarafında hello yönetimi komutları bakın. Bu seçenekler tooadd paylaşımları veya birimler kullanmak, güncelleştirme veya Cihazınızı başarısız.

![Yönetim Komut çubuğu](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Temel Bileşenler

Merhaba essentials alanı bazı hello önemli özellikler gibi hello durumu, model, hedef IQN ve hello yazılım sürümü yakalar. 

![Cihaz temelleri](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>İzleme

* Merhaba **uyarıları** kutucuğu uyarı önem derecesine göre gruplandırılmış cihazınız için bir anlık görüntüsünü tüm hello etkin uyarıları sağlar.

    ![Uyarı döşeme](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Merhaba döşeme tooopen hello tıklatın **uyarıları** dikey ve ardından tek bir uyarı tooview ek herhangi dahil olmak üzere Bu uyarıyla ilgili ayrıntılar önerilen eylemler. Merhaba sorunu çözerseniz hello uyarı işaretini kaldırabilirsiniz.

    ![Uyarı kutucuğa tıklayın](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Merhaba **durumunu** kutucuğu hello Aygıt durumu da dahil olmak üzere bir aygıt için hello donanım bileşen durumu fikir sağlar. Merhaba Aygıt durumu yukarı çevrimdışı, çevrimiçi, devre dışı bırakılmış veya hazır tooset olabilir.

    ![Durum ve sistem durumu kutucuğu](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Merhaba **birimleri** kutucuğu duruma göre gruplanmış Cihazınızı birimlerinde hello sayısı özetini sağlar.

    ![Birimler kutucuğunu](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Merhaba döşeme tooopen hello tıklatın **birimleri** listesi dikey penceresinde, bir tek tek birim tooview'ı tıklatın veya özelliklerini değiştirin.
    
    ![Birimler kutucuğunu tıklatın](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Daha fazla bilgi için bkz. nasıl çok[birimleri yönetme](storsimple-8000-manage-volumes-u2.md).

* Merhaba, **kullanım** grafiği, cihaz ve son 7 gün, hello varsayılan süre hello tüketilen hello bulut depolama kullanılan hello birincil depolama görüntüleyebilirsiniz.

     ![Kullanımı kutucuğu](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose farklı zaman ölçeği kullanmak hello **Düzenle** hello grafik hello sağ üst köşedeki seçeneği.

     ![Kullanım grafiği Düzenle](./media/storsimple-8000-device-dashboard/device-summary12.png)

     Bu grafikte görüntülemek hello toplam birincil depolama (ana bilgisayar tooyour aygıt tarafından yazılan veri miktarı hello) için Ölçümler ve toplam hello bulut bir süre boyunca cihazınız tarafından tüketilen depolama.
  
     Bu bağlamda *birincil depolama* toohello toplam hello ana bilgisayar tarafından yazılan veri miktarını gösterir ve birim türüne göre ayrılabilir: *birincil katmanlı depolama* her ikisini de içeren yerel olarak depolanan verileri ve verileri Katmanlı toohello bulut. *Birincil yerel olarak sabitlenmiş depolama* yerel olarak depolanan yalnızca verileri içerir. *Bulut depolama*, üzerinde diğer yandan Merhaba, hello toplam hello bulutta depolanan veri miktarını ölçüsüdür. Bu depolama katmanlı veri ve yedeklemeler içerir. Hello bulutta depolanan hello veri yinelenenleri kaldırılmış ve sıkıştırılmış ancak birincil depolama hello hello veri yinelenenleri kaldırılmış ve sıkıştırılmış önce kullanılan depolama alanı miktarını gösterir. (Bu iki sayının tooget hello sıkıştırma oranı hakkında bir fikir karşılaştırabilirsiniz.) Hem birincil hem de için ve bulut depolama, gösterilen tutarlar yapılandırdığınız sıklığı izleme hello üzerinde dayalı hello. Bir hafta sıklığı seçerseniz, örneğin, daha sonra hello grafik veri her günü için hello önceki hafta gösterir.

     toosee hello süre, select hello tüketilen bulut depolama alanı miktarını **bulut depolama kullanılan** seçeneği. select hello hello konak tarafından yazılmış toosee hello toplam depolama **birincil KATMANLI depolama kullanılan** ve **birincil yerel olarak SABİTLENMİŞ depolama kullanılan** seçenekleri. 
     Daha fazla bilgi için bkz: [kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti toomonitor hello](storsimple-monitor-device.md).


* Merhaba **kapasite** sağlanmış döşeme görüntüler hello birincil depolama ve hello aygıt göreli toohello toplam depolama alanı için kullanılabilir arasında kalan hello aynı. **Sağlanan** toohello hazırlanmış ve kullanım için ayrılan depolama alanı miktarını başvuruyor **kalan** bu cihaz sağlanan kapasite kalan toohello başvuruyor. 

    ![Kullanımı kutucuğu](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Merhaba kapasite katmanlı ve yerel olarak sabitlenmiş birimleri arasında nasıl sağlandığında bu kutucuğu tooview'ı tıklatın. Merhaba **kalan katmanlı** kapasitesi ise hello sırasında bulut dahil olmak üzere sağlanabilir hello kullanılabilir kapasite **kalan yerel** hello disklerde kalan hello kapasitesi toothis aygıt eklenmiş.

    ![Kullanım grafiği tıklatın](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Sonraki adımlar
* Merhaba hakkında daha fazla bilgi [StorSimple hizmeti Özet dikey](storsimple-8000-service-dashboard.md).
* Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).

