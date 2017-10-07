---
title: "aaaStorSimple yerel olarak sabitlenmiş birimleri ile ilgili SSS | Microsoft Docs"
description: "StorSimple hakkında sorular yerel olarak sabitlenmiş birimleri yanıtlar toofrequently sorulan sağlar."
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/26/2017
ms.author: manuaery
ms.openlocfilehash: a3a6557ca15e7e1947b45dcfd005640103c09591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>StorSimple yerel olarak sabitlenmiş birimleri: sık sorulan sorular (SSS)
## <a name="overview"></a>Genel Bakış
Hello şunlardır sorular ve yanıtlar bir StorSimple yerel olarak sabitlenmiş birim oluştururken sahip bir katmanlı birim tooa yerel olarak sabitlenmiş birim dönüştürün (ve tersi) veya yedeklemek ve geri yükleme yerel olarak sabitlenmiş bir birim.

Sorular ve yanıtlar kategorileri aşağıdaki hello düzenlenir

* Yerel olarak sabitlenmiş bir birim oluşturma
* Yerel olarak sabitlenmiş yedekleme
* Bir katmanlı birim tooa yerel olarak sabitlenmiş birim dönüştürme
* Yerel olarak sabitlenmiş bir birim geri yükleme
* Yerel olarak sabitlenmiş bir birim yapabilmesini

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Yerel olarak sabitlenmiş bir birim oluşturma hakkında sorular
**S.** Merhaba 8000 serisi cihazlar üzerinde oluşturabilmeniz için yerel olarak sabitlenmiş bir birim hello en büyük boyutu nedir?

**A** StorSimple 8000 serisi güncelleştirme 3.0 çalıştıran cihazlarda too8.5 TB yerel olarak sabitlenmiş birimleri veya hello 8100 cihazda too200 TB katmanlı birimleri sağlayabilirsiniz. Merhaba büyük 8600 cihazında yerel olarak sabitlenmiş birimleri too22.5 TB yedeklemek veya too500 TB katmanlı birimleri sağlayabilirsiniz.

**S.** En son sürümüne yükselttiğimde my 8100 aygıt tooUpdate 3.0 ve toocreate yerel olarak sabitlenmiş birimin çalıştığımda hello kullanılabilir en büyük boyutu yalnızca 6 TB ve 8,5 TB değil. Neden bir 8,5 TB birim oluşturamazsınız?

**A** Cihazınızı güncelleştirme 3.0 çalıştıran too8.5 TB yerel olarak sabitlenmiş birimleri sağlayabilir veya üzerinde too200 TB katmanlı birimleri hello 8100 aygıt. Aygıtınız zaten birimleri katmanlı değilse, yerel olarak sabitlenmiş bir birim oluşturmak için kullanılabilir hello alanı bu Maksimum boyuttan orantılı olarak daha düşük olacaktır. Örneğin, yaklaşık 106 TB katmanlı birimlerin 8100 Cihazınızda zaten sağlanmamışsa (Merhaba yarısı olduğu katmanlı Kapasite), hello 8100 cihazda oluşturabilirsiniz yerel bir birimi en büyük boyutunu hello sonra daha az too4 TB ( kabaca yarısı yerel olarak hello maksimum birim kapasitesi sabitlenmiş).

Merhaba cihazda yerel alan katmanlı birimlerin çalışma kullanılan toohost hello olduğundan hello aygıt birimleri katmanlı değilse hello yerel olarak sabitlenmiş bir birim oluşturmak için kullanılabilir alan azalır. Buna karşılık, yerel olarak sabitlenmiş bir birim orantılı olarak oluşturma hello katmanlı birimler kullanılabilir alanı azaltır. yerel olarak sabitlenmiş birimleri oluşturduğunuzda tabloları aşağıdaki hello hello kullanılabilir katmanlı kapasite hello 8100 ve 8600 cihazlarda özetler.

