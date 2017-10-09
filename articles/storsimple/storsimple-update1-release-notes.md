---
title: "aaaStorSimple 8000 serisi güncelleştirme 1.2 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler, sorunlar ve geçici çözümler için StorSimple 8000 serisi güncelleştirme 1.2 açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>1.2 sürüm notları, StorSimple 8000 serisi cihazınız için güncelleştirme

## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello yeni özellikleri açıklar ve hello kritik açık sorunlar için StorSimple 8000 serisi güncelleştirme 1.2 tanımlayın. Bunlar ayrıca hello StorSimple yazılım, sürücü ve disk Bellenim güncelleştirmeleri bu sürümde dahil listesini içerir. 

Güncelleştirme 1.2 sürümü (GA), güncelleştirme 0.1, güncelleştirme 0.2 veya Update 0.3 yazılımı çalıştıran uygulanan tooany StorSimple cihazı olabilir. Cihazınızı güncelleştirme 1 veya güncelleştirme 1.1 çalışıyorsa, güncelleştirme 1.2 kullanılamaz. Cihazınızı sürüm (GA) çalışıyorsa, lütfen [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) tooassist, bu güncelleştirme yükleme.

Aşağıdaki tablo listeleri hello aygıt yazılım sürümleri tooUpdates 1, 1.1 ve 1.2 karşılık gelen hello.

| Güncelleştirme çalıştırılıyorsa... | Bu, cihaz yazılım sürümüdür. |
| --- | --- |
| 1.2 güncelleştir |6.3.9600.17584 |
| Güncelleştirme 1.1 |6.3.9600.17521 |
| Güncelleştirme 1.0 |6.3.9600.17491 |

