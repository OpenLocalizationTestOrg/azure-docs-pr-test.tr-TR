---
title: aaaRestore yedekten bir StorSimple biriminin | Microsoft Docs
description: "Nasıl toouse hello StorSimple Yöneticisi hizmeti yedekleme kataloğu sayfa toorestore bir StorSimple biriminin bir yedekleme kümesinden açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>Bir StorSimple biriminin bir yedekleme kümesi (güncelleştirme 2) geri yükleme
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Genel Bakış
Merhaba **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. Bu sayfa toolist kullanın ve yedeklemeleri yönetmek, bir yedekleme kümesinden geri yüklemek veya bir birim kopyalama.

 ![Yedekleme kataloğu sayfası](./media/storsimple-restore-from-backup-set-u2/restore.png)

Bu öğretici açıklar nasıl toouse hello **yedekleme kataloğu** toorestore bir yedekleme kümesi aygıtınızdan sayfa.

Yerel bir birimden veya Bulut yedeklemesini geri yükleyebilirsiniz. Her iki durumda da hemen veri hello arka planda yüklenirken hello geri yükleme işlemi hello birimini çevrimiçi getirir. 

## <a name="before-you-restore"></a>Geri yüklemeden önce
Bir geri yükleme işlemini başlatmadan önce uyarılar aşağıdaki hello bilmeniz gerekir:

