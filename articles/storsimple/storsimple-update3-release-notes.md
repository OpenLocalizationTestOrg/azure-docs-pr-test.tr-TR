---
title: "aaaStorSimple 8000 serisi güncelleştirme 3 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler, sorunlar ve geçici çözümler için StorSimple 8000 serisi güncelleştirme 3 açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>3 sürüm notları, StorSimple 8000 serisi cihazınız için güncelleştirme

## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello yeni özellikleri açıklar ve hello kritik açık sorunlar için StorSimple 8000 serisi güncelleştirme 3 tanımlayın. Ayrıca bu sürümde dahil hello StorSimple yazılım güncelleştirmelerinin bir listesini içerir. 

Güncelleştirme 3 sürüm (GA) veya güncelleştirme 0.1 güncelleştirme 2.2 çalışan uygulanan tooany StorSimple cihazı olabilir. Güncelleştirme 3 ile ilişkili hello aygıt 6.3.9600.17759 sürümüdür.

Lütfen StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello sürümde bulunan hello bilgileri gözden geçirin.

> [!IMPORTANT]
> * Güncelleştirme 3 aygıt yazılımı, LSI sürücü ve bellenim ve Storport sahiptir ve Spaceport güncelleştirir. Bu güncelleştirme yaklaşık 1,5-2 saat tooinstall sürer. 
> * Yeni sürümler için güncelleştirmelerinin göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Birkaç gün bekleyin ve ardından güncelleştirmeleri taramak üzere yeniden bunlar olarak yakında kullanılabilir hale gelecektir.
> 
> 

## <a name="whats-new-in-update-3"></a>Güncelleştirme 3'te yenilikler nelerdir?
Merhaba aşağıdaki anahtar geliştirmeler ve hata düzeltmeleri güncelleştirme 3'te yapıldı.

