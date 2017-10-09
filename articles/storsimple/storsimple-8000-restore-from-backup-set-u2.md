---
title: aaaRestore StorSimple 8000 serisi yedekleme birimden | Microsoft Docs
description: "Nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti yedekleme kataloğu toorestore bir StorSimple biriminin bir yedekleme kümesinden açıklanmaktadır."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Bir yedeklemek kümesinden StorSimple birimini geri

## <a name="overview"></a>Genel Bakış

Bu öğretici, var olan bir yedekleme kümesi kullanarak bir StorSimple 8000 serisi cihazda gerçekleştirilen hello geri yükleme işlemi açıklanmaktadır. Kullanım hello **yedekleme kataloğu** dikey toorestore yerel bir birimden veya Bulut yedekleme. Merhaba **yedekleme kataloğu** dikey penceresinde el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler. hemen veri hello arka planda yüklenirken hello birimini çevrimiçi bir yedekleme kümesi geri yükleme işleminin hello getirir.

Bir Alternatif yöntem toostart geri yükleme toogo çok.**cihazlar > [Cihazınızı] > birimleri**. Merhaba, **birimleri** dikey penceresinde sağ tıklatma tooinvoke hello bağlam menüsünde bir birim seçin ve ardından **geri**.

## <a name="before-you-restore"></a>Geri yüklemeden önce

Bir geri yükleme başlamadan önce uyarılar aşağıdaki hello gözden geçirin:

