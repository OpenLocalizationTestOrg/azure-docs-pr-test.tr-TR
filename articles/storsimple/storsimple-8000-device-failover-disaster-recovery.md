---
title: "aaaStorSimple yük devretme, 8000 serisi cihazlar için olağanüstü durum kurtarma | Microsoft Docs"
description: "Bilgi nasıl StorSimple cihaz tooitself, başka bir fiziksel aygıt ya da bulut uygulaması üzerinden toofail."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>StorSimple 8000 serisi cihazınız için yük devretme ve olağanüstü durum kurtarma

## <a name="overview"></a>Genel Bakış

Bu makalede hello aygıt yük devretme özelliğini hello StorSimple 8000 serisi cihazlar için ve olağanüstü bir durum oluşursa, bu özellik kullanılan toorecover StorSimple cihazları nasıl yüklenebilir açıklanmaktadır. StorSimple cihaz yük devretme toomigrate hello veri kaynağı aygıttan hello datacenter tooanother hedef aygıt kullanır. Bu makaledeki Hello kılavuz tooStorSimple 8000 serisi fiziksel cihazlar ve yazılım sürümlerini güncelleştirme 3 ve sonraki sürümleri çalıştıran bulut uygulamaları geçerlidir.

StorSimple kullanan hello **aygıtları** dikey toostart hello aygıt yük devretme özelliğini hello olayı olağanüstü bir durum içinde. Bu dikey tüm hello StorSimple cihazları bağlı tooyour StorSimple cihaz Yöneticisi hizmeti listeler.