* **Merhaba birim çevrimdışına** – hem hello konakta hello birim çevrimdışı gerçekleştirin ve hello geri yükleme işlemini başlatmadan önce aygıt hello. Merhaba geri yükleme işlemi, çevrimiçi hello birimi otomatik olarak hello aygıtta duruma getirir. rağmen el ile Merhaba cihaz çevrimiçi hello konakta getirmeniz gerekir. Merhaba birim hello aygıtta çevrimiçi olduğunda hello konakta hello birimini çevrimiçi kullanıma sunabilirsiniz. (Merhaba geri yükleme işlemi tamamlanana kadar toowait gerekmez.) Yordamlar için çok Git[bir birim çevrimdışına](storsimple-manage-volumes-u2.md#take-a-volume-offline).
* **Birim türü geri yükleme sonrasında** – silinen birimler geri yüklenir hello anlık görüntüdeki hello türüne göre. Yerel olarak sabitlenmiş birimleri yerel olarak sabitlenmiş birimleri olarak geri yüklenir ve katmanlı birimleri katmanlı birimler olarak geri yüklenir.
  
    Var olan birimler için hello geçerli kullanım türü hello birimin hello anlık depolanan hello türü geçersiz kılar. Örneğin, yerel olarak sabitlenmiş bir birim Hello birim geri sonra hello birim türü katmanlı yükleyen alındığı bir anlık görüntüden bir birime geri yüklerseniz ve birim türü artık yerel olarak olduğunu (tooa dönüştürme işlemi), sabitlenmiş. Var olan yerel olarak sabitlenmiş bir birim genişletilmiş ve daha sonra hello birim daha küçük olduğunda gerçekleştirilecek daha eski bir anlık görüntüden geri, benzer şekilde, hello geri yüklenen toplu hello geçerli genişletilmiş boyutu korur.
  
    Bir birim bir katmanlı birim yerel olarak sabitlenmiş tooa birimden dönüştürülemiyor veya _tam tersini_ hello birim geri yüklenirken. Merhaba geri yükleme işlemi tamamlandıktan ve daha sonra hello birim tooanother türü dönüştürebilirsiniz kadar bekleyin. Bir birim dönüştürme hakkında daha fazla bilgi için çok Git[değiştirmek hello birim türü](storsimple-manage-volumes-u2.md#change-the-volume-type). 
* **Merhaba birim boyutu geri hello biriminde yansıtılır** – (yerel olarak sabitlenmiş birimlerin tam olarak sağlandıktan nedeniyle), silinmiş olan yerel olarak sabitlenmiş bir birim geri yüklüyorsanız bu önemli bir konudur. Daha önce silinmiş yerel olarak sabitlenmiş bir birim toorestore denemeden önce yeterli alan olduğundan emin olun. 
* **Bu geri yüklenirken bir birim genişletilemiyor** – tooexpand hello birim çalışmadan önce hello geri yükleme işlemi tamamlanana kadar bekleyin. Bir birim genişletme hakkında daha fazla bilgi için çok Git[bir birim değiştirmek](storsimple-manage-volumes-u2.md#modify-a-volume).
* **Yerel bir birime geri yüklediğiniz sırada bir yedekleme gerçekleştirebilirsiniz** – için yordamlar çok gidin[hello StorSimple Yöneticisi hizmet toomanage yedekleme ilkelerini kullanma](storsimple-manage-backup-policies.md).
* **Bir geri yükleme işlemi iptal** – hello geri yükleme başlatılan önce içindeydi toohello durumunu hello birim geri sonra hello geri yükleme işi iptal ederseniz. Yordamlar için çok Git[bir işi iptal](storsimple-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Nasıl iş geri yükleme
Güncelleştirme 4 veya üstünü çalıştıran cihazlarda heatmap tabanlı geri yükleme uygulanır. Merhaba ana istekleri tooaccess verileri hello aygıt ulaşmak gibi bu istekleri izlenir ve bir heatmap oluşturulur. Alt istek hızı alt ısı ile toochunks çevirir ancak yüksek istek hızı veri öbekleri yüksek ısı ile sonuçlanır. Toobe olarak işaretli hello veri en az iki kez erişmesi gereken _etkin_. Değiştirilen bir dosya da olarak işaretlenmiş _etkin_. Merhaba geri yüklemesini başlatmak sonra veri öngörülü hidrasyonu hello heatmap göre gerçekleşir. Sürümleri için güncelleştirme 4'ten önceki hello veri erişimini kullanarak geri yükleme sırasında indirilen. 

Katmanlı birimlerin ve yerel olarak sabitlenmiş birimleri desteklenmez yalnızca Heatmap tabanlı izleme etkinleştirilir. Heatmap tabanlı geri yükleme, bir birim tooanother aygıtı kopyalarken de desteklenmez. (Veri zaten yerel olarak kullanılabilir olduğu gibi) bir yerinde geri yükleme ve hello aygıtta geri hello birim toobe için yerel bir anlık görüntü var, ardından biz rehydrate değil. Geri yüklendiğinde varsayılan olarak, önceden hello heatmap üzerinde göre verileri rehydrate hello rehydration işleri başlatılan. Güncelleştirme 4'te Windows PowerShell cmdlet'leri rehydration işleri çalıştırma kullanılan tooquery olması, rehydration işi iptal ve hello hello rehydration işinin durumunu al.

* `Get-HcsRehydrationJob`-Bu cmdlet hello hello rehydration işinin durumunu alır. Tek bir birim için bir tek rehydration işi tetiklenir.
* `Set-HcsRehydrationJob`-Bu cmdlet'i toopause sağlar, durdurmak, hello rehydration devam ederken hello rehydration işi devam ettirin. 

Rehydration cmdlet'leri hakkında daha fazla bilgi için çok Git[StorSimple için Windows PowerShell cmdlet başvurusu](https://technet.microsoft.com/library/dn688168.aspx).

Otomatik rehdyration ile genellikle yüksek geçici okuma performansı beklenir. Merhaba gerçek magniutde geliştirme erişim düzeni, veri dalgalanmasına ve veri türü gibi çeşitli etkenlere bağlıdır. toocancel rehydration işi, hello PowerShell cmdlet'ini kullanabilirsiniz. Tüm hello gelecekteki geri yüklemeler için toopermanently devre dışı bırakma rehydration işleri isterseniz, Microsoft Support başvurun.

## <a name="how-toouse-hello-backup-catalog"></a>Nasıl toouse hello yedekleme kataloğu
Merhaba **yedekleme kataloğu** sayfası, yedekleme kümesi seçiminiz toonarrow yardımcı olan bir sorgu sağlar. Şu parametreler hello üzerinde temel alınan hello yedekleme kümelerini filtreleyebilirsiniz:

* **Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.
* **Yedekleme İlkesi** veya **birim** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.
* **Gelen** ve **için** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.

Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:

* **Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.
* **Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.
* **Oluşturulan** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat. 
* **Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler. Bir yedekleme verilerinizin hello cihazda yerel olarak depolanan tüm birim yerel bir anlık görüntüdür. Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvurur. Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.
* **Tarafından başlatılan** – hello yedeklemeleri otomatik olarak tooa zamanlamaya göre başlatılabilir veya sizin tarafınızdan elle. (Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz. Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake etkileşimli bir yedek.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Nasıl toorestore, StorSimple birim bir yedekten
Merhaba kullanabilirsiniz **yedekleme kataloğu** toorestore StorSimple biriminiz belirli bir yedekten sayfa. Ancak unutmayın, bu bir birime geri hello yedeğin alındığı zamanki hello birim toohello durumu döner. Merhaba yedekleme işleminden sonra eklenen tüm veriler kaybolur.

> [!WARNING]
> Bir yedekten geri yükleme hello var olan birimler hello yedekten yerini alır. Bu hello hello yedeğin alındığı sonra yazıldı herhangi bir veri kaybına neden olabilir.
> 
> 

### <a name="toorestore-your-volume"></a>toorestore biriminiz
1. Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.
   
    ![Yedekleme kataloğu](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. Bir yedekleme kümesi aşağıdaki gibi seçin:
   
   1. Merhaba uygun cihazı seçin.
   2. Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.
   3. Merhaba zaman aralığı belirtin.
   4. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute bu sorgu.
      
      Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.
3. Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin. Geri yüklemeden önce bu birimleri hello ana bilgisayar ve aygıt çevrimdışına alınması gerekir. Erişim hello hello birimlerde **birim kapsayıcıları** sayfasında ve hello adımları izleyin [bir birim çevrimdışına](storsimple-manage-volumes-u2.md#take-a-volume-offline) tootake çevrimdışı.
   
   > [!IMPORTANT]
   > Merhaba aygıtta çevrimdışı hello birimleri olabilmesi hello birimlerde çevrimdışı hello konak ilk olarak, gerçekleştirdiğinizden emin olun. Merhaba konakta çevrimdışı hello birimleri almazsanız, büyük olasılıkla toodata bozulmasına yol açabilir.
   > 
   > 
4. Geri toohello gidin **yedekleme kataloğu** sekmesinde ve bir yedekleme kümesi seçin.
5. Tıklatın **geri** hello sayfanın hello sonundaki.
6. Onayınız istenir. Gözden geçirme hello bilgileri geri yüklemek ve hello onay onay kutusunu seçin.
   
    ![Onay sayfası](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. Merhaba onay simgesine ![onay simgesi](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png). Bir geri yükleme işi başlar. Merhaba erişerek hello iş görüntüleyebilirsiniz **işleri** sayfası. 
8. Merhaba geri yükleme tamamlandıktan sonra birimlerinizi Merhaba içeriğine hello yedekleme birimlerden değiştirilir olduğunu doğrulayabilirsiniz.

![Video var](./media/storsimple-restore-from-backup-set-u2/Video_icon.png) **Video var**

toowatch nasıl hello kopya kullanın ve geri yükleme StorSimple silinmiş toorecover dosyalarında özellikleri gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="if-hello-restore-fails"></a>Merhaba geri yükleme başarısız olur
Merhaba herhangi bir nedenden dolayı işlem başarısız geri yüklerseniz, bir uyarı alırsınız. Bu meydana gelirse, yedekleme hello yenileme hello yedekleme listesi tooverify hala geçerlidir. Ardından Hello yedeğinin geçerli olduğundan ve hello buluttan geri yüklüyorsanız, bağlantı sorunları hello soruna neden. 

toocomplete hello geri yükleme işlemi, çevrimdışı hello birim hello ana bilgisayarda gerçekleştirin ve hello geri yükleme işlemi yeniden deneyin. Merhaba geri yükleme işlemi sırasında gerçekleştirilen tüm değişiklikler toohello birim veriler kaybolur.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[yönetmek StorSimple birimlerini](storsimple-manage-volumes-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