* **Merhaba birim çevrimdışı duruma** – hem hello konakta hello birim çevrimdışı gerçekleştirin ve hello geri yükleme işlemini başlatmadan önce aygıt hello. Merhaba geri yükleme işlemi, çevrimiçi hello birimi otomatik olarak hello aygıtta duruma getirir. rağmen el ile Merhaba cihaz çevrimiçi hello konakta getirmeniz gerekir. Merhaba hello aygıtta çevrimiçi birimdir hemen hello konakta hello birimini çevrimiçi kullanıma sunabilirsiniz. (Merhaba geri yükleme işlemi tamamlanana kadar toowait gerekmez.) Yordamlar için çok Git[bir birim çevrimdışına](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **Birim türü geri yükleme sonrasında** – silinen birimler geri yüklenir hello anlık görüntüdeki hello türüne göre; diğer bir deyişle, yerel olarak sabitlenmiş birimleri yerel olarak sabitlenmiş birimleri olarak geri yüklenir ve katmanlı birimleri katmanlı birimler olarak geri yüklenir.

    Var olan birimler için hello geçerli kullanım türü hello birimin hello anlık depolanan hello türü geçersiz kılar. Örneğin, bir birimi hello birim türü katmanlı yükleyen alındığı bir anlık görüntüden geri ve birim türü artık yerel olarak değil, sabitlenmiş (gerçekleştirilen tooa dönüştürme işlemi), ardından hello birim yerel olarak sabitlenmiş bir birim geri yüklenir. Var olan yerel olarak sabitlenmiş bir birim genişletilmiş ve daha sonra hello birim daha küçük olduğunda gerçekleştirilecek daha eski bir anlık görüntüden geri, benzer şekilde, hello geri yüklenen toplu hello geçerli genişletilmiş boyutu korur.

    Bir birim bir katmanlı birim yerel olarak sabitlenmiş tooa birimden dönüştürülemiyor veya hello birim geri yüklenirken bir yerel olarak sabitlenmiş birim tooa birimi katmanlı. Merhaba geri yükleme işlemi tamamlandıktan ve daha sonra hello birim tooanother türü dönüştürebilirsiniz kadar bekleyin. Bir birim dönüştürme hakkında daha fazla bilgi için çok Git[değiştirmek hello birim türü](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **Merhaba birim boyutu geri hello biriminde yansıtılır** – (yerel olarak sabitlenmiş birimlerin tam olarak sağlandıktan nedeniyle), silinmiş olan yerel olarak sabitlenmiş bir birim geri yüklüyorsanız bu önemli bir konudur. Daha önce silinmiş yerel olarak sabitlenmiş bir birim toorestore denemeden önce yeterli alan olduğundan emin olun.

* **Bu geri yüklenirken bir birim genişletilemiyor** – tooexpand hello birim çalışmadan önce hello geri yükleme işlemi tamamlanana kadar bekleyin. Bir birim genişletme hakkında daha fazla bilgi için çok Git[bir birim değiştirmek](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **Yerel bir birime geri yükleme sırasında bir yedekleme gerçekleştirebilirsiniz** – için yordamlar çok gidin[hello StorSimple cihaz Yöneticisi hizmeti toomanage yedekleme ilkelerini kullanma](storsimple-8000-manage-backup-policies-u2.md).

* **Bir geri yükleme işlemi iptal** – hello birim hello geri yükleme işlemi başlattı önce içindeydi toohello durumunu geri alınacak sonra hello geri yükleme işi iptal ederseniz. Yordamlar için çok Git[bir işi iptal](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Nasıl iş geri yükleme

Güncelleştirme 4 veya üstünü çalıştıran cihazlarda heatmap tabanlı geri yükleme uygulanır. Merhaba ana istekleri tooaccess verileri hello aygıt ulaşmak gibi bu istekleri izlenir ve bir heatmap oluşturulur. Alt istek hızı alt ısı ile toochunks çevirir ancak yüksek istek hızı veri öbekleri yüksek ısı ile sonuçlanır. Toobe olarak işaretli hello veri en az iki kez erişmesi gereken _etkin_. Değiştirilen bir dosya da olarak işaretlenmiş _etkin_. Merhaba geri yüklemesini başlatmak sonra veri öngörülü hidrasyonu hello heatmap göre gerçekleşir. Sürümleri için yalnızca erişimini kullanarak geri yükleme sırasında hello veri güncelleştirme 4'ten önceki indirilir.

Uyarılar aşağıdaki hello tooheatmap tabanlı geri yüklemeler Uygula:

* Heatmap izleme yalnızca katmanlı birimler için etkindir ve yerel olarak sabitlenmiş birimlerin desteklenmez.

* Bir birim tooanother aygıtı kopyalarken Heatmap tabanlı geri yükleme desteklenmez. 

* (Veri zaten yerel olarak kullanılabilir olduğu gibi) bir yerinde geri yükleme ve hello aygıtta geri hello birim toobe için yerel bir anlık görüntü var, ardından biz rehydrate değil. 

* Geri yüklendiğinde varsayılan olarak, önceden hello heatmap üzerinde göre verileri rehydrate hello rehydration işleri başlatılan. 

Güncelleştirme 4'te Windows PowerShell cmdlet'leri rehydration işleri çalıştırma kullanılan tooquery olması, rehydration işi iptal ve hello hello rehydration işinin durumunu al.

* `Get-HcsRehydrationJob`-Bu cmdlet hello hello rehydration işinin durumunu alır. Tek bir birim için bir tek rehydration işi tetiklenir.

* `Set-HcsRehydrationJob`-Bu cmdlet'i toopause sağlar, durdurmak, hello rehydration devam ederken hello rehydration işi devam ettirin.

Rehydration cmdlet'leri hakkında daha fazla bilgi için çok Git[StorSimple için Windows PowerShell cmdlet başvurusu](https://technet.microsoft.com/library/dn688168.aspx).

Otomatik rehdyration ile genellikle yüksek geçici okuma performansı beklenir. Merhaba gerçek magniutde geliştirme erişim düzeni, veri dalgalanmasına ve veri türü gibi çeşitli etkenlere bağlıdır. 

toocancel rehydration işi, hello PowerShell cmdlet'ini kullanabilirsiniz. Tüm gelecekteki geri yüklemeler hello için toopermanently devre dışı bırakma rehydration işleri istiyorsanız [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>Nasıl toouse hello yedekleme kataloğu

Merhaba **yedekleme kataloğu** dikey yedekleme kümesi seçiminiz toonarrow yardımcı olan bir sorgu sağlar. Şu parametreler hello üzerinde temel alınan hello yedekleme kümelerini filtreleyebilirsiniz:

* **Zaman aralığı** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.
* **Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.
* **Yedekleme İlkesi** veya **birim** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.

Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:

* **Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.
* **Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler. Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir. Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.
* **Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.
* **Oluşturulan** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat. 
* **Birimleri** -hello hello yedekleme kümesiyle ilişkili birimlerin sayısı.
* **Başlatılan** – hello yedeklemeleri otomatik olarak tooa zamanlamaya göre başlatılabilir veya bir kullanıcı tarafından el ile. (Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz. Alternatif olarak, hello kullanabilirsiniz **yedek alın** etkileşimli veya isteğe bağlı bir yedekleme seçeneği tootake.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Nasıl toorestore, StorSimple birim bir yedekten

Merhaba kullanabilirsiniz **yedekleme kataloğu** dikey toorestore StorSimple biriminiz belirli bir yedekten. Ancak bu bir birim döner geri hello yedeğin alındığı zamanki hello birim toohello durumu unutmayın. Merhaba yedekleme işleminden sonra eklenen tüm veriler kaybolacak.

> [!WARNING]
> Bir yedekten geri yükleme hello var olan birimler hello yedekten yerini alır. Bu hello hello yedeğin alındığı sonra yazıldı herhangi bir veri kaybına neden olabilir.


### <a name="toorestore-your-volume"></a>toorestore biriminiz
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **yedekleme kataloğu**.

2. Bir yedekleme kümesi aşağıdaki gibi seçin:
   
   1. Merhaba zaman aralığı belirtin.
   2. Merhaba uygun cihazı seçin.
   3. Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.
   4. Tıklatın **Uygula** tooexecute bu sorgu.

    Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.
   
    ![Yedekleme kümesi listesi](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin. Geri yüklemeden önce bu birimleri hello ana bilgisayar ve aygıt çevrimdışına alınması gerekir. Erişim hello hello birimlerde **birimleri** dikey cihaz ve ardından izleme hello adımları [bir birim çevrimdışına](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake çevrimdışı.
   
   > [!IMPORTANT]
   > Merhaba aygıtta çevrimdışı hello birimleri olabilmesi hello birimlerde çevrimdışı hello konak ilk olarak, gerçekleştirdiğinizden emin olun. Merhaba konakta çevrimdışı hello birimleri almazsanız, büyük olasılıkla toodata bozulmasına yol açabilir.
   
4. Geri toohello gidin **yedekleme kataloğu** sekmesinde ve bir yedekleme kümesi seçin. Sağ tıklayın ve ardından hello bağlam menüsünden seçin **geri**.

    ![Yedekleme kümesi listesi](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. Onayınız istenir. Gözden geçirme hello bilgileri geri yüklemek ve hello onay onay kutusunu seçin.
   
    ![Onay sayfası](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Tıklatın **geri**. Bu hello erişerek görüntüleyebileceğiniz bir geri yükleme işi başlattığı **işleri** sayfası.

    ![Onay sayfası](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Merhaba geri yükleme tamamlandıktan sonra birimlerinizi Merhaba içeriğine hello yedekleme birimlerden değiştirilir olduğunu doğrulayın.


## <a name="if-hello-restore-fails"></a>Merhaba geri yükleme başarısız olur

Merhaba herhangi bir nedenden dolayı işlem başarısız geri yüklerseniz, bir uyarı alırsınız. Bu meydana gelirse, yedekleme hello yenileme hello yedekleme listesi tooverify hala geçerlidir. Ardından Hello yedeğinin geçerli olduğundan ve hello buluttan geri yüklüyorsanız, bağlantı sorunları hello soruna neden.

toocomplete hello geri yükleme işlemi, çevrimdışı hello birim hello ana bilgisayarda gerçekleştirin ve hello geri yükleme işlemi yeniden deneyin. Geri yükleme işlemi sırasında hello gerçekleştirilen tüm değişiklikler toohello birim verilerini Not kaybolur.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[yönetmek StorSimple birimlerini](storsimple-8000-manage-volumes-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

