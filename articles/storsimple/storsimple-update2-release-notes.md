---
title: "aaaStorSimple 8000 serisi güncelleştirme 2 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler, sorunlar ve geçici çözümler için StorSimple 8000 serisi güncelleştirme 2 açıklar."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>StorSimple 8000 serisi güncelleştirme 2 sürüm notları
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello yeni özellikleri açıklar ve hello kritik açık sorunlar için StorSimple 8000 serisi güncelleştirme 2 tanımlayın. Ayrıca hello StorSimple yazılım listesi, sürücü ve disk Bellenim güncelleştirmeleri bu sürümde dahil içerirler. 

Güncelleştirme 2 sürüm (GA) veya güncelleştirme 0.1 güncelleştirme 1.2 çalışan uygulanan tooany StorSimple cihazı olabilir. Güncelleştirme 2 ile ilişkili hello aygıt 6.3.9600.17673 sürümüdür.

Lütfen StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello sürümde bulunan hello bilgileri gözden geçirin.

> [!IMPORTANT]
> * Bu güncelleştirme (Merhaba Windows güncelleştirmeleri de dahil olmak üzere) yaklaşık 4-7 saat tooinstall sürer. 
> * Güncelleştirme 2 yazılım, LSI sürücü ve SSD Bellenim güncelleştirmeleri içerir.
> * Yeni sürümler için güncelleştirmelerinin göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Birkaç gün bekleyin ve ardından güncelleştirmeleri taramak üzere yeniden bunlar olarak yakında kullanılabilir hale gelecektir.
> 
> 

## <a name="whats-new-in-update-2"></a>Güncelleştirme 2'deki yenilikler
Güncelleştirme 2 hello aşağıdaki yeni özellikleri sunar.

* **Birimler'yerel olarak sabitlenmiş** – hello StorSimple 8000 serisi önceki sürümlerde kullanıma dayalı katmanlı toohello bulut veri bloklarını olan. Blokları yerel kalmasını hiçbir şekilde tooguarantee vardı. Bir birim oluştururken yerel olarak sabitlenmiş ve birincil veri birimden katmanlı toohello bulut olmaz gibi güncelleştirme 2'de, bir birim belirleyebilirsiniz. Yerel olarak sabitlenmiş birimlerin anlık görüntüleri çıkarılsın hello bulut veri mobility ve olağanüstü durum kurtarma işlemleri için kullanılır böylece toohello bulut yedekleme için kopyalanır. Ayrıca, hello birim türünü değiştirebilirsiniz (diğer bir deyişle, katmanlı birimleri sabitlenmiş toolocally birimi dönüştürmek ve dönüştürme yerel olarak sabitlenmiş birimleri tootiered). 
* **StorSimple sanal cihazı geliştirmeleri** – hello StorSimple 8000 serisi hello sanal cihaz bir olağanüstü durum kurtarma ya da geliştirme ve test çözümü olarak daha önce konumlandırıldı. Sanal cihazı (modeli 1100) yalnızca bir model vardı. Güncelleştirme 2 iki sanal aygıt modeli sunar: 
  
  * 8010 (önceden çağrılan hello 1100) – değişiklik yok; 30 TB kapasitesine sahip ve Azure standard storage kullanır.
  * 8020 – 64 TB'lık bir kapasitesine sahiptir ve iyileştirilmiş performans için Azure Premium storage kullanır.
    
    Her iki sanal aygıt modelleri (8010/8020) için tek bir VHD yoktur. Merhaba sanal cihaz ilk kez başlattığınızda, hello platform parametreleri algılar ve hello doğru model sürümü geçerlidir.
* **Ağ iyileştirmeleri** – güncelleştirme 2 ağ iyileştirmeleri aşağıdaki hello içerir:
  
  * Yük devretme, bir NIC başarısız olursa gerçekleştirilmesi birden çok NIC hello bulut için etkinleştirilebilir.
  * Bulut için sabit ölçümlerle yönlendirme geliştirmeleri blokları etkin.
  * Bir yük devretme önce başarısız kaynaklarının çevrimiçi yeniden deneyin.
  * Hizmet hataları için yeni uyarıları.
