---
title: "aaaStorSimple yük devretme ve olağanüstü durum kurtarma | Microsoft Docs"
description: "Bilgi nasıl StorSimple cihaz tooitself, başka bir fiziksel aygıt ya da sanal cihazı üzerinden toofail."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>StorSimple cihazınız için yük devretme ve olağanüstü durum kurtarma
## <a name="overview"></a>Genel Bakış
Bu öğretici, bir olağanüstü durum hello olayı içinde StorSimple cihazı üzerinden hello adımları gerekli toofail açıklar. Bir yük devretme toomigrate sağlayacak. aynı veya farklı bir coğrafi konum hello datacenter tooanother fiziksel bir kaynak aygıt ya da sanal bir cihaz verilerinizden hello bulunur. 

Olağanüstü Durum Kurtarma (DR) hello aygıt yük devretme özelliği düzenlenir ve hello başlatılan **aygıtları** sayfası. Bu sayfayı tüm hello StorSimple cihazları bağlı tooyour StorSimple Yöneticisi hizmeti tablo haline getirir. Her cihaz, hello kolay adını, durumunu, sağlanan ve maksimum kapasite için türünü ve model görüntülenir.

![Cihazlar sayfası](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

Bu öğreticide Hello yönerge tooStorSimple fiziksel ve sanal aygıtların tüm yazılım sürümleri arasında geçerlidir.

## <a name="disaster-recovery-dr-and-device-failover"></a>Olağanüstü Durum Kurtarma (DR) ve aygıtı yük devretme
Bir olağanüstü durum kurtarma (DR) senaryosunda hello birincil aygıt çalışmamaya başlar. Bu durumda, hello birincil cihaz hello kullanarak hello başarısız aygıt tooanother aygıtla ilişkilendirilen hello bulut verilerini taşıyabilirsiniz *kaynak* ve başka bir aygıt hello belirterek *hedef*. Bir veya daha fazla birim kapsayıcıları toomigrate toohello hedef aygıt seçebilirsiniz. Bu bir işlemdir başvurulan tooas hello *yük devretme*. 

Hello yük devretme sırasında hello kaynak aygıttan hello birim kapsayıcıları sahipliği değiştirir ve aktarılan toohello hedef aygıta. Merhaba birim kapsayıcıları sahipliği değiştirdiğinizde, bu hello kaynak aygıttan silinir. Merhaba silme işlemi tamamlandıktan sonra hello hedef aygıt sonra geri çalışılabilir.

Genellikle aşağıdaki DR, hello en son yedeklemenin kullanılan toorestore hello veri toohello hedef aygıttır. Ancak, varsa aynı birim için birden çok yedekleme ilkeleri Merhaba, ardından hello yedekleme İlkesi hello en büyük birim sayısı ile çekilen ve hello en son yedeklemeden bu ilkeyi hello hedef aygıttaki kullanılan toorestore hello verileri.

Örneğin iki yedekleme ilkeleri (varsayılan ve bir özel) varsa, *defaultPol*, *customPol* aşağıdaki ayrıntılara hello ile:

* *defaultPol* : tek bir birim *vol1*, günlük 10: 30'pm başlangıç çalıştırır.
* *customPol* : dört birim *vol1*, *vol2*, *vol3*, *vol4*, günlük 10: 00'dan başlayarak çalıştırır.

Bu durumda, *customPol* daha fazla birim varsa ve biz kilitlenme tutarlılığı için öncelik olarak kullanılır. Bu ilke en son yedeklemeden Hello kullanılan toorestore verilerdir.

## <a name="considerations-for-device-failover"></a>Cihaz yük devretme için ilgili önemli noktalar
Bir olağanüstü durum Hello olayda StorSimple Cihazınızı toofail tercih edebilirsiniz:

* tooa fiziksel cihaz 
* tooitself
* tooa sanal cihaz

Tüm aygıt yük devretme için hello aşağıdakileri göz önünde bulundurun:

* Merhaba DR için Önkoşullar hello birim kapsayıcıları içindeki tüm hello birimleri çevrimdışı ve hello birim kapsayıcıları ilişkili bir sahip olan bulut anlık görüntüsü. 
* Merhaba kullanılabilir hedef DR için yeterli alanı tooaccommodate Seçili birim kapsayıcıları hello cihazları aygıtlardır. 
* Merhaba bağlı tooyour cihazlar hizmet ancak yeterli hello ölçütleri karşılamayan alanı hedef cihazlar olarak kullanılabilir olmaz.
* Sınırlı bir süre için bir DR aşağıdaki hello veri erişim performansını önemli ölçüde etkilenebilir, hello cihazı olarak tooaccess hello bulut verilerden hello ve yerel olarak depolamak.

#### <a name="device-failover-across-software-versions"></a>Cihaz yük devretme yazılım sürümleri arasında
Bir StorSimple Yöneticisi hizmeti bir dağıtımda birden çok aygıt, fiziksel ve sanal tüm çalışan farklı yazılım sürümleri olabilir. Hello yazılımın sürümüne bağlı olarak, hello cihazlarda hello birim türleri de farklı olabilir. Güncelleştirme 2 veya daha yüksek yerel olarak sabitlenmiş ve katmanlı birimlerin örneği için bir aygıt çalışan (ile arşivleme bir alt kümesi olan katmanlı). Bir güncelleştirme öncesi 2 cihaz üzerinde hello diğer yandan katmanlı ve arşivleme birimler. 

DR sırasında birim türlerinin farklı yazılım sürümü ve hello davranışını çalıştıran tooanother cihaz devredebildiğini tablo toodetermine izlemeyi hello kullanın.

| Gelen yük devri | Fiziksel cihaz için izin verilen | Sanal cihaz için izin verilen |
| --- | --- | --- |
| Güncelleştirme 2 toopre-Update 1 (sürüm, 0.1, 0.2, 0.3) |Hayır |Hayır |
| Güncelleştirme 2 tooUpdate 1 (1, 1.1, 1.2) |Evet <br></br>Yerel olarak sabitlenmiş kullanarak veya birimleri katmanlı veya birimleri her zaman olarak yük devredildi iki hello karışımını katmanlı. |Evet<br></br>Kullanarak yerel olarak sabitlenmiş birimler varsa, bunlar üzerinde katmanlı olarak başarısız. |
| Güncelleştirme 2 tooUpdate 2 (sonraki bir sürümünü) |Evet<br></br>Yerel olarak sabitlenmiş veya katmanlı birim veya iki bir karışımını kullanıyorsanız, hello birimleri her zaman birim türü başlangıç hello yük devredildi; Katmanlı ve yerel olarak sabitlenmiş olarak yerel olarak sabitlenmiş katmanlı. |Evet<br></br>Kullanarak yerel olarak sabitlenmiş birimler varsa, bunlar üzerinde katmanlı olarak başarısız. |

#### <a name="partial-failover-across-software-versions"></a>Yazılım sürümleri arasında kısmi yük devretme
Güncelleştirme öncesi 1 tooa hedef güncelleştirme 1 veya sonrasını çalıştırıyor çalıştıran bir StorSimple kaynak aygıtı kullanarak kısmi bir yük devretme tooperform düşünüyorsanız, bu yönergeleri izleyin. 

| Kısmi bir yük devretme işlemini | Fiziksel cihaz için izin verilen | Sanal cihaz için izin verilen |
| --- | --- | --- |
| 1 (sürüm, 0.1, 0.2, 0.3) güncelleştirme öncesi tooUpdate 1 veya sonraki sürümler |Evet, aşağıda hello en iyi yöntem ipucu için bkz. |Evet, aşağıda hello en iyi yöntem ipucu için bkz. |

> [!TIP]
> Güncelleştirme 1 ve sonraki sürümlerde bulut meta verileri ve veri biçimi değişikliği oluştu. Bu nedenle, kısmi bir yük devretme işlemini güncelleştirme öncesi 1 tooUpdate 1 veya sonraki sürümler önermiyoruz. Tooperform kısmi bir yük devretme gerekiyorsa, ilk önce Güncelleştirme 1 veya daha sonra hem hello aygıtları (kaynak ve hedef) uygulayın ve hello yük devretme kümelemesiyle devam öneririz. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>Tooanother fiziksel aygıt üzerinden başarısız
Aşağıdaki adımları toorestore hello aygıt tooa hedef fiziksel cihazınız gerçekleştirin.

1. Bu hello birim kapsayıcısı üzerinde toofail istediğiniz bulut anlık görüntüleri ilişkili doğrulayın.
2. Merhaba üzerinde **aygıtları** hello sayfasında, **birim kapsayıcıları** sekmesi.
3. Tooanother aygıt üzerinden toofail istediğiniz bir birim kapsayıcısı seçin. Merhaba birim kapsayıcı toodisplay hello birimlerin listesini bu kapsayıcıdaki'ı tıklatın. Bir birim seçin ve tıklatın **Çevrimdışına Al** tootake hello çevrimdışı birim. Merhaba birim kapsayıcısındaki tüm hello birimleri için bu işlemi yineleyin.
4. Önceki adımı yineleyin hello tüm birim kapsayıcıları hello için tooanother aygıt üzerinden toofail istersiniz.
5. Merhaba üzerinde **aygıtları** sayfasında, **yük devretme**.
6. Altında açılır hello Sihirbazı'nda **üzerinden birim kapsayıcı toofail seçin**:
   
   1. Birim kapsayıcıları Hello listesinde toofail üzerinden istediğiniz hello birim kapsayıcıları seçin.
      **Yalnızca ilişkili bulut anlık görüntüleri ile birim kapsayıcıları hello ve çevrimdışı birimler görüntülenir.**
   2. Altında **hedef aygıt seçin** seçili hello kapsayıcılarında hello birimler için hedef aygıtta hello aşağı açılan listesinden kullanılabilir aygıtları seçin. Merhaba kullanılabilir kapasiteye sahip hello aygıtlar hello aşağı açılan listede görüntülenir.
   3. Son olarak, tüm hello yük devretme ayarlarda gözden **yük devretme onaylayın**. Merhaba onay simgesine ![onay simgesi](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Bir yük devretme iş oluşturulur hello izlenebilir **işleri** sayfası. Ardından üzerinden başarısız hello birim kapsayıcısı yerel birim varsa, tek tek geri yükleme işleri hello kapsayıcıdaki her yerel birimi (değil için katmanlı birimleri) görürsünüz. Bu geri yükleme işleri oldukça bazı zaman toocomplete sürebilir. Bu hello yük devretme işine önceki tamamlanabilir olasıdır. Yalnızca hello geri yükleme işi tamamlandıktan sonra bu birimler yerel GARANTİLERİN sahip gerektiğini unutmayın. Merhaba yük devretme tamamlandıktan sonra toohello Git **aygıtları** sayfası.                                            
   
   1. Merhaba yük devretme işlemi için hello hedef cihaz olarak kullanılan hello cihazı seçin.
   2. Toohello Git **birim kapsayıcıları** sayfası. Merhaba birimleri hello eski aygıttan yanı sıra tüm hello birim kapsayıcıları listelenmelidir.

## <a name="failover-using-a-single-device"></a>Tek bir cihazı kullanarak yük devretme
Merhaba bir yük devretme yalnızca tek bir cihaz ve gerek tooperform varsa, aşağıdaki adımları gerçekleştirin.

1. Tüm hello birimleri bulut anlık görüntülerini kullanarak Cihazınızı alın.
2. Cihaz toofactory Varsayılanları sıfırlayın. İzleyin hello ayrıntılı yönergeleri [nasıl tooreset StorSimple cihaz toofactory varsayılan ayarları](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Cihazınızı yapılandırmak ve StorSimple Yöneticisi hizmetiniz ile yeniden kaydedin.
4. Merhaba üzerinde **aygıtları** hello eski aygıt sayfasında göster olarak **çevrimdışı**. Merhaba yeni kayıtlı cihaz olarak göstermelidir **çevrimiçi**.
5. Merhaba yeni cihaz hello en düşük yapılandırma hello cihazın ilk tamamlayın. 
   
   > [!IMPORTANT]
   > **Merhaba en düşük yapılandırma ilk tamamlanmazsa, DR hello geçerli uygulama bir hata nedeniyle başarısız olur. Bu davranış, bir sonraki sürümde düzeltilecektir.**
   > 
   > 
6. Merhaba eski aygıt (çevrimdışı durumu) seçin ve tıklatın **yük devretme**. Sunulan hello Sihirbazı'nda bu cihaz başarısız ve hello hedef aygıt hello yeni kayıtlı cihazı olarak belirtin. Ayrıntılı yönergeler için çok başvuran[tooanother fiziksel aygıt üzerinden başarısız](#fail-over-to-another-physical-device).
7. Cihaz geri yükleme işi hello izleyebilirsiniz oluşturulacak **işleri** sayfası.
8. Merhaba iş başarıyla tamamlandıktan sonra erişim hello yeni cihaz ve toohello gidin **birim kapsayıcıları** sayfası. Merhaba eski aygıttan tüm hello birim kapsayıcıları artık geçirilen toohello yeni cihaz olması gerekir.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>Tooa StorSimple sanal cihazı başarısız
Bir StorSimple sanal cihazı oluşturulur ve önceki toorunning yapılandırılmış olması gerekir bu yordam. Güncelleştirme 2 çalıştıran bir 8020 sanal cihazı Merhaba 64 TB sahiptir ve Premium depolama kullanan DR kullanmayı düşünün. 

Aşağıdaki adımları toorestore hello aygıt tooa hedef StorSimple sanal cihazı hello gerçekleştirin.

1. Bu hello birim kapsayıcısı üzerinde toofail istediğiniz bulut anlık görüntüleri ilişkili doğrulayın.
2. Merhaba üzerinde **aygıtları** hello sayfasında, **birim kapsayıcıları** sekmesi.
3. Tooanother aygıt üzerinden toofail istediğiniz bir birim kapsayıcısı seçin. Merhaba birim kapsayıcı toodisplay hello birimlerin listesini bu kapsayıcıdaki'ı tıklatın. Bir birim seçin ve tıklatın **Çevrimdışına Al** tootake hello çevrimdışı birim. Merhaba birim kapsayıcısındaki tüm hello birimleri için bu işlemi yineleyin.
4. Önceki adımı yineleyin hello tüm birim kapsayıcıları hello için tooanother aygıt üzerinden toofail istersiniz.
5. Merhaba üzerinde **aygıtları** sayfasında, **yük devretme**.
6. Altında açılır hello Sihirbazı'nda **birim kapsayıcı toofailover seçin**, hello aşağıdaki adımları tamamlayın:
   
    a. Birim kapsayıcıları Hello listesinde toofail üzerinden istediğiniz hello birim kapsayıcıları seçin.
   
    **Yalnızca ilişkili bulut anlık görüntüleri ile birim kapsayıcıları hello ve çevrimdışı birimler görüntülenir.**
   
    b. Altında **bir hedef cihaz hello birimleri için seçilen Merhaba kapsayıcılara seçin**, hello StorSimple sanal cihazı kullanılabilir cihazların Merhaba aşağı açılan listeden seçin. **Yalnızca yeterli kapasiteye sahip hello cihazların Merhaba aşağı açılan listesinde görüntülenir.**  
7. Son olarak, tüm hello yük devretme ayarlarda gözden **yük devretme onaylayın**. Merhaba onay simgesine ![onay simgesi](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Merhaba yük devretme tamamlandıktan sonra toohello Git **aygıtları** sayfası.
   
    a. Merhaba yük devretme işlemi için hello hedef cihaz olarak kullanılan hello StorSimple sanal cihazı seçin.
   
    b. Toohello Git **birim kapsayıcıları** sayfası. Merhaba eski aygıt hello birimlerden yanı sıra tüm hello birim kapsayıcıları listelenmiş olmalıdır.

![Video var](./media/storsimple-device-failover-disaster-recovery/Video_icon.png) **Video var**

toowatch nasıl, başarısız bir fiziksel aygıt tooa sanal aygıt hello bulutta üzerinden geri yükleyebilirsiniz gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Yeniden çalışma
Güncelleştirme 3 ve sonraki sürümler için StorSimple geri dönme de destekler. Merhaba yük devretme işlemi tamamlandıktan sonra hello aşağıdaki eylemler gerçekleşir:

* Yük devredildi hello birim kapsayıcıları hello kaynak aygıttan temizlenir.
* Birim kapsayıcısı (devredilir) başına arka plan işi hello kaynak aygıtta başlatılır. Merhaba işi devam ederken toofailback çalışırsanız, bir bildirim toothat efekti alırsınız. Merhaba iş tam toostart hello geri dönme kadar toowait gerekir. 
  
    Merhaba zaman toocomplete hello birim kapsayıcıları silinmesini veri miktarı, hello işlemi için hello veri yedeklemeleri ve hello ağ bant genişliği miktarını sayısı, geçerlilik süresi gibi çeşitli etkenlere bağlıdır. Test yük devretmeleri/mantığın planlıyorsanız, daha az veri (GB) ile birim kapsayıcıları test etmenizi öneririz. Çoğu durumda, 24 saat hello yük devretme işlemi tamamlandıktan sonra hello yeniden başlatabilirsiniz. 

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
Q. **Merhaba DR başarısız veya kısmi başarılı olup olmadığını ne olur?**

A. Merhaba DR başarısız olursa, yeniden deneyin öneririz. Merhaba, geçici ikinci kez DR ne bilir tüm yapıldı ve ne zaman hello işlemi durduruldu hello ilk kez. Merhaba DR işlem veya sonraki sürümleri, bu noktadan başlar. 

Q. **Merhaba aygıt yük devretme işlemi devam ederken bir aygıtı silme?**

A. Bir kurtarma işlemi devam ederken, bir cihaz silemezsiniz. Merhaba DR tamamlandıktan sonra yalnızca cihazınız silebilirsiniz.

Q.    **Böylece Hello yerel veri kaynağı aygıtta silinir hello çöp toplama hello kaynak aygıtta başlattığınızda?**

A. Yalnızca hello aygıt tamamen temizlenir sonra atık toplama hello kaynak aygıtta etkinleştirilecek. Merhaba temizleme üzerinden birimler, yedek nesnesini (verileri değil), birim kapsayıcıları ve ilkeleri gibi hello kaynak aygıttan başarısız olan nesneleri temizleniyor içerir.

Q. **Başarısız Hello hello birim kapsayıcıları hello kaynak aygıtta ile ilişkili iş silersem ne olur?**

A.  Ardından Hello işi başarısız silerseniz, hello birim kapsayıcıları toomanually tetikleyici hello silinmesi gerekir. Merhaba, **aygıtları** sayfasında, kaynak Cihazınızı seçin ve tıklayın **birim kapsayıcıları**. Üzerinden ve başlangıç sayfasının alt kısmındaki Merhaba, başarısız select hello birim kapsayıcıları tıklatın **silmek**. Tüm hello sildikten sonra hello kaynak cihazdaki birim kapsayıcıları devredilir, hello yeniden başlatabilirsiniz.

## <a name="business-continuity-disaster-recovery-bcdr"></a>İş sürekliliği olağanüstü durum kurtarma (BCDR)
Bir iş sürekliliği olağanüstü durum kurtarma (BCDR) senaryosu Hello tüm Azure veri merkezi çalışmıyor oluşur. Bu, StorSimple Yöneticisi hizmetiniz etkileyebilir ve StorSimple cihazlar hello ilişkili.

Yalnızca bir olağanüstü durum oluşmadan önce kaydedilen StorSimple cihazlar varsa, bu StorSimple cihazlar fabrika ayarlarına sıfırlama tooundergo gerekebilir. Merhaba olağanüstü durum sonra hello StorSimple cihaz çevrimdışı olarak gösterilir. Merhaba StorSimple cihazı hello portalından silinmelidir ve yeni bir kayıt tarafından izlenen bir Fabrika sıfırlaması yapılmalıdır.

## <a name="next-steps"></a>Sonraki adımlar
* Bir yük devretme gerçekleştirdikten sonra çok gerekebilir[StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-deactivate-and-delete-device.md).
* Hizmet nasıl toouse hello StorSimple Yöneticisi hakkında daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

