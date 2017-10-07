---
title: "aaaStorSimple, sanal dizinin olağanüstü durum kurtarma ve aygıt yük devretme | Microsoft Docs"
description: "Hakkında daha fazla bilgi toofailover, StorSimple sanal dizi."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Olağanüstü durum kurtarma ve cihaz için yük devretme StorSimple sanal dizinizi Azure Portalı aracılığıyla

## <a name="overview"></a>Genel Bakış
Merhaba dahil olmak üzere Azure StorSimple sanal dizinin ayrıntılı Microsoft toofail tooanother sanal dizinin adımları için bu makalede hello olağanüstü durum kurtarma açıklanmaktadır. Bir yük devretme sayesinde toomove verilerinizden bir *kaynak* hello datacenter tooa aygıtı *hedef* aygıt. Merhaba hedef aygıt olabilir hello aynı veya farklı bir coğrafi konum bulunur. Merhaba aygıt yük devretme hello tüm cihaz için olduğunu. Yük devretme sırasında hello bulut verilerini hello kaynak cihaz için sahipliği toothat hello hedef aygıt değiştirir.

Bu makalede yalnızca sanal diziler geçerli tooStorSimple ' dir. 8000 serisi aygıt üzerinden toofail Git çok[aygıt yük devretme ve olağanüstü durum kurtarma StorSimple cihazınızın](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>Olağanüstü durum kurtarma ve aygıt yük devretme nedir?

Bir olağanüstü durum kurtarma (DR) senaryosunda hello birincil aygıt çalışmamaya başlar. Bu senaryoda, hello başarısız aygıt tooanother aygıtla ilişkilendirilen hello bulut verilerini taşıyabilirsiniz. Merhaba birincil cihaz hello kullanabilirsiniz *kaynak* ve başka bir aygıt hello belirtmek *hedef*. Bu bir işlemdir başvurulan tooas hello *yük devretme*. Yük devretme sırasında tüm birimleri hello veya hello paylaşımları hello kaynak aygıttan sahipliğini değiştirmek ve aktarılan toohello hedef aygıta. Hiçbir hello veri filtreleme izin verilir.

DR hello ısı Haritası tabanlı katmanlama ve izleme kullanarak bir cihazın tamamen geri yükleme modellenir. Isı Haritası bağlı verilerini okuma ve desenler yazma ısı değeri toohello atayarak tanımlanır. Bu ısı hello yerel katmanında hello (en kullanılan) yüksek ısı veri öbekleri tutarken ilk katmanları en düşük ısı veri öbekleri toohello bulut hello sonra eşleyin. Bir DR sırasında StorSimple hello ısı Haritası toorestore kullanır ve hello bulut hello verilerden rehydrate. Merhaba aygıt (dahili olarak belirlenen) tüm hello birimleri/paylaşımları hello son son yedekleme getirir ve o yedekten geri yükleme gerçekleştirir. Merhaba sanal dizinin hello tüm DR işlemini düzenler.

> [!IMPORTANT]
> Merhaba kaynak aygıt hello aygıt yük devretme sonunda silinir ve bu nedenle bir yeniden çalışma desteklenmez.
> 
> 

Olağanüstü durum kurtarma hello aygıt yük devretme özelliği düzenlenir ve hello başlatılan **aygıtları** dikey. Bu dikey tüm hello StorSimple cihazları bağlı tooyour StorSimple cihaz Yöneticisi hizmeti tablo haline getirir. Her cihaz için hello kolay ad, durumu, sağlanan ve maksimum kapasite, türünü ve model görebilirsiniz.

## <a name="prerequisites-for-device-failover"></a>Cihaz yük devretme için Önkoşullar

### <a name="prerequisites"></a>Ön koşullar

Cihaz yük devretme için Önkoşulları aşağıdaki o hello uyduğunuzdan emin olun:

* Hello kaynak aygıtın gerekiyor toobe içinde bir **devre dışı** durumu.
* Merhaba hedef aygıt tooshow yukarı olarak gereken **yukarı tooset hazır** hello Azure Portalı'nda. Merhaba hedef sanal dizisi sağlamak aynı veya daha yüksek kapasite. Merhaba yerel web kullanıcı Arabirimi tooconfigure kullanın ve başarıyla hello hedef sanal dizi kaydedin.
  
  > [!IMPORTANT]
  > Tooconfigure hello kayıtlı sanal aygıt hello hizmeti aracılığıyla çalışmayın. Hiçbir aygıt yapılandırması hello hizmeti aracılığıyla yapılmalıdır.
  > 
  > 
* Merhaba hedef aygıt aynı hello kaynak cihazı olarak ad hello sahip olamaz.
* Merhaba kaynak ve hedef cihaz sahip toobe hello aynı türde. Yalnızca bir dosya sunucusu tooanother dosya sunucusu olarak yapılandırılmış sanal bir dizi üzerinden başarısız olabilir. Merhaba aynı iSCSI sunucusu için geçerlidir.
* Bir dosya sunucusu DR için hello hedef aygıt toohello katılma olan öneririz hello kaynak aynı etki alanında. Bu yapılandırma hello paylaşım izinleri otomatik olarak çözümlenmiş olmasını sağlar. Yalnızca hello yük devretme tooa hedef aygıt hello aynı etki alanı.
* Merhaba kullanılabilir hedef DR için olan aygıtları aynı hello veya büyük kapasite toohello kaynak aygıt karşılaştırıldığında aygıtlardır. Merhaba bağlı tooyour cihazlar hizmet ancak hello karşılamayan ölçütleri yeterli alan hedef cihazlar olarak kullanılabilir değildir.