![Aygıtları dikey penceresi](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Olağanüstü Durum Kurtarma (DR) ve aygıtı yük devretme

Bir olağanüstü durum kurtarma (DR) senaryosunda hello birincil aygıt çalışmamaya başlar. StorSimple kullanan hello birincil cihaz olarak _kaynak_ ve ilişkili hello bulut veri tooanother taşır _hedef_ aygıt. Bu bir işlemdir başvurulan tooas hello *yük devretme*. Grafiği aşağıdaki hello yük devretme hello işlemi gösterilmektedir.

![Cihaz yük devretme kümesinde ne olur?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

Merhaba hedef cihaz için bir yük devretme, bir fiziksel aygıt ya da bulut uygulaması olabilir. Merhaba hedef aygıt olabilir hello aynı veya farklı bir coğrafi konumda hello kaynak cihaz bulunur.

Merhaba yük devretme sırasında geçiş için birim kapsayıcıları seçebilirsiniz. StorSimple sonra hello kaynak aygıt toohello hedef aygıttan hello bu birim kapsayıcıları sahipliği değiştirir. Merhaba birim kapsayıcıları sahipliği değiştirdiğinizde, StorSimple Bu kapsayıcılar hello kaynak aygıttan siler. Merhaba silme işlemi tamamlandıktan sonra geri hello hedef aygıt başarısız olabilir. _Yeniden çalışma_ aktarımları hello sahipliği geri toohello özgün kaynak aygıt.

### <a name="cloud-snapshot-used-during-device-failover"></a>Cihaz yük devretme sırasında kullanılan bulut anlık görüntüsü

Bir DR hello en son bulut yedekleme kullanılan toorestore hello veri toohello hedef aygıttır. Bulut anlık görüntüleri hakkında daha fazla bilgi için bkz: [hello StorSimple cihaz Yöneticisi hizmeti tootake el ile yedekleme kullanmak](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

Bir StorSimple 8000 serisi yedekleme ilkeleri yedeklemelerini ile ilişkilendirilir. Birden çok yedekleme ilkeleri varsa hello aynı birim sonra StorSimple seçer hello en büyük birim sayısı ile yedekleme İlkesi hello için. StorSimple seçili hello yedekleme İlkesi toorestore hello veri hello en son yedeklemeden sonra hello hedef cihazda kullanır.

Vardır varsayalım iki yedekleme ilkeleri *defaultPol* ve *customPol*:

* *defaultPol*: tek bir birim *vol1*, günlük 10: 30'pm başlangıç çalıştırır.
* *customPol*: dört birim *vol1*, *vol2*, *vol3*, *vol4*, günlük 10: 00'dan başlayarak çalıştırır.

Bu durumda, StorSimple kilitlenme tutarlılığı için öncelik veren ve kullandığı *customPol* daha fazla birim sahibidir. Bu ilke en son yedeklemeden Hello kullanılan toorestore verilerdir. Hakkında daha fazla bilgi için toocreate ve yedekleme ilkelerini yönetmek, çok gidin[hello StorSimple cihaz Yöneticisi hizmeti toomanage yedekleme ilkelerini kullanma](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Cihaz yük devretme için ortak ilgili önemli noktalar

Bir aygıt üzerinden başarısız önce aşağıdaki bilgilerle hello gözden geçirin:

* Bir aygıt yük devretmeyi başlatmadan önce tüm hello birimleri hello birim kapsayıcıları içinde çevrimdışı olması gerekir. Planlanmamış yük devretme kümesinde StotSimple birimleri otomatik olarak çevrimdışı. Ancak, planlanmış bir yük devretme (tootest DR) gerçekleştiriyorsanız, tüm hello birimleri çevrimdışı duruma getirmeniz gerekir.
* Yalnızca ilişkili bir sahip birim kapsayıcıları hello bulut anlık görüntüsü, DR için listelenir. En az bir birim kapsayıcısı ile ilişkili bulut anlık görüntü toorecover veri olması gerekir.
* StorSimple arasında birden çok birim kapsayıcıları span bulut anlık görüntüleri varsa, bu birim kapsayıcıları bir küme olarak başarısız olur. Nadir bir örneğinde birden çok birim kapsayıcıları yayılan yerel anlık görüntüleri vardır, ancak ilişkili bulut anlık görüntüleri yapın, StorSimple hello yerel anlık görüntüleri başarısız ve hello yerel veri DR sonra kaybolur.
* Merhaba kullanılabilir hedef DR için yeterli alanı tooaccommodate Seçili birim kapsayıcıları hello cihazları aygıtlardır. Yeterli alana sahip değilse, hedef cihaz olarak listelenmeyen tüm cihazlar.
* DR (için sınırlı bir süresi) sonra hello veri erişim performansını önemli ölçüde etkilenebilir, hello cihazı olarak tooaccess hello bulut verilerden hello ve yerel olarak depolamak.

#### <a name="device-failover-across-software-versions"></a>Cihaz yük devretme yazılım sürümleri arasında

StorSimple cihaz Yöneticisi hizmeti bir dağıtımda olabilir birden çok aygıt, fiziksel ve bulut, tüm çalışan farklı yazılım sürümleri.

Yük devri veya farklı bir yazılım sürümü ve hello birim türleri DR sırasında nasıl davranacağını çalıştıran arka tooanother cihaz başarısız olursa tablo toodetermine aşağıdaki hello kullanın.

#### <a name="failover-and-failback-across-software-versions"></a>Yük devretme ve yeniden çalışma yazılım sürümleri arasında

| Yük devri / geri başarısız | Fiziksel cihaz | Bulut gereci |
| --- | --- | --- |
| Güncelleştirme 3 tooUpdate 4 |Katmanlı birimlerin katmanlı üzerinde başarısız. <br></br>Yerel olarak sabitlenmiş üzerinde yerel olarak sabitlenmiş birimlerin başarısız. <br></br> Bir yük devretme hello güncelleştirme 4 aygıtta bir anlık görüntüsünü olduğunda aşağıdaki [heatmap tabanlı izleme](storsimple-update4-release-notes.md#whats-new-in-update-4) devreye girer. |Yerel olarak katmanlı birimler yük devretme sabitlenir. |
| Güncelleştirme 4 tooUpdate 3 |Katmanlı birimlerin katmanlı üzerinde başarısız. <br></br>Yerel olarak sabitlenmiş üzerinde yerel olarak sabitlenmiş birimlerin başarısız. <br></br> Kullanılan yedeklemeleri toorestore heatmap meta verileri korur. <br></br>Heatmap tabanlı izleme, güncelleştirme bir yeniden çalışma aşağıdaki 3'te kullanılamıyor. |Yerel olarak katmanlı birimler yük devretme sabitlenir. |


## <a name="device-failover-scenarios"></a>Cihaz yük devretme senaryoları

Bir olağanüstü durum varsa, StorSimple Cihazınızı toofail tercih edebilirsiniz:

* [tooa fiziksel aygıt](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [tooa bulut uygulaması](storsimple-8000-device-failover-cloud-appliance.md).

Merhaba önceki makaleleri ayrıntılı adımlar için her yük devretme durumları yukarıda hello sağlayın.


## <a name="failback"></a>Yeniden çalışma

Güncelleştirme 3 ve sonraki sürümler için StorSimple geri dönme de destekler. Yeniden çalışma yalnızca hello yük devretme ters, hello hedef hello kaynağı haline gelir ve hello özgün kaynak cihaz şimdi hello yük devretme sırasında hello hedef aygıt hale içindir. 

StorSimple hello veri geri toohello birincil konumu yeniden eşitler geri dönme sırasında hello g/ç ve uygulama etkinlik durdurur ve özgün konumuna geri toohello geçiş.

Bir yük devretme işlemi tamamlandıktan sonra StorSimple hello aşağıdaki eylemleri gerçekleştirir:

* StorSimple hello kaynak aygıttan devredildi hello birim kapsayıcıları temizler.
* StorSimple birim kapsayıcısı (Merhaba kaynak aygıtta devredilir) başına bir arka plan iş başlatır. Geri hello işi devam ederken toofail çalışırsanız, bir bildirim toothat efekti alıyorsunuz. Tam toostart hello geri dönme Hello iş olana kadar bekleyin.
* toocomplete hello birim kapsayıcıları silinmesini gerçekleştirilecek hello zaman veri miktarı, hello işlemi için hello veri yedeklemeleri ve hello ağ bant genişliği miktarını sayısı, geçerlilik süresi gibi çeşitli etkenlere bağlıdır.

Yük devretme sınaması işlemlerini planlama veya test çalışmaları, daha az veri (GB) ile birim kapsayıcıları test etmenizi öneririz. Genellikle, 24 saat hello yük devretme işlemi tamamlandıktan sonra hello yeniden başlatabilirsiniz.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

Q. **Merhaba DR başarısız veya kısmi başarılı olup olmadığını ne olur?**

A. Merhaba DR başarısız olursa, yeniden deneyin öneririz. Hello ikinci aygıt yük devretme işine hello ilk iş hello ilerleme durumunu farkındadır ve sonraki sürümlerde, bu noktadan başlar.

Q. **Merhaba aygıt yük devretme işlemi devam ederken bir aygıtı silme?**

A. Bir kurtarma işlemi devam ederken, bir cihaz silemezsiniz. Merhaba DR tamamlandıktan sonra yalnızca cihazınız silebilirsiniz. Merhaba hello aygıt yük devretme iş ilerleme durumunu izleyebilirsiniz **işleri** dikey.

Q. **Böylece Hello yerel veri kaynağı aygıtta silinir hello çöp toplama hello kaynak aygıtta başlattığınızda?**

A. Yalnızca hello aygıt tamamen temizlendikten sonra atık toplama hello kaynak aygıtta etkinleştirilir. Merhaba temizleme üzerinden birimler, yedek nesnesini (verileri değil), birim kapsayıcıları ve ilkeleri gibi hello kaynak aygıttan başarısız olan nesneleri temizleniyor içerir.

Q. **Başarısız Hello hello birim kapsayıcıları hello kaynak aygıtta ile ilişkili iş silersem ne olur?**

A.  Merhaba işi başarısız silerseniz, hello birim kapsayıcıları el ile silebilirsiniz. Merhaba, **aygıtları** dikey penceresinde kaynak Cihazınızı seçin ve tıklatın **birim kapsayıcıları**. Merhaba dikey penceresinde hello sonuna ve üzerinden başarısız select hello birim kapsayıcıları tıklatın **silmek**. Tüm hello sildikten sonra hello kaynak cihazdaki birim kapsayıcıları devredilir, hello yeniden başlatabilirsiniz. Daha fazla bilgi için çok Git[birim kapsayıcısı silme](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>İş sürekliliği olağanüstü durum kurtarma (BCDR)

Bir iş sürekliliği olağanüstü durum kurtarma (BCDR) senaryosu Hello tüm Azure veri merkezi çalışmıyor oluşur. Bu senaryo, StorSimple cihaz Yöneticisi hizmetiniz etkileyebilir ve StorSimple cihazlar hello ilişkili.

Yalnızca bir olağanüstü durum oluşmadan önce StorSimple cihazını kaydedildiyse, bu cihazı fabrika ayarlarına sıfırlama tooundergo gerekebilir. Merhaba olağanüstü durum sonra hello StorSimple cihazı hello Azure portal çevrimdışı olarak görünür. Bu cihaz hello portalından silinmesi gerekir. Merhaba aygıt toofactory varsayılana ve hello hizmeti ile yeniden kaydedin.

## <a name="next-steps"></a>Sonraki adımlar

Hazır tooperform aygıt yük devretme varsa, senaryoları ayrıntılı yönergeler için aşağıdaki hello birini seçin:

- [Tooanother fiziksel aygıt üzerinden başarısız](storsimple-8000-device-failover-physical-device.md)
- [Toohello aynı başarısız aygıt](storsimple-8000-device-failover-same-device.md)
- [Bulut uygulaması tooStorSimple başarısız](storsimple-8000-device-failover-cloud-appliance.md)

Cihazınızı başarısızsa, aşağıdaki seçenekleri şu hello birini seçin:

* [StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).
* [Kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