* **Geliştirmeleri güncelleştirme** – 1.2 güncelleştirmek ve hello StorSimple 8000 serisi iki kanallar daha önce güncelleştirildi: Windows Update kümeleme, iSCSI ve benzeri ve ikili dosyaları ve bellenim için Microsoft Update için.
    Tüm güncelleştirme paketlerinin güncelleştirme 2 Microsoft Update kullanılır. Bu, yük devretme işlemlerini yaparken veya düzeltme eki uygulama tooless zaman yol. 
* **Bellenim güncelleştirmeleri** – hello Bellenim güncelleştirmeleri eklenmiştir:
  
  * LSI: lsi_sas2.sys ürün sürümü 2.00.72.10
  * Yalnızca SSD (HDD güncelleştirme yok): XMGG, XGEG, KZ50, F6C2 ve VR08
* **Öngörülü Destek** – güncelleştirme 2 Microsoft toopull ek tanılama bilgilerinin hello aygıttan sağlar. Sorunlarınız aygıtları operations ekibimiz belirlediğinde, biz hello aygıttan daha iyi donanımlı toocollect bilgileri sorunlarını tanılamak ve. **Güncelleştirme 2 kabul ederek, bize tooprovide izin öngörülü Bu destek**.    

## <a name="issues-fixed-in-update-2"></a>Güncelleştirme 2'de giderilen sorunlar
Aşağıdaki tablolar hello güncelleştirme 2'de düzeltilen sorunlardan özetini sağlar.    

| Hayır. | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Ağ arabirimleri |Bir yükseltme tooUpdate sonra 1, hello StorSimple Yöneticisi hizmeti hello veri2 ve Data3 bağlantı noktaları bir denetleyicisinde başarısız olduğunu bildirdi. Bu sorun düzeltilmiştir. |Evet |Hayır |
| 2 |Güncelleştirmeler |Bir yükseltme tooUpdate sonra 1, Klasik Azure portalı birden çok aygıta hello sesli alarm uyarılar oluştu. Bu sorun düzeltilmiştir. |Evet |Hayır |
| 3 |Openstack kimlik doğrulaması |Openstack bulut hizmeti sağlayıcısı olarak kullanırken, bulut kimlik doğrulama dizesi çok uzun bir hata alabilir. Bu düzeltilmiştir. |Evet |Hayır |

## <a name="known-issues-in-update-2"></a>Güncelleştirme 2 bilinen sorunlar
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
| 20 |Yerel olarak sabitlenmiş birimleri |Tooconvert (oluşturulan ve güncelleştirme 1.2 ile kopyalanan veya öncesi) katmanlı birim çalışırsanız tooa yerel olarak sabitlenmiş birim ve Cihazınızı alana sahip değil veya bir bulut kesinti yoktur ve sonra hello clone(s) bozulmuş. |Bu sorun, oluşturulan ve kopyalanan ile güncelleştirme öncesi 2 yazılım olan birimlerle oluşur. Bu, seyrek bir senaryo olmalıdır. | | |
| 21 |Birim dönüştürme |Bir birim dönüştürme işlemi devam ederken hello ACRs ekli tooa toplu güncelleştirmeyi (katmanlı toolocally sabitlenmiş veya tersi). Merhaba ACRs güncelleştirme veri bozulmasına neden olabilir. |Gerekirse, hello ACRs önceki toohello birim dönüştürme güncelleştirin ve hello dönüştürme işlemi devam ederken ACR güncelleştirmeleri başka yapmayın. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Güncelleştirme 2 denetleyicisi ve bellenim güncelleştirmeleri
Bu sürüm hello sürücü ve hello disk cihazınızın bellenimini güncelleştirir.

* Güncelleştirmesi hello LSI bellenim hakkında daha fazla bilgi için Microsoft Bilgi Bankası makalesi 3121900. 
* Güncelleştirmesi hello disk bellenim hakkında daha fazla bilgi için Microsoft Bilgi Bankası makalesi 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Güncelleştirme 2'deki sanal aygıt güncelleştirmeleri
Bu güncelleştirme uygulanan toohello sanal aygıt olamaz. Yeni sanal cihazların oluşturulan toobe gerekir. 

## <a name="next-step"></a>Sonraki adım
Nasıl çok öğrenin[güncelleştirme 2'yi yükleme](storsimple-install-update-2.md) , StorSimple Cihazınızda.