#### <a name="update-30"></a>Güncelleştirme 3.0 
| Yerel olarak sabitlenmiş birimlerin sağlanan kapasite | Katmanlı birimler için - 8100 sağlanan kullanılabilir kapasite toobe | Katmanlı birimler için - 8600 sağlanan kullanılabilir kapasite toobe |
| --- | --- | --- |
| 0 |200 TB |500 TB |
| 1 TB |176.5 TB |477.8 TB |
| 4 TB |105.9 TB |411.1 TB |
| 8.5 TB |0 TB |311.1 TB |
| 10 TB |NA |277.8 TB |
| 15 TB |NA |166.7 TB |
| 22.5 TB |NA |0 TB |

**S.** Yerel olarak sabitlenmiş birimin oluşturulmasına neden uzun süren bir işlem mi?

**C.** Yerel olarak sabitlenmiş birimlerin sıkı sağlanır. toocreate alan Merhaba hello cihaz yerel katmanlarda, hello sağlama işlemi sırasında bazı verileri var olan katmanlı birimler toohello bulut edilmesini. Ve sağlanacak, hello birimin cihaz ve hello kullanılabilir bant genişliğini toohello bulut, var olan verilere hello hello boyutuna bağlıdır bu yana geçen hello süre toocreate birkaç saat yerel bir birim olabilir.

**S.** Yerel olarak sabitlenmiş bir birim toocreate ne kadar sürer?

**C.** Yerel olarak sabitlenmiş birimlerin sıkı sağlanan olduğundan, katmanlı birimleri varolan bazı verileri toohello bulut hello sağlama işlemi sırasında edilmesini. Bu nedenle, birden çok etkene hello hello birimin boyutunu dahil olmak üzere, yerel olarak sabitlenmiş bir birim bağlıdır geçen süre toocreate Merhaba, veri aygıtınızda hello ve kullanılabilir bant genişliğini hello. Birim olan yeni yüklenmiş cihazda hello zaman toocreate yerel olarak sabitlenmiş bir birim terabayt veri başına yaklaşık 10 dakika ' dir. Ancak, yerel birimlerin oluşturması kullanımda olan bir aygıtta yukarıda açıklanan hello etkenlere bağlı olarak birkaç saat sürebilir.

**S.** Yerel olarak sabitlenmiş bir birim toocreate istiyorum. Tüm en iyi uygulamalarını toobe farkında ihtiyacım var mı?

**C.** Yerel olarak sabitlenmiş birimlerin, veri yerel GARANTİLERİN her zaman gerektirir ve hassas toocloud gecikmeleri olan iş yükleri için uygundur. Herhangi bir iş yükleriniz için yerel birimleri kullanımını ınızın Lütfen hello aşağıdakilere dikkat edin:

* Yerel olarak sabitlenmiş birimlerin sıkı sağlanır ve yerel birimleri oluşturmak katmanlı birimler kullanılabilir alanı hello etkiler. Bu nedenle, küçük boyutlu birimler ile başlamalı ve depolama gereksinimi arttıkça ölçeği öneririz.
* Yerel birimlerin sağlanması, katmanlı birimleri toohello buluttan var olan verileri Ftp'den gerektirebilir uzun süren bir işlemdir. Sonuç olarak, bu birimlerdeki azaltılmış performansla karşılaşabilirsiniz.
* Yerel birimlerin sağlanması uzun süren bir işlemdir. Merhaba gerçek süre ilgili birden çok etkene bağlıdır: Merhaba sağlanacak hello birim, cihaz ve kullanılabilir bant genişliğini veri boyutu. Var olan birimler toohello bulutunuzu yedeklemediyseniz birim oluşturma yavaştır. Yerel bir birim sağlamadan önce var olan birimlerinizi bulut anlık görüntüsünü öneririz.
* Var olan katmanlı birimler toolocally sabitlenmiş birimler dönüştürebilir ve bu dönüştürme alanı hello cihazda yerel olarak sabitlenmiş biriminde (toplama toobringing varsa hello buluta katmanlı veri aşağı) kaynaklanan hello için sağlama ilgilidir. Yeniden, biz yukarıda açıklanan faktöre bağlıdır uzun süre çalışan bir işlemin budur. Merhaba işlemi var olan birimler yedeklenmez, hatta daha yavaş olacak şekilde, var olan birimler önceki tooconversion geri öneririz. Cihazınızı da bu işlem sırasında azaltılmış performansla karşılaşabilirsiniz.