* **Alan geri kazanma değişiklikleri otomatik** – güncelleştirme 3, başlangıç hello alan geri kazanma algoritmalarını çalıştırabilir daha hızlı yürütme kaynaklanan hello sisteminin hello bekleme denetleyicisinde. Alan geri kazanma ile gerekli toowork hello bağlantı hakkında daha fazla bilgi için toohello başvuran [ağ gereksinimleri StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Performans iyileştirmeleri** – güncelleştirme 3'ü okuma-yazma performansı toohello bulut iyileştirilmiştir.
* **Geçiş ile ilgili geliştirmeler** – bu sürümde, çeşitli hata düzeltmeleri ve geliştirmeleri 5000/7000 Serisi cihazlar too8000 serisi aygıtlardan hello geçiş özelliği için yapılan. Nasıl toouse hello geçiş özelliğini daha fazla bilgi için çok Git[5000/7000 Serisi aygıt too8000 serisi aygıttan geçiş](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **İlgili düzeltmeleri izleme** - bu sürümde, hatalar ilgili toomonitoring grafikler, hizmet panosunu ve cihaz Pano giderildi.

## <a name="issues-fixed-in-update-3"></a>Güncelleştirme 3'te giderilen sorunlar
Aşağıdaki tablolar hello güncelleştirme 3'te düzeltilen sorunlardan özetini sağlar.    

| Hayır | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Konak tarafındaki veri geçişi |Hello önceki sürüm, StorSimple bulut uygulaması hello bir ana bilgisayar tarafı veri geçişi sırasında çevrimdışı duruma geçiyor. Bu sürümde bu sorun düzeltilmiştir. |Hayır |Evet |
| 2 |Yerel olarak sabitlenmiş birimleri |Merhaba önceki sürümde sorunları ilgili tooI/O hataları, toplu dönüştürme hataları ve yerel olarak sabitlenmiş birimlerin datapath hataları vardı. Bu sorunları kök neden oldu ve bu sürümde sabit. |Evet |Hayır |
| 3 |İzleme |Birden çok sorunları ilgili tooreporting birimleri yoktu ve sabitlenmiş birimleri izleme cihaz Pano grafikleri yanı sıra yanlış bilgiler için yerel olarak görüntülendiği. Bu sürümde bu sorunlar giderildi. |Evet |Hayır |
| 4 |Ağır yazma g/ç |StorSimple ağır yazma işlemleri içeren iş yükleri için kullanılırken, hello kullanıcı sık bir hatayı burada hello çalışma kümesi hello bulutunu katmanlı çalışır. Bu hata, bu sürümde sabittir. |Evet |Evet |
| 5 |Backup |Merhaba önceki sürümlerinde, yazılımın nadir bazı durumlarda, kullanıcı uzak bir kopya yedeği sürdü, bulut hatalarla karşılaşırsanız çalışır ve kullanıma alma hatası hello işlemi gerekir. Bu sürümde, hello sorun giderilmiştir ve hello işlemi başarıyla tamamlandıktan. |Evet |Evet |
| 6 |Yedekleme ilkesi |Belirli ender durumlarda hello daha önce yayınlanan yazılım, bir hata oluştu ilgili yedekleme ilkesini toohello silinmesini. Bu sürümde bu sorun düzeltilmiştir. |Evet |Evet |

## <a name="known-issues-in-update-3"></a>Güncelleştirme 3'te bilinen sorunlar
Aşağıdaki tablonun hello bu sürümdeki bilinen sorunlara özetini sağlar.

| Hayır. | Özellik | Sorun | Yorumlar / geçici çözüm | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |Disk çekirdek |Hiçbir disk çekirdek kaynaklanan hello EBOD muhafazası 8600 aygıtının diskleri Hello çoğunluğu bağlantısı kesildiyse nadir durumlarda, ardından hello depolama havuzu çevrimdışı geçer. Merhaba diskleri bağlanırlar olsa bile çevrimdışı kalır. |Tooreboot hello aygıt gerekir. Merhaba sorun devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 2 |Yanlış denetleyici kimliği |Bir denetleyici değiştirme gerçekleştirildiğinde, denetleyici 0 denetleyicisi 1 olarak görünebilirler. Merhaba görüntü hello eş düğümden yüklendiğinde denetleyicisi değiştirme sırasında hello denetleyici kimliği başlangıçta hello eş denetleyicinin kimliği olarak gösterebilir Nadir durumlarda, bu davranış bir sistem yeniden başlatıldıktan sonra görülebilir. |Hiçbir kullanıcı eylemi gerekli değildir. Merhaba denetleyicisi değiştirme işlemi tamamlandıktan sonra bu durum kendisini çözümleyin. |Evet |Hayır |
| 3 |Depolama hesapları |Merhaba depolama hizmeti toodelete hello depolama hesabı kullanarak desteklenmeyen bir senaryodur. Bu kullanıcı verileri alınamıyor tooa durum götürür. | |Evet |Evet |
| 4 |Cihaz yük devretme |Aynı kaynak aygıt toodifferent hedef cihazlar desteklenmiyor hello birim kapsayıcıdan birden çok yük. Yük devretme tek ölü aygıt toomultiple aygıtlardan veri sahipliği kaybetmek hello birim kapsayıcıları ilk aygıt üzerinden başarısız hello üzerinde hale getirir. Bu tür bir yük devretme sonrasında, bu birim kapsayıcıları görünür veya hello Klasik Azure portalında görüntülediğinizde farklı şekilde davranır. | |Evet |Hayır |
| 5 |Yükleme |SharePoint yükleme için StorSimple bağdaştırıcısı sırasında tooprovide cihaz IP hello yükleme toofinish sırada başarıyla gerekir. | |Evet |Hayır |
| 6 |Web proxy |Web proxy yapılandırması varsa hello olarak HTTPS protokolü, belirtilen sonra aygıtı hizmeti iletişimi etkilenecek ve hello aygıt çevrimdışı. Destek paketleri aygıtınızda önemli miktarda kaynak tüketen hello işlemde de oluşturulur. |Belirtilen protokol hello gibi Hello web proxy URL'Sİ'ın HTTP olduğundan emin olun. Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](storsimple-configure-web-proxy.md). |Evet |Hayır |
| 7 |Web proxy |Yapılandırma ve web proxy bir kayıtlı cihazda etkinleştirirseniz, Cihazınızda toorestart hello etkin denetleyicisine ihtiyacınız vardır. | |Evet |Hayır |
| 8 |Yüksek bulut gecikme süresi ve yüksek g/ç iş yükü |StorSimple Cihazınızı çok yüksek bulut gecikme (saniye sırasını) ve yüksek g/ç iş yükü bileşimini karşılaştığında, düzeyi düşürülmüş bir duruma hello aygıt birimleri gidin ve hello g/ç "cihaz hazır değil" hatası ile başarısız. |Toomanually yeniden başlatma hello cihaz denetleyicilerinin gerekir veya bir aygıt yük devretme toorecover bu durumdan gerçekleştirin. |Evet |Hayır |
| 9 |Azure PowerShell |Merhaba StorSimple cmdlet'ini kullandığınızda **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - ilk 1 - bekleme** tooselect yeni oluşturabilmesi için ilk nesne hello **VolumeContainer** nesne hello cmdlet'i tüm hello nesneleri döndürür. |Merhaba cmdlet parantez içine aşağıdaki gibi kaydır: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - ilk 1 - bekleme** |Evet |Evet |
| 10 |Geçiş |Geçiş için birden çok birim kapsayıcıları geçirildiğinde hello ETA son yedekleme için yalnızca hello ilk birim kapsayıcısı için doğru olur. Ayrıca, paralel geçiş Hello hello ilk birim kapsayıcısı ilk 4 yedeklemelerin geçirildikten sonra başlar. |Bir kerede bir birim kapsayıcısı geçirmek öneririz. |Evet |Hayır |
| 11 |Geçiş |Merhaba geri yüklendikten sonra birimleri toohello yedekleme İlkesi veya hello sanal disk grubu eklenmedi. |Bu birimleri tooa yedekleme ilkesine sipariş toocreate yedeklemeleri tooadd gerekir. |Evet |Evet |
| 12 |Geçiş |Merhaba geçiş tamamlandıktan sonra hello 5000/7000 Serisi aygıt değil erişmelisiniz hello geçirilen verileri kapsayıcıları. |Merhaba silmenizi öneririz tam ve kaydedilmiş hello geçiş tamamlandıktan sonra veri kapsayıcıları geçişi. |Evet |Hayır |
| 13 |Kopya ve DR |Güncelleştirme 1 çalıştıran bir StorSimple cihazı kopyalama veya güncelleştirme 1 yazılımı öncesini çalıştıran olağanüstü durum kurtarma tooa cihaz gerçekleştirin. |Bu işlemler tooupdate hello hedef aygıt tooUpdate 1 tooallow gerekir |Evet |Evet |
| 14 |Geçiş |Birim grupları ile ilişkili birim olduğunda geçiş için yedekleme yapılandırması 5000-7000 Serisi aygıtta başarısız olabilir. |Tüm hello boş birim grupları ile ilişkili birim silin ve hello yapılandırma yedeklemeyi yeniden deneyin. |Evet |Hayır |
| 15 |Azure PowerShell cmdlet'leri ve yerel olarak sabitlenmiş birimleri |Azure PowerShell cmdlet'leri aracılığıyla yerel olarak sabitlenmiş bir birim oluşturamazsınız. (Azure PowerShell ile oluşturduğunuz herhangi bir birim katmanlı.) |Her zaman hello StorSimple Yöneticisi hizmeti tooconfigure yerel olarak sabitlenmiş birimleri kullanın. |Evet |Hayır |
| 16 |Yerel olarak sabitlenmiş birimleri için kullanılabilir alanı |Yerel olarak sabitlenmiş bir birim silerseniz, yeni birimleri için kullanılabilir hello alanı hemen güncelleştirilmemiş. Merhaba StorSimple Yöneticisi hizmet güncelleştirmeleri kullanılabilir yerel alanı yaklaşık olarak saatte hello. |Toocreate hello yeni birim denemeden önce bir saat bekleyin. |Evet |Hayır |
| 17 |Yerel olarak sabitlenmiş birimleri |Geri yükleme işi hello geçici anlık görüntü yedekleme hello yedekleme kataloğu, ancak yalnızca hello geri yükleme işi hello süresi için kullanıma sunar. Ayrıca, bir sanal disk grubu önekiyle gösterir **tmpCollection** hello üzerinde **yedekleme ilkeleri** sayfasında, ancak yalnızca hello süresince hello geri yükleme işi. |Bu davranış, geri yükleme işi birimleri veya yerel olarak sabitlenmiş ve katmanlı birimlerin bir karışımını yalnızca yerel olarak sabitlenmiş ortaya çıkabilir. Merhaba geri yükleme işi yalnızca katmanlı birimleri içeriyorsa, bu davranış gerçekleşmez. Kullanıcı müdahalesi gerekli değildir. |Evet |Hayır |
| 18 |Yerel olarak sabitlenmiş birimleri |Bir geri yükleme işi iptal edin ve hello geri yükleme işi daha sonra gösterecektir hemen denetleyici yük devretmesi oluşursa **başarısız** yerine **iptal edildi**. Geri yükleme işi başarısız olur ve daha sonra hello geri yükleme işi gösterecektir hemen denetleyici yük devretmesi oluşursa **iptal edildi** yerine **başarısız**. |Bu davranış, geri yükleme işi birimleri veya yerel olarak sabitlenmiş ve katmanlı birimlerin bir karışımını yalnızca yerel olarak sabitlenmiş ortaya çıkabilir. Merhaba geri yükleme işi yalnızca katmanlı birimleri içeriyorsa, bu davranış gerçekleşmez. Kullanıcı müdahalesi gerekli değildir. |Evet |Hayır |
| 19 |Yerel olarak sabitlenmiş birimleri |Bir geri yükleme işi iptal edin veya geri yükleme başarısız olur ve bir denetleyici yük devretmesi oluşur, ek geri yükleme işi hello üzerinde görünür **işleri** sayfası. |Bu davranış, geri yükleme işi birimleri veya yerel olarak sabitlenmiş ve katmanlı birimlerin bir karışımını yalnızca yerel olarak sabitlenmiş ortaya çıkabilir. Merhaba geri yükleme işi yalnızca katmanlı birimleri içeriyorsa, bu davranış gerçekleşmez. Kullanıcı müdahalesi gerekli değildir. |Evet |Hayır |
| 20 |Yerel olarak sabitlenmiş birimleri |Tooconvert (oluşturulan ve güncelleştirme 1.2 ile kopyalanan veya öncesi) katmanlı birim çalışırsanız tooa yerel olarak sabitlenmiş birim ve Cihazınızı alana sahip değil veya bir bulut kesinti yoktur ve sonra hello clone(s) bozulmuş. |Bu sorun, oluşturulan ve kopyalanan ile güncelleştirme öncesi 2.1 yazılım olan birimlerle oluşur. Bu, seyrek bir senaryo olmalıdır. | | |
| 21 |Birim dönüştürme |Bir birim dönüştürme işlemi devam ederken hello ACRs ekli tooa toplu güncelleştirmeyi (katmanlı toolocally sabitlenmiş veya tersi). Merhaba ACRs güncelleştirme veri bozulmasına neden olabilir. |Gerekirse, hello ACRs önceki toohello birim dönüştürme güncelleştirin ve hello dönüştürme işlemi devam ederken ACR güncelleştirmeleri başka yapmayın. | | |
| 22 |Güncelleştirmeler |Güncelleştirme 3'ü uygularken hello **Bakım** hello Azure Klasik portalı sayfasında görünen hello aşağıdaki ileti ilgili tooUpdate 2 - "StorSimple 8000 serisi güncelleştirme 2 hello özelliğini içerir Microsoft tooproactively toplama için Biz olası sorunlar algılandığında aygıtınızdan günlük bilgileri". Güncelleştirilmiş tooUpdate 2 Bu hello aygıtı olmaktan belirttiği yanıltıcıdır. Güncelleştirilmiş succeesfully tooUpdate 3 Hello cihaz olduktan sonra bu ileti kaybolur. |Bu davranış, bir sonraki sürümde düzeltilecektir. |Evet |Hayır |

## <a name="controller-and-firmware-updates-in-update-3"></a>Güncelleştirme 3'te denetleyicisi ve bellenim güncelleştirmeleri
Bu sürüm LSI sahip sürücü ve bellenim güncelleştirmeleri. Tooinstall hello LSI sürücü ve bellenim güncelleştirmeleri nasıl görürüm hakkında daha fazla bilgi için [güncelleştirme 3'ü yükleme](storsimple-install-update-3.md) , StorSimple Cihazınızda.

## <a name="virtual-device-updates-in-update-3"></a>Güncelleştirme 3'te sanal aygıt güncelleştirmeleri
Bu güncelleştirme uygulanan toohello StorSimple bulut uygulaması (olarak da bilinen hello sanal cihaz) olamaz. Yeni sanal cihazların oluşturulan toobe gerekir. 

## <a name="next-step"></a>Sonraki adım
Nasıl çok öğrenin[güncelleştirme 3'ü yükleme](storsimple-install-update-3.md) , StorSimple Cihazınızda.

