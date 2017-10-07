---
title: StorSimple 8000 serisi bir birimde aaaClone | Microsoft Docs
description: "Merhaba farklı kopya türleri ve kullanım ve bir yedekleme kümesi tooclone bağımsız bir birim bir StorSimple 8000 serisi cihazda nasıl kullanabileceğiniz açıklanmaktadır."
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Azure portal tooclone bir birim Hello StorSimple cihaz Yöneticisi hizmetini kullanma

## <a name="overview"></a>Genel Bakış

Bu öğretici bir yedekleme kümesi tooclone hello aracılığıyla tek bir birim nasıl kullanabileceğinizi açıklar **yedekleme kataloğu** dikey. Ayrıca hello birbirinden açıklar *geçici* ve *kalıcı* klonlar. Bu öğreticide Hello yönerge güncelleştirme 3 veya üstünü çalıştıran tooall hello StorSimple 8000 serisi aygıt geçerlidir.

Merhaba StorSimple cihaz Yöneticisi hizmeti **yedekleme kataloğu** dikey penceresinde el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Ardından, bir birim bir yedekleme kümesi tooclone seçebilirsiniz.

 ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Bir birim kopyalama dikkat edilmesi gereken noktalar

Bir birim kopyalarken aşağıdaki bilgilerle hello göz önünde bulundurun.

- Bir kopya hello aynı şekilde davranır normal bir birim olarak yolu. Bir birimde mümkündür herhangi bir işlem hello kopya için kullanılabilir.

- İzleme ve varsayılan yedekleme otomatik olarak kopyalanan bir birimde devre dışı. Tüm yedeklemeler için tooconfigure kopyalanan birim gerekir.