Hakkında daha fazla bilgi çok[yerel olarak sabitlenmiş bir birim oluşturun](storsimple-8000-manage-volumes-u2.md#add-a-volume)

**S.** Merhaba birden çok yerel olarak sabitlenmiş birimler oluşturabilirsiniz aynı anda?

**C.** Evet, ancak herhangi bir yerel olarak sabitlenmiş birim oluşturma ve genişletme işi sıralı olarak işlenir.

Yerel olarak sabitlenmiş birimlerin sıkı sağlanır ve bu (, katmanlı birimleri toobe toohello bulut hello sağlama işlemi sırasında gönderilen varolan veriler sonuçlanabilir) hello cihazda yerel alan oluşturulmasını gerektirir. Sağlama işi devam ediyorsa, bu iş tamamlanana kadar bu nedenle, diğer yerel birim oluşturma işleri sıraya alınır.

Benzer şekilde, var olan bir yerel toplu Genişletilmekte olan veya katmanlı birim dönüştürülen tooa yerel olarak sabitlenmiş birim sonra hello önceki iş tamamlanana kadar hello yeni bir yerel olarak sabitlenmiş birimin oluşturulması sıraya alındı. Yerel olarak sabitlenmiş bir birim Hello boyutunu genişletme hello genişletme hello o birim için var olan yerel alanı içerir. Bir katmanlı toolocally sabitlenmiş birim dönüştürme de yerel olarak sabitlenmiş birim kaynaklanan hello için yerel alan hello oluşturulmasını içerir. Hem bu işlemler, oluşturma veya yerel alan genişlemesi uzun işi çalışıyor.

Bu işleri hello görüntüleyebilirsiniz **işleri** dikey penceresinde hello StorSimple cihaz Yöneticisi hizmeti. Merhaba etkin olarak işlenen sürekli olarak iş alanı sağlama tooreflect hello ilerleme güncelleştirildi. yerel olarak sabitlenmiş birim işleri kalan hello çalışıyor olarak işaretlenmiş, ancak kendi ilerleme durduruldu ve sıraya alınan hello sırayla çekilir.

**S.** I yerel olarak sabitlenmiş bir birim silindi. Toocreate çalıştığınızda iadesi hello alanı hello kullanılabilir alanı yeni bir birim yansıtılır. neden görmüyorum?

**C.** Yerel olarak sabitlenmiş bir birim silerseniz, yeni birimleri için kullanılabilir hello alanı hemen güncelleştirilmemiş. Merhaba StorSimple cihaz Yöneticisi hizmeti hello yerel alan kullanılabilir yaklaşık olarak saatte güncelleştirir. Toocreate hello yeni birim denemeden önce bir saat bekleyin öneririz.

**S.** Yerel olarak sabitlenmiş birimlerin hello bulut aygıtındaki destekleniyor mu?

**C.** Yerel olarak sabitlenmiş birimlerin hello bulut uygulaması (8010 ve 8020 aygıtları önceden başvurulan tooas hello StorSimple sanal cihazı) üzerinde desteklenmez.

**S.** I hello Azure PowerShell cmdlet'leri toocreate kullanabilir ve yerel olarak sabitlenmiş birimleri yönetme?

**C.** Hayır, Azure PowerShell cmdlet'lerini (Azure PowerShell ile oluşturduğunuz herhangi bir birim katmanlı) aracılığıyla yerel olarak sabitlenmiş birimler oluşturamazsınız. Bunu sahip hello gibi istenmeyen etkisini hello birim türü tootiered değiştirme hello Azure PowerShell cmdlet'leri toomodify tüm özelliklerini yerel olarak sabitlenmiş bir birim kullanmayın da öneririz.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Yerel olarak sabitlenmiş bir birim yedekleme hakkında sorular
**S.** Desteklenen yerel olarak sabitlenmiş birimlerin yerel anlık görüntüleri misiniz?

**C.** Evet, yerel olarak sabitlenmiş birimlerin yerel anlık görüntüleri alabilir. Ancak, düzenli olarak, yedekleme verilerinizi, korunan bulut anlık görüntüleri tooensure ile yerel olarak sabitlenmiş birimlerinizi bir olağanüstü durum planlıyorsanız hello öneririz.

Yerel olarak sabitlenmiş birimlerin yerel anlık görüntüleri toohello bulut katmanı da ve hello cihazın hello yerel katmanındaki toostay garanti edilmez unutmayın.

**S.** Yerel olarak sabitlenmiş birimleri için yerel anlık görüntülerini yönetmek için herhangi bir yönerge var mı?

**C.** Yerel anlık görüntüleri yerel olarak sabitlenmiş bir birim üzerinde hello aygıt toobe hızlı bir şekilde kullanılan yerel alan neden ve toohello bulut gönderilen katmanlı birimler verilerden sonucunda hello veri karmaşıklık oranı yüksek yanında sık. Bu nedenle, yerel anlık görüntü hello sayısını en aza öneririz.

**S.** Yerel olarak sabitlenmiş birimlerin my yerel anlık görüntüleri geçersiz bildiren bir uyarı aldım. Ne zaman bu durum oluşabilir?

**C.** Yerel anlık görüntü veri dalgalanmasına hello yerel olarak sabitlenmiş bir birim üzerinde hello aygıt toobe hızlı bir şekilde kullanılan yerel alan neden olabilir, yüksek oranda yanında sık. Merhaba cihaz yerel katmanlarda Hello yoğun olarak kullanılıyorsa, genişletilmiş bulut kesinti dolmasını hello aygıtı neden olabilir ve (boşluk tooupdate hello anlık görüntüleri toorefer aldığından gelen yazma toohello birim hello anlık görüntüleri geçersiz kılma neden olabilir toohello eski bloklarını üzerine yazıldı veri). Böyle bir durum hello toobe sunulan ancak hello yerel anlık görüntüleri geçersiz olabilir, yazma toohello birim devam eder. Hiçbir etkisi tooyour mevcut bulut anlık yoktur.

Merhaba uyarı uyarı, söz konusu böyle bir durum meydana ve aynı zamanında, yerel anlık görüntüleri inceleyerek sık yerel anlık görüntüler veya artık silme eski yerel anlık görüntü daha az tootake zamanlar hello adres olun toonotify değil Gerekli.

Merhaba yerel anlık görüntüleri doğrulanamazsa, zaman damgaları geçersiz kılındı hello arası yerel anlık görüntü hello listesi hello yerel anlık görüntüleri hello özel yedekleme ilkesi için geçersiz kılındı bildiren bir bilgi uyarısı alırsınız. Bu anlık görüntüler otomatik silindi ve artık mümkün tooview olacaktır hello bunları **yedekleme kataloglar** dikey penceresinde hello Azure portalı.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Bir katmanlı birim tooa yerel olarak sabitlenmiş birim dönüştürme hakkında sorular
**S.** Bazı yavaşlığı hello aygıtta bir katmanlı birim tooa yerel olarak sabitlenmiş birim dönüştürülürken Gözlemleme. Bunun nedeni nedir?

**C.** Merhaba dönüştürme işlemi iki adımdan oluşur:

1. Alanı hello cihazda hello için sağlama yakında-için--dönüştürülmesi yerel olarak birim sabitlenir.
2. Herhangi bir katmanlı veri hello bulut tooensure yerel indirme güvence altına alır.

Bu adımları hem de uzun süreli hello dönüştürülür, veri hello cihaz ve kullanılabilir bant genişliğini hello birimin boyutunu bağımlı işlemler. Var olan katmanlı birimler bazı verileri toohello bulut sağlama işlemi hello bir parçası olarak sığdırmaya olarak Cihazınızı bu süre boyunca düşük performansla karşılaşabilirsiniz. Ayrıca, hello dönüştürme işlemi yavaş olabilir varsa:

* Var olan birimler toohello bulut yedeklediyseniz değil; Böylece, birimleri önceki tooinitiating dönüştürme yedekleme öneririz.
* Hangi hello kullanılabilir bant genişliğini toohello bulut kısıtlayabilir bant genişliği azaltma ilkeleri uygulanmış; Bu nedenle, adanmış bir 40 MB/sn veya daha fazla bağlantı toohello bulut sahip öneririz.
* Merhaba dönüştürme işlemi toohello birden çok yukarıda açıklanan faktörleri son birkaç saat sürebilir; Bu nedenle, bu işlemi yükselmeleri olmayan saatlerde veya hafta sonu tooavoid gerçekleştirmek önerdiğimiz hello son tüketiciler üzerindeki etkisi.

Hakkında daha fazla bilgi çok[bir katmanlı birim tooa yerel olarak sabitlenmiş birim Dönüştür](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)

**S.** Merhaba birimi dönüştürme işlemi iptal edebilir miyim?

**C.** Hayır, bir kez başlatılan iptal hello dönüştürme işlemi hello olamaz. Merhaba önceki sorunun içinde açıklandığı gibi hello işlemi sırasında karşılaştığınız ve, dönüştürme planlarken, yukarıda listelenen hello en iyi uygulamaları izleyerek hello olası performans sorunları lütfen unutmayın.

**S.** Toomy birim, Hello dönüştürme işlemi başarısız olursa ne olur?

**C.** Birim dönüştürme toocloud bağlantı sorunları başarısız olabilir. Merhaba aygıt, bir dizi başarısız denemeleri toobring hello bulut katmanlı verilerden aşağı sonra hello dönüştürme işlemi sonunda vermeyebilir. Böyle bir senaryoda hello birim türü toobe hello kaynak birim türü önceki tooconversion, devam eder ve:

* Kritik Uyarı yükseltilmiş toonotify olacaktır, hello birimi dönüştürme hatası. Daha fazla bilgi [ilgili toolocally sabitlenmiş birimleri uyarıları](storsimple-8000-manage-alerts.md#locally-pinned-volume-alerts)
* Bir katmanlı tooa yerel olarak sabitlenmiş birim dönüştürüyorsanız veri hala hello bulutta bulunabilecek şekilde hello birim katmanlı birim tooexhibit özelliklerini devam eder. Merhaba bağlantı sorunlarını çözün ve sonra hello dönüştürme işlemi yeniden deneyin öneririz.
* Hello birim yerel olarak sabitlenmiş bir birim işaretlenir ancak yerel olarak sabitlenmiş tooa dönüştürme birim başarısız katmanlı, (veri toohello bulut geçmiş çünkü) benzer şekilde, bu bir katmanlı birim olarak çalışacaktır. Ancak, hello cihaz yerel katmanlarda hello toooccupy alanı devam eder. Bu alan diğer yerel olarak sabitlenmiş birimler için kullanılamaz. Merhaba birimi dönüştürme işlemi tamamlandığında ve hello cihazda yerel alan hello alınabilmesini bu işlemi tooensure yeniden deneme öneririz.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Yerel olarak sabitlenmiş bir birim geri yükleme hakkında sorular
**S.** Yerel olarak sabitlenmiş birimlerin anında geri olan?

**C.** Evet, yerel olarak sabitlenmiş birimlerin anında geri yüklenir. Merhaba birim Hello meta veri bilgilerini hello buluttan hello geri yükleme işleminin bir parçası olarak çekilir hemen hello birim çevrimiçi olana ve hello ana bilgisayar tarafından erişilebilir. Ancak, yerel GARANTİLERİN hello birim için verileri tüm hello indirilen veri hello buluttan ve karşılaşabileceğiniz kadar mevcut olmaz hello süresi hello geri yükleme için bu birimlerdeki performans azalır.

**S.** Yerel olarak sabitlenmiş bir birim toorestore ne kadar sürer?

**C.** Yerel olarak sabitlenmiş birimlerin anında geri ve toobe hello arka planda indirilir hello birim verilerini devam ederken hello birim meta veri bilgileri hello buluttan alınır hemen çevrimiçi. Bu ikinci bölümü hello geri yükleme işlemi--hello yerel GARANTİLERİN hello birim verileri--geri alamazsınız uzun süren bir işlemdir ve yeniden yerel yapılan tüm hello veri toobe için birkaç saat sürebilir. aynı geri yüklenen hello birimin boyutunu hello gibi birden çok etkene bağlıdır ve kullanılabilir bant genişliğini hello hello geçen süre toocomplete hello. Geri yüklenen hello özgün birimin sildiyseniz ek zaman toocreate hello hello geri yükleme işleminin parçası olarak hello cihazda yerel alan ulaşabilirsiniz.

**S.** My varolan yerel olarak sabitlenmiş (Merhaba birim katmanlı gerçekleştirilecek) birim tooan eski anlık görüntüsü toorestore ihtiyacım. Bu durumda katmanlı gibi Hello birim geri yüklenecek?

**C.** Hayır, hello birim yerel olarak sabitlenmiş bir birim geri yüklenir. Hello tarihleri toohello zaman zaman hello birim, var olan birimler, geri yükleme sırasında katmanlı anlık görüntü rağmen şu anda mevcut olduğundan StorSimple birim hello türünü hello disk üzerinde her zaman kullanır.

**S.** My yerel olarak sabitlenmiş bir birim son genişletilmiş ancak şimdi toorestore hello veri tooa zaman zaman hello birim boyutu daha küçük gerekir. Geri yükleme hello geçerli birim yeniden boyutlandırma ve hello geri yükleme tamamlandıktan sonra tooextend hello hello birimin boyutunu gerekir?

**C.** Evet, hello geri yükleme hello birim yeniden boyutlandırma ve hello geri yükleme tamamlandıktan sonra tooextend hello hello birimin boyutunu gerekir.

**S.** Geri yükleme sırasında bir birimin hello türü değiştirebilir miyim?

**A.**Hayır, geri yükleme sırasında hello birim türünü değiştiremezsiniz.

* Silinmiş birimleri hello anlık depolanan hello türü olarak geri yüklenir.
* Var olan birimler geri yüklenir hello anlık saklanan hello türü ne olursa olsun geçerli tipine göre (toohello önceki iki soruları bakın).

**S.** My yerel olarak sabitlenmiş bir birim toorestore ihtiyacım ancak ı yanlış noktanız zaman anlık Çekildi. Merhaba geçerli geri yükleme işlemi iptal edebilir miyim?

**C.** Evet, devam eden geri yükleme işlemini iptal edebilirsiniz. Merhaba biriminin Hello durumunu hello hello geri yükleme başlangıcında toohello durumu geri alınacak. Ancak, hello geri yükleme devam ederken toohello birim yapılan yazma kaybolur.

**S.** My yerel olarak sabitlenmiş birimlerin birinde bir geri yükleme işlemi başlatıldı ve anlık görüntü oluşturma recollect yok my biriktirme listesi kataloğunda şimdi görüyorum. Ne için kullanılır?

**C.** Bu, önceki toohello geri yükleme işlemi oluşturulur ve hello geri yükleme iptal edildi veya başarısız durumda geri almak için kullanılan hello geçici anlık görüntüsüdür. Bu anlık görüntü silmeyin; Merhaba geri yükleme tamamlandıktan sonra otomatik olarak silinir. Bu davranış, geri yükleme işi birimleri veya yerel olarak sabitlenmiş ve katmanlı birimlerin bir karışımını yalnızca yerel olarak sabitlenmiş ortaya çıkabilir. Merhaba geri yükleme işi yalnızca katmanlı birimleri içeriyorsa, bu davranış gerçekleşmez.

**S.** Yerel olarak sabitlenmiş bir birim kopyalamak?

**C.** Evet, kullanabilirsiniz. Ancak, yerel olarak sabitlenmiş hello birim katmanlı birim varsayılan olarak kopyalanma. Hakkında daha fazla bilgi çok[yerel olarak sabitlenmiş bir birim kopyalama](storsimple-8000-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Yerel olarak sabitlenmiş bir birim yapabilmesini hakkında sorular
**S.** Cihaz my tooanother fiziksel aygıt toofail ihtiyacım. My yerel olarak sabitlenmiş birimleri üzerinde yerel olarak sabitlenmiş veya katmanlı başarısız?

**C.** Merhaba yerel olarak sabitlenmiş birimleri hello hedef cihaz StorSimple 8000 serisi güncelleştirme 3 veya üstü çalışıyorsa, yerel olarak sabitlenmiş yük devredildi.

Daha fazla bilgi [yük devretme ve kurtarma, yerel olarak sabitlenmiş birimleri sürümleri arasında](storsimple-8000-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**S.** Yerel olarak sabitlenmiş birimlerin anında olağanüstü durum kurtarma (DR) sırasında geri yüklenir?

**C.** Evet, yerel olarak sabitlenmiş birimlerin anında yük devretme sırasında geri yüklenir. Merhaba birim Hello meta veri bilgilerini hello buluttan hello yük devretme işleminin bir parçası çekilir hemen hello birim hello hedef cihazda çevrimiçi olana ve hello ana bilgisayar tarafından erişilebilir. Bu sırada, hello birim verilerini toodownload hello arka planda devam eder ve hello süresi hello yük devretme için bu birimlerdeki azaltılmış performansla karşılaşabilirsiniz.

**S.** Tamamlanan hello yük devretme işine bakın, nasıl ı hello hedef cihazda geri yüklenen yerel olarak sabitlenmiş bir birim hello ilerlemesini izleyebilirsiniz?

**C.** Merhaba yük devretme kümesindeki tüm hello birimleri alınan anında geri ve hello hedef cihazda çevrimiçine sonra Yük devretme işlemi sırasında hello yük devretme iş tamamlandı olarak işaretlenir. Üzerinden başarısız tüm yerel olarak sabitlenmiş birimler de buna dahildir; Merhaba birim için tüm hello veri yüklenen ancak, yerel GARANTİLERİN hello veri yalnızca kullanılabilir. Merhaba yük devretme bir parçası olarak oluşturulan hello karşılık gelen geri yükleme işleri izleme tarafından devralınırsa başarısız oldu her yerel olarak sabitlenmiş bir birim için bu ilerleme durumunu izleyebilirsiniz. Bu tek tek geri yükleme işleri, yalnızca yerel olarak sabitlenmiş birimler için oluşturulur.

**S.** Yük devretme sırasında bir birimin hello türü değiştirebilir miyim?

**C.** Hayır, bir yük devretme sırasında hello birim türünü değiştiremezsiniz. Başarısız olan StorSimple 8000 serisi çalıştıran tooanother fiziksel aygıt güncelleştirme 3, hello birimleri hello anlık depolanan hello birim türüne göre yük devredildi.

**S.** Birim kapsayıcısı üzerinde yerel olarak sabitlenmiş birimlerin toohello bulut uygulaması ile başarısız olabilir?

**C.** Evet, kullanabilirsiniz. Merhaba yerel olarak sabitlenmiş birimleri üzerinde katmanlı birimler olarak devredilir. Daha fazla bilgi [yük devretme ve kurtarma, yerel olarak sabitlenmiş birimleri sürümleri arasında](storsimple-8000-device-failover-disaster-recovery.md#common-considerations-for-device-failover)

