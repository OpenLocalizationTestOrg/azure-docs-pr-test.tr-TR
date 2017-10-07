---
title: aaaClone StorSimple biriminiz | Microsoft Docs
description: "Merhaba farklı kopya türlerini açıklar ve ne zaman toouse bunları ve bir yedekleme kümesi tooclone bağımsız bir birim nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a>Merhaba StorSimple Yöneticisi hizmet tooclone bir birim kullanın
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.

![Yedekleme kataloğu sayfası](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

Bu öğretici, bir yedekleme kümesi tooclone bağımsız bir birim nasıl kullanabileceğinizi açıklar. Ayrıca hello birbirinden açıklar *geçici* ve *kalıcı* klonlar. 

## <a name="create-a-clone-of-a-volume"></a>Bir birimin bir kopyasını oluşturun
Kopya üzerinde hello oluşturma aynı aygıt, başka bir aygıt veya hatta bir sanal yerel ya da bir bulut anlık görüntüsü kullanarak makine.

#### <a name="tooclone-a-volume"></a>tooclone bir birim
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesinde ve bir yedekleme kümesi seçin.
2. Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin. ' I tıklatın ve hello yedekleme kümesinden bir birim seçin.
   
     ![Bir birimi kopyalama](./media/storsimple-clone-volume/HCS_Clone.png) 
3. Tıklatın **kopya** toobegin seçili hello birim kopyalama.
4. Merhaba kopya Birim Sihirbazı'nda altında **ad ve konum belirtin**:
   
   1. Bir hedef cihaz tanımlayın. Bu hello kopya oluşturulacağı hello konumdur. Merhaba aynı cihaz veya başka bir aygıt belirtmek seçebilirsiniz. Diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim seçerseniz (değil Azure), hello açılan hello hedef aygıt yalnızca fiziksel cihazlarını göstermeyecektir için liste. Bir sanal cihazdaki diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim kopyalayamıyor.
      
      > [!NOTE]
      > Merhaba kopyalama için gereken hello kapasite hello hedef cihazda kullanılabilir hello kapasitesinden daha düşük olduğundan emin olun.
      > 
      > 
   2. Kopya için benzersiz birim adı belirtin. Merhaba ad 3 ile 127 karakter içermelidir.
   3. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-clone-volume/HCS_ArrowIcon.png) tooproceed toohello sonraki sayfa.
5. Altında **bu birimi kullanabilir ana bilgisayarları belirleyin**:
   
   1. Merhaba kopya için bir erişim denetimi kaydı (ACR) belirtin. Yeni bir ACR ekleyebilir veya hello varolan listeden seçin.
   2. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-clone-volume/HCS_CheckIcon.png)toocomplete hello işlemi.
6. Bir kopya iş başlatılır ve hello kopya başarıyla oluşturulduğunda size bildirilecek. Tıklatın **işi görüntüle** toomonitor hello kopya hello işinde **işleri** sayfası.
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
Yalnızca tooa farklı aygıtta kopyalarken geçici ve kalıcı klonlar oluşturulur. Yedekleme kümesi tooa farklı bir cihaz belirli bir birimden kopyalayabilirsiniz. Bu yolla oluşturulan bir kopya olduğundan bir *geçici* kopya. Merhaba geçici kopya başvuruları toohello özgün birimin sahip olur ve bu birimi tooread yerel olarak yazılırken kullanır. 

Bir geçici kopya bir bulut anlık görüntüsünü sonra hello elde edilen kopya olacak bir *kalıcı* kopya. Merhaba kalıcı kopya bağımsızdır ve gelen kopyalandı tüm başvuruları toohello özgün birim yok.  

## <a name="scenarios-for-transient-and-permanent-clones"></a>Geçici ve kalıcı klonlar senaryoları
Aşağıdaki bölümlerde hello geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.

### <a name="item-level-recovery-with-a-transient-clone"></a>Geçici bir kopya ile öğe düzeyinde kurtarma
Toorecover bir yıl eski Microsoft PowerPoint sunusu dosyası gerekir. BT yöneticiniz hello belirli o zaman çerçevesi yedekten tanımlar ve ardından birim filtreleri hello. Hello Yöneticisi sonra hello birim klonlar, aradığınız hello dosyayı bulur ve tooyou sağlar. Bu senaryoda, bir geçici kopya kullanılır. 

![Video var](./media/storsimple-clone-volume/Video_icon.png) **Video var**

toowatch nasıl hello kopya kullanın ve geri yükleme StorSimple silinmiş toorecover dosyalarında özellikleri gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Kalıcı bir kopya ile Merhaba üretim ortamında test etme
Tooverify hello üretim ortamında test hata gerekir. Bir bulut bu kopya anlık görüntüsü tarafından hello üretim ortamında hello birimin bir kopyasını oluşturun. Merhaba kopyalanan birim artık bağımsızdır. Bu senaryoda, kalıcı bir kopya kullanılır.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-restore-from-backup-set.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

