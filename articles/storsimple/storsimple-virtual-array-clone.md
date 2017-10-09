---
title: StorSimple sanal dizinin yedekleme aaaClone | Microsoft Docs
description: "Öğrenin nasıl tooclone bir yedekleme ve dosya, StorSimple sanal diziden kurtarın."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi yedekten kopyalama

## <a name="overview"></a>Genel Bakış

Bu makalede adım adım nasıl tooclone bir yedekleme, paylaşımlar veya birimler, Microsoft Azure StorSimple sanal dizisinde kümesi açıklanmaktadır. Merhaba kopyalanan kullanılan toorecover silinmiş veya kayıp dosya yedeğidir. Merhaba makale ayrıca bir öğe düzeyinde kurtarma, StorSimple sanal dizisindeki bir dosya sunucusu olarak yapılandırılmış ayrıntılı adımlar tooperform içerir.

## <a name="clone-shares-from-a-backup-set"></a>Bir yedekleme kümesinden kopya paylaşımları

**Tooclone paylaşımları denemeden önce bu işlem hello aygıt toocomplete yeterli alan olduğundan emin olun.** Merhaba, bir yedekten tooclone [Azure portal](https://portal.azure.com/), hello aşağıdaki adımları gerçekleştirin.

#### <a name="tooclone-a-share"></a>tooclone bir paylaşımı

1. Çok Gözat**aygıtları** dikey. Seçin ve aygıtınızı tıklatın ve ardından **paylaşımları**. Hello paylaşımı tooclone, sağ tıklatma hello paylaşımı tooinvoke hello bağlam menüsünde istediğinizi seçin. Seçin **kopya**.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. Merhaba, **kopya** dikey penceresinde tıklatın **yedekleme > seçin** ve ardından aşağıdaki hello: 
   
   a.    Bu aygıtta hello zaman aralığı tabanlı bir yedekleme filtreleyin. Aralarından seçim yapabileceğiniz **son 7 gün**, **son 30 gündeki**, ve **geçen yılda**.
   
   b.    Merhaba listesinde görüntülenen filtrelenmiş yedeklemeler, gelen bir yedekleme tooclone seçin.
   
   c.    **Tamam** düğmesine tıklayın.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. Merhaba, **kopya** dikey penceresinde tıklatın **hedef ayarları** ve ardından aşağıdaki hello:
   
   a.    Bir paylaşım adı belirtin. Merhaba paylaşım adı 3-127 karakter içermelidir.
   
   b.    İsteğe bağlı olarak hello kopyalanan paylaşımı için bir açıklama sağlayın.
   
   c.    Geri yüklediğiniz hello paylaşımının hello türünü değiştiremezsiniz. Katmanlı bir paylaşımı, bir katmanlı ve yerel olarak sabitlenmiş yerel olarak sabitlenmiş bir paylaşım olarak kopyalandı.
   
   d.    Merhaba kapasite kopyalama hello paylaşımının boyutuna eşit toohello olarak ayarlanır.
   
   e.    Bu paylaşım için Hello Yöneticiler atayın. Merhaba kopya tamamlandıktan sonra dosya Gezgini aracılığıyla mümkün toomodify hello paylaşım özellikleri olacaktır.
   
   f.    **Tamam** düğmesine tıklayın.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Tıklatın **kopya** toostart bir kopya işi. Merhaba işi tamamlandıktan sonra hello kopyalama işlemi başlatır ve size bildirilir. kopya, Git toohello toomonitor hello ilerlemesini **işleri** tıklayın ve dikey penceresinde hello iş tooview iş ayrıntıları.
5. Merhaba kopya başarıyla oluşturulduktan sonra geri toohello gidin **paylaşımları** Cihazınızı dikey penceresinde.
6. Şimdi Cihazınızda hello paylaşımlar listesinde hello yeni kopyalanan paylaşımı görüntüleyebilirsiniz. Katmanlı bir paylaşımı katmanlı gibi kopyalanan ve yerel olarak sabitlenmiş bir paylaşım olarak yerel olarak sabitlenmiş bir paylaşımı.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Bir yedekleme kümesi birimlerden kopyalama

tooclone hello Azure portal'ın bir yedekten bir paylaşımı kopyalarken tooperform adımları benzer toohello olanları sahip. Merhaba kopyalama işlemi klonlar hello yedekleme tooa yeni birimde hello aynı sanal aygıt; tooa farklı cihaz kopyalayamıyor.

#### <a name="tooclone-a-volume"></a>tooclone bir birim

1. Çok Gözat**aygıtları** dikey. Seçin ve aygıtınızı tıklatın ve ardından **birimleri**. Tooclone, istediğiniz Seç hello birimi hello birim tooinvoke hello bağlam menüsü sağ tıklatın. Seçin **kopya**.
   
   ![Bir birimi kopyalama](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. Merhaba, **kopya** dikey penceresinde tıklatın **yedekleme** ve ardından aşağıdaki hello: 
   
   a.    Bu aygıtta hello zaman aralığı tabanlı bir yedekleme filtreleyin. Aralarından seçim yapabileceğiniz **son 7 gün**, **son 30 gündeki**, ve **geçen yılda**. 
   
   b.    Merhaba listesinde görüntülenen filtrelenmiş yedeklemeler, gelen bir yedekleme tooclone seçin.
   
   c.    **Tamam** düğmesine tıklayın.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. Merhaba, **kopya** dikey penceresinde tıklatın **hedef birim ayarlarını** ve ardından aşağıdaki hello::
   
   a. Merhaba aygıt adı otomatik olarak doldurulur.
   
   b. Hello için bir birim ad **birim klonlanmış**. Merhaba birim adı 3 too127 karakter içermelidir.
   
   c. Merhaba birim türü toohello özgün birimin otomatik olarak ayarlanır. Katmanlı birim katmanlı olarak kopyalanabilen ve yerel olarak sabitlenmiş bir birim yerel olarak sabitlenmiş.
   
   d. Hello için **bağlı Konaklar**, tıklatın **seçin**.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. Merhaba, **bağlı Konaklar** dikey penceresinde, varolan bir ACR seçin veya yeni bir ACR ekleyin. Yeni bir ACR tooadd, tooprovide ACR adı ve hello konak IQN gerekir. **Seç**'e tıklayın.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Tıklatın **kopya** toolaunch bir kopya işi.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Merhaba kopya işi oluşturulduktan sonra kopyalama başlatılır. Merhaba kopya oluşturulduktan sonra aygıtınızda hello birimleri dikey penceresinde görüntülenir. Katmanlı birim katmanlı olarak kopyalanabilen ve yerel olarak sabitlenmiş bir birim yerel olarak sabitlenmiş bir birim klonlanmış unutmayın.
   
   ![Bir yedekleme kopyalama](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Merhaba birim birimlerin hello listesini çevrimiçi göründükten sonra hello birim kullanıma hazırdır. Merhaba iSCSI başlatıcısı konakta hedefleri iSCSI Başlatıcı Özellikleri penceresinde hello listesini yenileyin. Merhaba kopyalanan birim adını içeren yeni bir hedef 'hello durum sütununun altında devre dışı olarak' görüntülenmesi gerekir.
8. Hello hedefi seçin ve tıklatın **Bağlan**. Merhaba Başlatıcı bağlı toohello hedef sonra hello durumu çok değişmelidir**bağlı**.
9. Merhaba, **Disk Yönetimi** penceresinde hello takılan birimler görünür hello aşağıdaki çizimde gösterildiği gibi. Merhaba bulunan birime sağ tıklayın (Merhaba disk adına tıklayın) ve ardından **çevrimiçi**.

> [!IMPORTANT]
> Ne zaman hello kopyalama işi başarısız olursa bir birim veya bir yedekleme kümesi paylaşımından tooclone çalışırken, bir hedef birim veya paylaşım hala hello portalda oluşturulabilir. Bu hedef birimde silin veya bu öğesinden kaynaklanan gelecekteki sorunlar hello portal toominimize içinde paylaşmak önemlidir.
> 
> 

## <a name="item-level-recovery-ilr"></a>Öğe düzeyinde Kurtarma (ILR)

Bu sürüm, StorSimple sanal bir dosya sunucusu olarak yapılandırılmış dizisindeki hello öğe düzeyinde Kurtarma (ILR) sunar. Merhaba özelliği hello StorSimple cihazında tüm hello paylaşımlarının bulut yedekleme dosyaları ve klasörleri kurtarma ayrıntılı toodo sağlar. Silinen dosyaların bir Self Servis modelini kullanarak son yedeklerden geri alabilirsiniz.

Her paylaşımı var. bir *.backups* hello en son yedeklemeleri içeren klasör. Toohello istenen yedek gidin, ilgili dosyaları ve klasörleri hello yedekten kopyalayın ve bunları geri yükleyin. Bu özellik dosyaları yedeklerden geri yüklemek için çağrıları tooadministrators ortadan kaldırır.

1. Merhaba ILR gerçekleştirirken, dosya Gezgini üzerinden hello yedeklemeleri görüntüleyebilirsiniz. Merhaba yedekleme için en toolook istediğiniz hello belirli Paylaş'ı tıklatın. Göreceğiniz bir *.backups* tüm hello yedeklemeleri depolar hello paylaşımı altında oluşturulan klasör. Merhaba genişletin *.backups* klasörü tooview hello yedekler. Başlangıç klasörü hello ayrılmış hello tüm yedekleme hiyerarşi görünümünü gösterir. Bu görünüm, isteğe bağlı oluşturulur ve genellikle, yalnızca birkaç saniye toocreate alır.
   
   Merhaba son beş yedeklemeler bu şekilde görüntülenir ve kullanılan tooperform öğe düzeyinde kurtarma olabilir. Merhaba beş son yedeklemelerini her ikisi de dahil hello zamanlanmış varsayılan ve el ile yedekleme hello.
   
   * **Zamanlanmış yedeklemeler** olarak adlandırılan &lt;aygıt adı&gt;YYYYAAGG SSDDSS UTC DailySchedule.
   * **El ile Yedekleme** Ad-özel-YYYYAAGG-SSDDSS-UTC olarak adlı.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Silinen hello dosya Hello en son sürümünü içeren hello yedeği tanımlayın. Her durumda önceki hello UTC zaman damgası Hello klasör adı içeriyor olsa hangi hello klasörü oluşturuldu hello hello yedekleme başladığında hello gerçek cihaz süresi dır. Başlangıç klasörü zaman damgası toolocate kullanın ve hello yedeklemeleri tanımlayın.

3. Başlangıç klasörü veya hello önceki adımda belirlediğiniz hello yedekleme toorestore istediğiniz hello dosyasını bulun. Merhaba dosyaları veya izniniz klasörleri yalnızca görüntüleme unutmayın. Belirli dosyaları veya klasörleri erişemiyorsanız, bir paylaşım yöneticisine başvurun. Hello Yöneticisi, dosya Gezgini tooedit hello paylaşım izinlerini kullanın ve erişim toohello belirli dosya veya klasör verin. Bu paylaşım yönetici hello önerilen bir en iyi uygulama yerine tek bir kullanıcı bir kullanıcı grubu olmasıdır.

4. Hello dosya ya da hello klasörü toohello uygun paylaşım StorSimple dosya sunucunuzda kopyalayın.

## <a name="next-steps"></a>Sonraki adımlar

Hakkında daha fazla çok bilgi[StorSimple sanal hello yerel web kullanıcı arabirimini kullanarak dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