### <a name="other-considerations"></a>Diğer konular

* Planlanmış bir yük devretme için 
  
  * Çevrimdışı hello kaynak cihazda tüm hello birimler veya paylaşımlar almanızı öneririz.
  * Merhaba aygıt yedekleyin ve hello yük devretme toominimize veri kaybı ile devam öneririz. 
* Planlanmamış yük devretme için hello aygıt hello en son yedekleme toorestore hello verileri kullanır.

### <a name="device-failover-prechecks"></a>Cihaz yük devretme prechecks

Hello DR başlamadan önce hello aygıt prechecks gerçekleştirir. Bu denetimler, DR başladığı zaman hata oluşmamasına sağlamaya yardımcı olur. Merhaba prechecks şunları içerir:

* Merhaba depolama hesabı doğrulanıyor.
* Merhaba bulut bağlantı tooAzure denetleniyor.
* Merhaba hedef aygıttaki kullanılabilir alanı denetleniyor.
* Bir iSCSI sunucu kaynak aygıt birim olup olmadığı denetleniyor
  
  * Geçerli ACR adları.
  * Geçerli IQN (220 karakteri aşan değil).
  * Geçerli CHAP parolalar (12-16 karakter uzunluğunda).

Prechecks önceki hello hiçbirini başarısız olursa, DR hello ile devam edemiyor. Bu sorunları çözün ve sonra kurtarma işlemini yeniden deneyin.

Merhaba DR başarıyla tamamlandıktan sonra hello bulut verilerinin hello kaynak aygıtta hello sahipliğini aktarılan toohello hedef aygıttır. Merhaba kaynak cihaz sonra artık hello Portalı'nda kullanılamıyor. Erişim tooall hello birimleri/paylaşımlarında hello kaynak cihaz engellenir ve hello hedef aygıt etkin hale gelir.

> [!IMPORTANT]
> Merhaba aygıt artık kullanılabilir olsa da, hello ana bilgisayar sisteminde sağlanan hello sanal makine hala kaynakları tüketilmesine neden olabilir. Merhaba DR başarıyla tamamlandıktan sonra bu sanal makine ana bilgisayar sisteminizden silebilirsiniz.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Tooa sanal dizinin başarısız

Sağlamak, yapılandırmak ve bu yordamı çalıştırmadan önce başka bir StorSimple sanal dizinin, StorSimple cihaz Yöneticisi Hizmeti'ne kaydedin öneririz.

> [!IMPORTANT]
> 
> * Üzerinden bir StorSimple 8000 serisi aygıt tooa 1200 sanal aygıttan kapatamazsınız.
> * Federal Bilgi İşleme Standardı (etkin FIPS) sanal aygıt tooanother etkin FIPS aygıt veya hello kamu Portalı'nda dağıtılan tooa FIPS olmayan cihazı üzerinden edilemeyebilir.


Aşağıdaki adımları toorestore hello aygıt tooa hedef StorSimple sanal cihazı hello gerçekleştirin.