- Yerel olarak sabitlenmiş bir birim katmanlı birim kopyalandı. Yerel olarak sabitlenmiş kopyalanan birim toobe hello varsa, başlangıç kopyalama işlemi başarıyla tamamlandıktan sonra hello kopya tooa yerel olarak sabitlenmiş birim dönüştürebilirsiniz. Çok katmanlı birim tooa yerel olarak dönüştürme hakkında bilgi sabitlenmiş birim için Git[değiştirmek hello birim türü](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- (Bunu yine bir geçici kopya olduğunda) hemen kopyalandıktan sonra katmanlı toolocally kopyalanan bir birimden sabitlenmiş tooconvert deneyin hello dönüştürme hello aşağıdaki hata iletisi ile başarısız olur:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Yalnızca tooa farklı cihazda kopyalama, bu hata alınır. Merhaba geçici kopya tooa kalıcı kopya ilk dönüştürürseniz sabitlenmiş hello birim toolocally başarıyla dönüştürebilirsiniz. Merhaba geçici kopya tooconvert bir bulut anlık görüntüsünü, tooa kalıcı kopya.

## <a name="create-a-clone-of-a-volume"></a>Bir birimin bir kopyasını oluşturun

Kopya oluşturma hello aynı aygıt, başka bir aygıt veya Bulut uygulaması yerel kullanarak veya Bulut anlık görüntü.

Aşağıdaki Hello yordamı nasıl toocreate hello bir kopya yedekleme kataloğu açıklar.  Alternatif yöntem tooinitiate kopya toogo çok uzun**birimleri**bir birim seçin, sonra tooinvoke hello bağlam menüsü sağ tıklatın ve seçin **kopya**.

Merhaba yedekleme Kataloğu'ndan adımları toocreate biriminiz kopyasını aşağıdaki hello gerçekleştirin.

#### <a name="tooclone-a-volume"></a>tooclone bir birim

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **yedekleme kataloğu**.

2. Bir yedekleme kümesi aşağıdaki gibi seçin:
   
   1. Merhaba uygun cihazı seçin.
   2. Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.
   3. Merhaba zaman aralığı belirtin.
   4. Tıklatın **Uygula** tooexecute bu sorgu.

    Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.
   
    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin. Geri yüklemeden önce bu birimleri hello ana bilgisayar ve aygıt çevrimdışına alınması gerekir. Erişim hello hello birimlerde **birimleri** dikey cihaz ve ardından izleme hello adımları [bir birim çevrimdışına](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake çevrimdışı.
   
   > [!IMPORTANT]
   > Merhaba aygıtta çevrimdışı hello birimleri olabilmesi hello birimlerde çevrimdışı hello konak ilk olarak, gerçekleştirdiğinizden emin olun. Merhaba konakta çevrimdışı hello birimleri almazsanız, büyük olasılıkla toodata bozulmasına yol açabilir.
   
4. Geri toohello gidin **yedekleme kataloğu** ve yedekleme kümesinde bir birim seçin. Sağ tıklayın ve ardından hello bağlam menüsünden seçin **kopya**.

   ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. Merhaba, **kopya** dikey penceresinde, adımları hello:
   
    1. Bir hedef cihaz tanımlayın. Bu hello kopya oluşturulacağı hello konumdur. Merhaba aynı cihaz veya başka bir aygıt belirtmek seçebilirsiniz.

      > [!NOTE]
      > Merhaba kopyalama için gereken hello kapasite hello hedef cihazda kullanılabilir hello kapasitesinden daha düşük olduğundan emin olun.
       
    2. Kopya için benzersiz birim adı belirtin. Merhaba ad 3 ile 127 karakter içermelidir.
      
        > [!NOTE]
        > Merhaba **kopya birim olarak** alan **katmanlı** yerel olarak sabitlenmiş bir birim kopyalama olsa bile. Bu ayarı değiştiremezsiniz; Bununla birlikte, kopyalanan birim toobe de yerel olarak sabitlenmiş hello varsa, hello kopya başarıyla oluşturduktan sonra hello kopya tooa yerel olarak sabitlenmiş birim dönüştürebilirsiniz. Çok katmanlı birim tooa yerel olarak dönüştürme hakkında bilgi sabitlenmiş birim için Git[değiştirmek hello birim türü](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. Altında **bağlı Konaklar**, hello kopya için bir erişim denetimi kaydı (ACR) belirtin. Yeni bir ACR ekleyebilir veya hello varolan listeden seçin. Merhaba ACR hangi ana bilgisayarların bu kopya erişebilirsiniz belirler.
      
        ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Tıklatın **kopya** toocomplete hello işlemi.

4. Bir kopya iş başlatılır ve hello kopya başarıyla oluşturulduğunda size bildirilir. Merhaba iş bildirimi tıklatın ya da çok Git**işleri** dikey toomonitor hello kopyalama işi.

    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Merhaba kopya işi tamamlandıktan sonra tooyour aygıt gidin ve ardından **birimleri**. Birimleri Hello listesinde hello aynı az önce oluşturulan hello kopya görmelisiniz hello kaynak biriminin birim kapsayıcısı.

    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Bu yolla oluşturulan bir kopya geçici kopya ' dir. Kopya türleri hakkında daha fazla bilgi için bkz: [geçici ve kalıcı klonlar](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Geçici ve kalıcı klonlar karşılaştırması
Yalnızca tooanother aygıt kopyaladığınızda geçici klonlar oluşturulur. Merhaba StorSimple cihaz Yöneticisi tarafından yönetilen bir yedekleme kümesi tooa farklı bir cihaz belirli bir birimden kopyalayabilirsiniz. Merhaba geçici kopya hello özgün birimin başvuruları toohello veri vardır ve bu verileri tooread ve yazma hello hedef cihazda yerel olarak kullanır.

Bir geçici kopya bir bulut anlık görüntüsünü sonra hello elde edilen kopya olan bir *kalıcı* kopya. Bu işlem sırasında hello verilerin bir kopyasını hello Bulutu üzerinde oluşturulur ve bu verileri hello veri hello boyutu tarafından belirlenir zaman toocopy hello ve (bir Azure Azure kopyalama budur) Azure gecikmeleri hello. Bu işlem gün tooweeks alabilir. Merhaba geçici kopya kalıcı bir kopya olur ve gelen kopyalandı tüm başvuruları toohello özgün birimin verileri yok.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Geçici ve kalıcı klonlar senaryoları
Aşağıdaki bölümlerde hello geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.

### <a name="item-level-recovery-with-a-transient-clone"></a>Geçici bir kopya ile öğe düzeyinde kurtarma
Toorecover bir yıl eski Microsoft PowerPoint sunusu dosyası gerekir. BT yöneticiniz hello belirli saat yedekten tanımlar ve ardından birim filtreleri hello. Hello Yöneticisi sonra hello birim klonlar, aradığınız hello dosyayı bulur ve tooyou sağlar. Bu senaryoda, bir geçici kopya kullanılır.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Kalıcı bir kopya ile Merhaba üretim ortamında test etme
Tooverify hello üretim ortamında test hata gerekir. Merhaba üretim ortamında hello birimin bir kopyasını oluşturun ve sonra bu kopya toocreate bağımsız kopyalanan birimin bir bulut anlık görüntüsünü. Bu senaryoda, kalıcı bir kopya kullanılır.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-8000-restore-from-backup-set-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

