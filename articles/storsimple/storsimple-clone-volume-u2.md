---
title: StorSimple 8000 serisi birim aaaClone | Microsoft Docs
description: "Merhaba farklı kopya türlerini açıklar ve ne zaman toouse bunları ve bir yedekleme kümesi tooclone bağımsız bir birim nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Merhaba StorSimple Yöneticisi hizmet tooclone (güncelleştirme 2) birim kullanın
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.

![Yedekleme kataloğu sayfası](./media/storsimple-clone-volume-u2/backupCatalog.png)  

Bu öğretici, bir yedekleme kümesi tooclone bağımsız bir birim nasıl kullanabileceğinizi açıklar. Ayrıca hello birbirinden açıklar *geçici* ve *kalıcı* klonlar.

> [!NOTE]
> Yerel olarak sabitlenmiş bir birim katmanlı birim kopyalanma. Yerel olarak sabitlenmiş kopyalanan birim toobe hello varsa, başlangıç kopyalama işlemi başarıyla tamamlandıktan sonra hello kopya tooa yerel olarak sabitlenmiş birim dönüştürebilirsiniz. Çok katmanlı birim tooa yerel olarak dönüştürme hakkında bilgi sabitlenmiş birim için Git[değiştirmek hello birim türü](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> (Bunu yine bir geçici kopya olduğunda) hemen kopyalandıktan sonra katmanlı toolocally kopyalanan bir birimden sabitlenmiş tooconvert deneyin hello dönüştürme hello aşağıdaki hata iletisi ile başarısız olur:
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Yalnızca tooa farklı cihazda kopyalama, bu hata alınır. Merhaba geçici kopya tooa kalıcı kopya ilk dönüştürürseniz sabitlenmiş hello birim toolocally başarıyla dönüştürebilirsiniz. tooconvert hello geçici kopya tooa kalıcı kopyalama, bunu bir bulut anlık görüntüsünü alın.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Bir birimin bir kopyasını oluşturun
Kopya oluşturma hello aynı aygıt, başka bir aygıt veya sanal makine bir yerel kullanarak veya Bulut anlık görüntü.

#### <a name="tooclone-a-volume"></a>tooclone bir birim
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesinde ve bir yedekleme kümesi seçin.
2. Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin. ' I tıklatın ve hello yedekleme kümesinden bir birim seçin.
   
     ![Bir birimi kopyalama](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Tıklatın **kopya** toobegin seçili hello birim kopyalama.
4. Merhaba kopya Birim Sihirbazı'nda altında **ad ve konum belirtin**:
   
   1. Bir hedef cihaz tanımlayın. Bu hello kopya oluşturulacağı hello konumdur. Merhaba aynı cihaz veya başka bir aygıt belirtmek seçebilirsiniz. Diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim seçerseniz (değil Azure), hello açılan hello hedef aygıt yalnızca fiziksel cihazlarını göstermeyecektir için liste. Bir sanal cihazdaki diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim kopyalayamıyor.
      
      > [!NOTE]
      > Merhaba kopyalama için gereken hello kapasite hello hedef cihazda kullanılabilir hello kapasitesinden daha düşük olduğundan emin olun.
      > 
      > 
   2. Kopya için benzersiz birim adı belirtin. Merhaba ad 3 ile 127 karakter içermelidir. 
      
      > [!NOTE]
      > Merhaba **kopya birim olarak** alan **katmanlı** yerel olarak sabitlenmiş bir birim kopyalama olsa bile. Bu ayarı değiştiremezsiniz; Bununla birlikte, kopyalanan birim toobe de yerel olarak sabitlenmiş hello varsa, hello kopya başarıyla oluşturduktan sonra hello kopya tooa yerel olarak sabitlenmiş birim dönüştürebilirsiniz. Çok katmanlı birim tooa yerel olarak dönüştürme hakkında bilgi sabitlenmiş birim için Git[değiştirmek hello birim türü](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Kopya Sihirbazı 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello sonraki sayfa.
5. Altında **bu birimi kullanabilir ana bilgisayarları belirleyin**:
   
   1. Merhaba kopya için bir erişim denetimi kaydı (ACR) belirtin. Yeni bir ACR ekleyebilir veya hello varolan listeden seçin.
      
        ![Kopyalama Sihirbazı'nı 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)toocomplete hello işlemi.
6. Bir kopya iş başlatılır ve hello kopya başarıyla oluşturulduğunda size bildirilecek. Tıklatın **işi görüntüle** toomonitor hello kopya hello işinde **işleri** sayfası. Merhaba kopya işi bittiğinde iletiden hello görürsünüz:
   
    ![Kopya iletisi](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Merhaba sonra kopyalama işi tamamlanır:
   
   1. Toohello Git **aygıtları** sayfası ve select hello **birim kapsayıcıları** sekmesi. 
   2. Kopyaladığınız hello kaynak birimi ile ilişkili hello birim kapsayıcısı seçin. Birimleri Hello listesinde, yeni oluşturduğunuz hello kopya görmeniz gerekir.

> [!NOTE]
> İzleme ve varsayılan yedekleme otomatik olarak kopyalanan bir birimde devre dışı.
> 
> 

Bu yolla oluşturulan bir kopya geçici kopya ' dir. Kopya türleri hakkında daha fazla bilgi için bkz: [geçici ve kalıcı klonlar](#transient-vs-permanent-clones).

Bu kopya artık normal bir birim ve bir birimde mümkündür herhangi bir işlem hello kopya için kullanılabilir olacak. Bu birimi tooconfigure tüm yedeklemeler için gerekir.

## <a name="transient-vs-permanent-clones"></a>Geçici ve kalıcı klonlar karşılaştırması
Yalnızca tooa farklı cihaz kopyalarken geçici klonlar oluşturulur. Merhaba StorSimple Yöneticisi tarafından yönetilen bir yedekleme kümesi tooa farklı bir cihaz belirli bir birimden kopyalayabilirsiniz. Merhaba geçici kopya hello özgün birimin başvuruları toohello verilere sahip ve bu verileri tooread kullanıyor ve yerel olarak hello hedef aygıtta yazma. 

Bir geçici kopya bir bulut anlık görüntüsünü sonra hello elde edilen kopya olacak bir *kalıcı* kopya. Bu işlem sırasında hello verilerin bir kopyasını hello Bulutu üzerinde oluşturulur ve bu verileri hello veri hello boyutu tarafından belirlenir zaman toocopy hello ve (bir Azure Azure kopyalama budur) Azure gecikmeleri hello. Bu işlem gün tooweeks alabilir. Merhaba geçici kopya kalıcı bir kopya bu şekilde haline gelir ve gelen kopyalandı tüm başvuruları toohello özgün birimin verileri yok. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Geçici ve kalıcı klonlar senaryoları
Aşağıdaki bölümlerde hello geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.

### <a name="item-level-recovery-with-a-transient-clone"></a>Geçici bir kopya ile öğe düzeyinde kurtarma
Toorecover bir yıl eski Microsoft PowerPoint sunusu dosyası gerekir. BT yöneticiniz hello belirli o zaman çerçevesi yedekten tanımlar ve ardından birim filtreleri hello. Hello Yöneticisi sonra hello birim klonlar, aradığınız hello dosyayı bulur ve tooyou sağlar. Bu senaryoda, bir geçici kopya kullanılır. 

![Video var](./media/storsimple-clone-volume-u2/Video_icon.png) **Video var**

toowatch nasıl hello kopya kullanın ve geri yükleme StorSimple silinmiş toorecover dosyalarında özellikleri gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Kalıcı bir kopya ile Merhaba üretim ortamında test etme
Tooverify hello üretim ortamında test hata gerekir. Merhaba üretim ortamında hello birimin bir kopyasını oluşturun ve sonra bu kopya toocreate bağımsız kopyalanan birimin bir bulut anlık görüntüsünü. Bu senaryoda, kalıcı bir kopya kullanılır.  

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-restore-from-backup-set-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

