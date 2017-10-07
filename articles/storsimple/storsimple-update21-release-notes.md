---
title: "aaaStorSimple 8000 serisi güncelleştirme 2.2 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler, sorunlar ve geçici çözümler için StorSimple 8000 serisi güncelleştirme 2.2 açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/18/2016
ms.author: alkohli
ms.openlocfilehash: a2902126f4011fa9ade64f63a8abdec095874fb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>StorSimple 8000 serisi güncelleştirme 2.2 sürüm notları
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello yeni özellikleri açıklar ve hello kritik açık sorunlar için StorSimple 8000 serisi güncelleştirme 2.2 tanımlayın. Ayrıca bu sürümde dahil hello StorSimple yazılım güncelleştirmelerinin bir listesini içerir. 

Güncelleştirme 2.2 sürüm (GA) veya güncelleştirme 0.1 güncelleştirme 2. 1 ' çalışan uygulanan tooany StorSimple cihazı olabilir. Güncelleştirme 2.2 ile ilişkili hello aygıt 6.3.9600.17708 sürümüdür.

Lütfen StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello sürümde bulunan hello bilgileri gözden geçirin.

> [!IMPORTANT]
> * Güncelleştirme 2.2 yalnızca yazılım güncelleştirmeleri sahiptir. Bu güncelleştirme yaklaşık 1,5-2 saat tooinstall sürer. 
> * Güncelleştirme 2.1 çalıştırıyorsanız, güncelleştirme 2.2 mümkün olan en kısa sürede uygulamanızı öneririz.
> * Yeni sürümler için güncelleştirmelerinin göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Birkaç gün bekleyin ve ardından güncelleştirmeleri taramak üzere yeniden bunlar olarak yakında kullanılabilir hale gelecektir.
> 
> 

## <a name="whats-new-in-update-22"></a>Güncelleştirme 2.2 yenilikler nelerdir?
Merhaba aşağıdaki anahtar iyileştirmeler güncelleştirme 2.2 yapılmıştır.

* **Alan geri kazanma iyileştirme otomatik** – veri ölçülü kaynak kullanan birimlerde silindiğinde hello kullanılmamış depolama blokları gereksinim iadesi toobe. Bu sürüm hello kullanılmayan kaynaklanan hello buluttan geliştirilmiş hello alan geri kazanma işlemin olma kullanılabilir daha hızlı olarak karşılaştırılan toohello önceki sürümler alanı vardır.
* **Performans iyileştirmeleri anlık görüntü** – güncelleştirme 2.2 burada büyük birimleri kullanıldığından ve en az toono veri dalgalanmasına olmadığından belirli senaryolarda bir bulut anlık görüntüsü geliştirilmiş hello zaman tooprocess sahiptir. Bu geliştirme için yararlı bir senaryo hello arşiv birimleri olacaktır.
* **Destek Paketi toplama sağlamlaştırma** – geliştirmeler hello destek paketi toplanan ve bu sürümde karşıya hello şekilde olmuştur. 
* **Güvenilirlik iyileştirmeleri güncelleştirme** – içinde geliştirilmiş bir güncelleştirme güvenilirliği neden hata düzeltmeleri bu sürüme sahip.

## <a name="issues-fixed-in-update-22"></a>Güncelleştirme 2.2 giderilen sorunlar
Aşağıdaki tablolar hello güncelleştirmeler 2.2 ve 2.1 düzeltilen sorunlardan özetini sağlar.    

| Hayır | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Ana performans |Hello önceki sürüm, ana bilgisayar tarafı performans sorunlarını yerel olarak sabitlenmiş bir birim hello oluşturma sırasında gözlenen ve yerel olarak bir katmanlı birim tooa hello dönüştürme sırasında birim sabitlenir. Böylece bir geliştirme hello ana performans hello birim oluşturma ve dönüştürme yordamları sırasında bunun sonucunda bu sürümde bu sorunlar giderildi. |Evet |Hayır |
| 2 |Yerel olarak sabitlenmiş birimleri |Nadir durumlarda, yerel olarak sabitlenmiş bir birim oluştururken hello sistem kilitlenme. Bu hata, bu sürümde düzeltilmiştir. |Evet |Hayır |
| 3 |Katmanlama |Çok katmanlı hello StorSimple bulut cihazları (8010 hem de 8020) için hello meta verileri Merhaba, bulut durumlarıyla çökme (Crash) vardı. Bu sürümde bu sorun düzeltilmiştir. |Hayır |Evet |
| 4 |Anlık görüntü oluşturma |Artımlı anlık görüntü senaryolarda büyük birimleri ve en az toono veri dalgalanmasına sorunları ilgili toohello oluşturmaya vardı. Bu sürümde bu sorunlar giderildi. |Evet |Evet |
| 5 |Openstack kimlik doğrulaması |Openstack hello bulut hizmeti sağlayıcısı olarak kullanırken, hello kullanıcı sık hata ilgili toohello kimlik doğrulaması burada hello JSON ayrıştırıcı bir kilitlenme sonuçlandı çalışır. Bu hata, bu sürümde sabittir. |Evet |Hayır |
| 6 |Konak tarafındaki kopyalama |Yazılım önceki sürümlerde, toohello ODX zamanlama hello verileri tek bir birim tooanother birimden kopyalarken görülen sık hata ilgili. Bu bir denetleyici yük devretme kümesinde neden olur ve hello sistem olası kurtarma moduna gidebilirsiniz. Bu hata, bu sürümde sabittir. |Evet |Hayır |
| 7 |Windows Yönetim Araçları (WMI) |Merhaba önceki sürümlerinde yazılım, web proxy hatası hello durumla çeşitli örneklerine vardı "<ManagementException> Sağlayıcı yükleme hatası". Bu hata öznitelikli tooa WMI bellek sızıntısı olan ve şimdi sabittir. |Evet |Hayır |
| 8 |Güncelleştirme |Yazılım, önceki sürümlerinde hello bazı nadir durumlarda tooscan veya yükleme güncelleştirmeleri çalışırken "CisPowershellHcsscripterror" Merhaba kullanıcı aldı. Bu sürümde bu sorun düzeltilmiştir. |Evet |Evet |
| 9 |Destek Paketi |Bu sürümde olmuştur geliştirmeleri hello destek paketi toplanan ve karşıya toohello yolu. |Evet |Evet |

## <a name="known-issues-in-update-22"></a>Güncelleştirme 2.2 bilinen sorunlar
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

## <a name="controller-and-firmware-updates-in-update-22"></a>Güncelleştirme 2.2 denetleyici ve bellenim güncelleştirmeleri
Bu sürüm yalnızca yazılım güncelleştirme içerir. Ancak, bir sürüm önceki tooUpdate 2 güncelleştiriyorsanız tooinstall sürücü, Storport, Spaceport, gerekir ve (bazı durumlarda) disk aygıtınızda Bellenim güncelleştirmeleri.

Tooinstall hello sürücü, Storport, Spaceport ve disk Bellenim güncelleştirmeleri nasıl görürüm hakkında daha fazla bilgi için [güncelleştirme 2.2 yüklemek](storsimple-install-update-21.md) , StorSimple Cihazınızda.

## <a name="virtual-device-updates-in-update-22"></a>Güncelleştirme 2.2 sanal aygıt güncelleştirmeleri
Bu güncelleştirme uygulanan toohello sanal aygıt olamaz. Yeni sanal cihazların oluşturulan toobe gerekir. 

## <a name="next-step"></a>Sonraki adım
Nasıl çok öğrenin[güncelleştirme 2.2 yüklemek](storsimple-install-update-21.md) , StorSimple Cihazınızda.