Lütfen StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello sürümde bulunan hello bilgileri gözden geçirin. Daha fazla bilgi için bkz. nasıl çok[StorSimple Cihazınızda güncelleştirme 1.2 yükleme](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Bu güncelleştirme (Windows hello güncelleştirmeleri dahil) yaklaşık 5-10 saat tooinstall sürer. 
> * Güncelleştirme 1.2 yazılım, LSI sürücü ve disk Bellenim güncelleştirmeleri içerir. tooinstall, izleme hello yönergeleri [StorSimple Cihazınızda güncelleştirme 1.2 yükleme](storsimple-install-update-1.md).
> * Yeni sürümler için güncelleştirmelerinin göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Yeniden birkaç gün içinde güncelleştirmeleri taramak üzere olarak yakında kullanılabilir hale gelecektir.
> 
> 

## <a name="whats-new-in-update-12"></a>Güncelleştirme 1.2 yenilikler nelerdir?
Bu özellikler, güncelleştirme 1 ile birlikte kullanıcılar sınırlı yapılmış kullanılabilir tooa kümesi ilk yayımlanmıştır. Merhaba güncelleştirme 1.2 sürümle birlikte, yeni özellikler ve geliştirmeler aşağıdaki hello hello StorSimple kullanıcıların çoğunun görür:

* **5000-7000 Serisi too8000 serisi cihazlar geçişini** – bu sürümde kendi veri tooa StorSimple 8000 serisi fiziksel Gereci hello StorSimple 5000-7000 Serisi Gereci kullanıcılar toomigrate olanak tanıyan yeni bir geçiş özelliği sunmaktadır veya Sanal gereç. Merhaba geçiş özelliğini iki anahtar değer önermeleri sahiptir:                                                                  
  
  * **İş sürekliliği**, 5000-7000 Serisi cihazları too8000 serisi cihazları üzerinde mevcut verilerin geçişini etkinleştirerek.
  * **Merhaba 8000 serisi cihazları özelliği teklifler geliştirilmiş**, verimli Merkezi Yönetimi StorSimple Yöneticisi hizmeti aracılığıyla birden çok Gereçleri gibi daha iyi donanım sınıfı ve güncelleştirilmiş üretici yazılımı, sanal gereçler, veri mobility ve hello gelecekteki yol haritası özellikleri.
    
    Toohello başvuran [Geçiş Kılavuzu](http://www.microsoft.com/download/details.aspx?id=47322) hakkında ayrıntılar için toomigrate StorSimple 5000-7000 Serisi tooan 8000 serisi cihazı. 
* **Hello Azure kamu Portal kullanılabilirlik** – StorSimple artık hello Azure kamu Portalı'nda kullanılabilir durumdadır. Bkz. nasıl çok[hello Azure kamu portalı bir StorSimple cihazı dağıtma](storsimple-deployment-walkthrough-gov.md).
* **Diğer bulut hizmeti sağlayıcıları için destek** – hello Amazon S3, Amazon S3 RRS, HP ve OpenStack (beta) ile desteklenen diğer bulut hizmeti sağlayıcıları şunlardır.
* **Toolatest depolama API'leri güncelleştirme** – bu sürümle birlikte, StorSimple bırakıldı toohello en son Azure depolama hizmeti API güncelleştirildi. Güncelleştirme 1 yazılımı sürümlerini çalıştıran StorSimple 8000 serisi cihazlar (sürüm, 0.1, 0.2 ve 0.3) hello Azure depolama hizmeti API'leri 17 Temmuz 2009'dan eski sürümlerini kullanan. Güncelleştirilmiş hello belirtildiği gibi [depolama hizmeti sürümleri kaldırma hakkında bildiri](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), bu API'leri 1 Ağustos 2016'da kullanım dışı kalacaktır. 2016 hello StorSimple 8000 serisi güncelleştirme 1 önceki tooAugust 1, geçerli zorunludur. Toodo nedenle başarısız olursa, StorSimple cihazları düzgün durdurur.
* **Bölge olarak yedekli depolama (ZRS için) desteği** – hello yükseltme toohello en son sürümüyle hello depolama API'leri, hello StorSimple 8000 serisi bölge olarak yedekli depolama (ZRS) toplama tooLocally yedekli depolama (LRS) içinde ve coğrafi olarak yedekli destekler Depolama (GRS). Toothis başvuran [Azure depolama artıklığı seçeneği makale](../storage/common/storage-redundancy.md) ZRS Ayrıntılar için.
* **İlk dağıtım ve güncelleştirme deneyimini Gelişmiş** – bu sürümde, yükleme hello ve güncelleştirme işlemleri geliştirilmiştir. Merhaba ağ yapılandırması ve güvenlik duvarı ayarları doğru değilse hello hello Kurulum Sihirbazı aracılığıyla geliştirilmiş tooprovide geri bildirim toohello kullanıcı yüklemesidir. Ek tanılama cmdlet'leri toohelp sağlandı, ağ hello aygıtının sorun giderme. Merhaba bkz [deployment makalesi sorun giderme](storsimple-troubleshoot-deployment.md) sorun giderme için kullanılan hello yeni tanılama cmdlet'leri hakkında daha fazla bilgi.

## <a name="issues-fixed-in-update-12"></a>Güncelleştirme 1.2 ile giderilen sorunlar
Aşağıdaki tablonun hello güncelleştirmeleri 1.2, 1.1 ve 1 düzeltilen sorunlardan özetini sağlar.    

| Hayır. | Özellik | Sorun | Düzeltilen güncelleştirme | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |StorSimple için Windows PowerShell |Bir kullanıcı hello StorSimple cihaz StorSimple için Windows PowerShell kullanarak uzaktan eriştikten ve hello Kurulum Sihirbazı'nı kullanmaya çalışırken bir kilitlenme IP giriş veri 0 olan en kısa sürede oluştu. Bu hata artık güncelleştirme 1'de düzeltilmiştir. |Güncelleştirme 1 |Evet |Evet |
| 2 |Fabrika sıfırlaması |Bazı durumlarda, bir Fabrika sıfırlaması gerçekleştirildiğinde hello StorSimple cihazı takılmış hale geldi ve bu ileti görüntülenir: **sıfırlama toofactory devam ediyor (aşama 8)**. Merhaba cmdlet devam ederken CTRL + C basıldıysa bu oldu. Bu hata artık giderilmiştir. |Güncelleştirme 1 |Evet |Hayır |
| 3 |Fabrika sıfırlaması |Başarısız çift denetleyici üretecini sıfırladıktan sonra cihaz kaydı ile tooproceed izin verildi. Desteklenmeyen Sistem Yapılandırması'nda sonuçlandı. Güncelleştirme 1'in bir hata iletisi gösterilir ve kayıt başarısız fabrika ayarlarına sıfırladı bir aygıtta engellendi. |Güncelleştirme 1 |Evet |Hayır |
| 4 |Fabrika sıfırlaması |Bazı durumlarda yanlış pozitif uyuşmazlığı uyarılar ortaya çıktı. Yanlış uyuşmazlığı uyarıları artık güncelleştirme 1 çalıştıran cihazlarda oluşturulur. |Güncelleştirme 1 |Evet |Hayır |
| 5 |Fabrika sıfırlaması |Fabrika sıfırlamasına kesildiyse, önceki toocompletion girilen aygıt kurtarma moduna hello ve StorSimple için Windows PowerShell tooaccess izin vermedi. Bu hata artık giderilmiştir. |Güncelleştirme 1 |Evet |Hayır |
| 6 |Olağanüstü durum kurtarma |Bir olağanüstü durum kurtarma (DR) hata; burada görüntülerle DR hello hedef aygıt yedeklemelerin hello bulma sırasında başarısız olacağı giderilmiştir. |Güncelleştirme 1 |Evet |Evet |
| 7 |İzleme LED'leri |Bazı durumlarda, hello Gereci arkasına adresindeki LED'leri izleme doğru durum yazılmasını belirtmedi. Merhaba mavi LED kapalıdır. Veri 0 ve veri 1 LED'leri bile ne zaman bu arabirimleri yapılandırılmamış yanıp. Merhaba sorun çözüldükten ve izleme LED'leri şimdi hello doğru durumunu gösterir. |Güncelleştirme 1 |Evet |Hayır |
| 8 |İzleme LED'leri |Bazı durumlarda, güncelleştirme 1'i uyguladıktan sonra hello mavi ışık hello etkin denetleyicisinde'böylece sabit tooidentify hello etkin denetleyicisi yapma açık. Bu düzeltme eki sürümde bu sorun düzeltilmiştir. |1.2 güncelleştir |Evet |Hayır |
| 9 |Ağ arabirimleri |Önceki sürümlerde yönlendirilemeyen bir ağ geçidi ile yapılandırılmış bir StorSimple cihazı çevrimdışı duruma. Bu sürümde, Data 0 için bir yönlendirme metriği hello hello düşük bulunuldu; Bu nedenle, diğer ağ arabirimleri bulut etkin olsa bile, tüm hello bulut trafiği hello aygıttan veri 0 yönlendirilir. |Güncelleştirme 1 |Evet |Evet |
| 10 |Yedeklemeler |24 gün sabit sonra yedeklemeler toofail hello düzeltme neden güncelleştirme 1 hatada güncelleştirme 1.1 bırakın. |Güncelleştirme 1.1 |Evet |Evet |
| 11 |Yedeklemeler |Önceki sürümlerde bir hata performansın düşük değişiklik oranları ile bulut anlık görüntüleri için ile sonuçlandı. Bu hata, bu düzeltme eki sürümde düzeltilmiştir. |1.2 güncelleştir |Evet |Evet |
| 12 |Güncelleştirmeler |Başarısız yükseltmeyi bildirilen ve kurtarma moduna hello denetleyicileri toogo neden güncelleştirme 1'in bir hata sabit bu düzeltme eki sürümde. |1.2 güncelleştir |Evet |Evet |

## <a name="known-issues-in-update-12"></a>Güncelleştirme 1.2 bilinen sorunlar
Aşağıdaki tablonun hello bu sürümdeki bilinen sorunlara özetini sağlar.

| Hayır. | Özellik | Sorun | Yorumlar/geçici çözüm | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |Disk çekirdek |Hiçbir disk çekirdek kaynaklanan hello EBOD muhafazası 8600 aygıtının diskleri Hello çoğunluğu bağlantısı kesildiyse nadir durumlarda, ardından hello depolama havuzu çevrimdışı olur. Merhaba diskleri bağlanırlar olsa bile çevrimdışı kalır. |Tooreboot hello aygıt gerekir. Merhaba sorun devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 2 |Yanlış denetleyici kimliği |Bir denetleyici değiştirme gerçekleştirildiğinde, denetleyici 0 denetleyicisi 1 olarak görünebilirler. Merhaba görüntü hello eş düğümden yüklendiğinde denetleyicisi değiştirme sırasında hello denetleyici kimliği başlangıçta hello eş denetleyicinin kimliği olarak gösterebilir Nadir durumlarda, bu davranış bir sistem yeniden başlatıldıktan sonra görülebilir. |Hiçbir kullanıcı eylemi gerekli değildir. Merhaba denetleyicisi değiştirme işlemi tamamlandıktan sonra bu durum kendisini çözümleyin. |Evet |Hayır |
| 3 |Depolama hesapları |Merhaba depolama hizmeti toodelete hello depolama hesabı kullanarak desteklenmeyen bir senaryodur. Bu kullanıcı verileri alınamıyor tooa durum götürür. |Evet |Evet | |
| 4 |Cihaz yük devretme |Aynı kaynak aygıt toodifferent hedef cihazlar desteklenmiyor hello birim kapsayıcıdan birden çok yük. Cihaz yük devretme tek ölü aygıt toomultiple aygıtlardan veri sahipliği kaybetmek hello birim kapsayıcıları ilk aygıt üzerinden başarısız hello üzerinde hale getirir. Bu tür bir yük devretme sonrasında, bu birim kapsayıcıları görünür veya hello Klasik Azure portalında görüntülediğinizde farklı şekilde davranır. | |Evet |Hayır |
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

## <a name="physical-device-updates-in-update-12"></a>Güncelleştirme 1.2 fiziksel aygıt güncelleştirmeleri
Düzeltme eki güncelleştirme 1.2 uygulanan tooa fiziksel aygıt (sürümleri önceki tooUpdate 1 çalıştıran) ise hello yazılım sürüm too6.3.9600.17584 değiştirin.

## <a name="controller-and-firmware-updates-in-update-12"></a>Güncelleştirme 1.2 denetleyici ve bellenim güncelleştirmeleri
Bu sürüm hello sürücü ve hello disk cihazınızın bellenimini güncelleştirir.

* Merhaba SAS denetleyicisi güncelleştirmesi hakkında daha fazla bilgi için bkz: [Microsoft Azure StorSimple Gereci LSI SAS denetleyicileri için Güncelleştirme 1](https://support.microsoft.com/kb/3043005). 
* Merhaba disk bellenim güncelleştirme hakkında daha fazla bilgi için bkz: [Microsoft Azure StorSimple Gereci için Disk bellenim güncelleştirme 1](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Güncelleştirme 1.2 sanal aygıt güncelleştirmeleri
Bu güncelleştirme uygulanan toohello sanal aygıt olamaz. Yeni sanal cihazların oluşturulan toobe gerekir. 

## <a name="next-steps"></a>Sonraki adımlar
* [Güncelleştirme 1.2 yüklemeniz](storsimple-install-update-1.md).