1. Sağlamak ve hello karşılayan bir hedef cihaz yapılandırma [aygıt yük devretme için Önkoşullar](#prerequisites). Merhaba yerel web kullanıcı Arabirimi aracılığıyla Hello aygıt yapılandırmasını tamamlamak ve tooyour StorSimple cihaz Yöneticisi Hizmeti'ne kaydedin. Bir dosya sunucusu oluşturuyorsanız, 1 toostep Git [dosya sunucusu olarak ayarlanmış](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Bir iSCSI sunucusu oluşturuyorsanız, toostep 1, Git [iSCSI sunucusu olarak ayarlanmış](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Birimleri/paylaşımları çevrimdışı hello ana bilgisayarda gerçekleştirin. tootake hello birimleri/paylaşımları çevrimdışı hello konağını toohello işletim sistemi – özel yönergeler bakın. Zaten çevrimdışı, tootake tüm hello birimleri/paylaşımlarında çevrimdışı hello aygıt hello aşağıdakileri yaparak gerekir.
   
    1. Çok Git**aygıtları** dikey ve Cihazınızı seçin.
   
    2. Çok Git**ayarlar > Yönet > paylaşımları** (veya **ayarlar > Yönet > birimleri**). 
   
    3. Bir paylaşım/birimi seçin, sağ tıklatın ve seçin **çevrimdışına**. 
   
    4. Onayınız istendiğinde denetleyin **bu paylaşım çevrimdışı duruma getirmeden hello etkisi anlıyorum.** 
   
    5. Tıklatın **çevrimdışına**.

3. StorSimple cihaz Yöneticisi hizmetinize çok Git**Yönetim > aygıtları**. Merhaba, **aygıtları** dikey penceresinde, seçin ve kaynak aygıtınızı tıklatın.

4. İçinde **cihaz Pano** dikey penceresinde tıklatın **etkinliğini**.

5. Merhaba, **etkinliğini** dikey penceresinde onaylamanız istenir. Aygıt devre dışı bırakma olan bir *kalıcı* işlem geri alınamaz. Ayrıca tootake görüntülenerek, paylaşımları/çevrimdışı hello konaktaki birimlerdir. Merhaba aygıt adı tooconfirm yazıp tıklatın **etkinliğini**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. Merhaba devre dışı bırakma işlemini başlatır. Merhaba devre dışı bırakma işlemi başarıyla tamamlandıktan sonra bir bildirim alırsınız.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Merhaba cihazlar sayfasında hello cihaz durumu şimdi çok değiştireceksiniz**devre dışı**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. Merhaba, **aygıtları** yük devretme için hello devre dışı bırakılmış kaynak aygıt dikey penceresinde, seçin ve'ı tıklatın. 
9. Merhaba, **cihaz Pano** dikey penceresinde tıklatın **yük devri**. 
10. Merhaba, **aygıt üzerinden başarısız** dikey penceresinde, aşağıdaki hello:
    
    1. Merhaba kaynak aygıt alanı otomatik olarak doldurulur. Merhaba toplam veri boyutuna hello kaynak aygıtın dikkat edin. Merhaba veri boyutu hello hedef aygıttaki hello kullanılabilir kapasitesinden daha az olmalıdır. Aygıt adı, toplam kapasite ve yük devredildi hello paylaşımları hello adları gibi hello kaynak aygıtla ilişkili hello ayrıntılarını gözden geçirin.

    2. Merhaba açılır listesinden kullanılabilir aygıtları seçin bir **hedef aygıt**. Yalnızca yeterli kapasiteye sahip hello cihazların Merhaba açılır listede görüntülenir.

    3. Denetleyin **veri toohello hedef aygıt bu işlemi başarısız olur anlıyorum**. 

    4. Tıklatın **yük devri**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Bir yük devretme iş başlatır ve bir bildirim alırsınız. Çok Git**cihazlar > işleri** toomonitor hello yük devretme.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. Merhaba, **işleri** dikey penceresinde hello kaynak cihaz için oluşturulan bir yük devretme işine bakın. Bu iş hello DR prechecks gerçekleştirir.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Merhaba DR prechecks başarılı olduktan sonra hello yük devretme işine kaynak Cihazınızda var. her paylaşım/birim için geri yükleme işleri oluşturma.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Tam, Git toohello Hello yük devretme tamamlandıktan sonra **aygıtları** dikey.
    
    1. Seçin ve hello yük devretme işlemi için hello hedef cihaz olarak kullanılan hello StorSimple cihazı tıklayın.
    2. Çok Git**ayarlar > Yönetim > paylaşımları** (veya **birimleri** , iSCSI sunucusu). Merhaba, **paylaşımları** dikey penceresinde tüm hello paylaşımlarını (birimler) hello eski aygıttan görüntüleyebilirsiniz.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. Çok gerekir[bir DNS diğer adı oluşturma](https://support.microsoft.com/kb/168322) böylece tüm çalışan uygulamalar hello tooconnect yeniden yönlendirilen toohello yeni cihaz elde edebilirsiniz.

## <a name="errors-during-dr"></a>DR sırasında hatalar

**DR sırasında bulut bağlantı kesintisi**

Merhaba bulut bağlantı sonra kesintiye uğrarsa DR başlatıldı ve hello DR hello aygıt geri yükleme tamamlanmadan önce başarısız olur. Failore bildirim alırsınız. Dr Hello hedef aygıt olarak işaretli *kullanılamaz.* Merhaba kullanamazsınız aynı hedef cihaz gelecekteki DRs için.

**Uyumlu hedef cihaz yok**

Merhaba kullanılabilir hedef aygıtlara yeterli alan yoksa hata toohello efekt uyumlu hedef aygıt yok bakın.

**Precheck hataları**

Merhaba prechecks birini memnun değil, precheck hataları konusuna bakın.

## <a name="business-continuity-disaster-recovery-bcdr"></a>İş sürekliliği olağanüstü durum kurtarma (BCDR)

Bir iş sürekliliği olağanüstü durum kurtarma (BCDR) senaryosu Hello tüm Azure veri merkezi çalışmıyor oluşur. Bu, StorSimple cihaz Yöneticisi hizmetiniz etkileyebilir ve StorSimple cihazlar hello ilişkili.

Yalnızca bir olağanüstü durum oluşmadan önce kaydedilen StorSimple cihazlar varsa, bu StorSimple cihazlar silinmiş toobe gerekebilir. Merhaba olağanüstü durum sonra yeniden oluşturun ve bu aygıtların yapılandırın.

## <a name="next-steps"></a>Sonraki adımlar

Hakkında daha fazla çok bilgi[StorSimple sanal hello yerel web kullanıcı arabirimini kullanarak dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

