---
title: "aaaStorSimple 8000 güncelleştirme 0,1 sürüm notları | Microsoft Docs"
description: "Ekim 2014 Hello yeni özellikler ve düzeltmeler, açık sorunlar ve hello için kullanılabilir geçici çözümler açıklanmaktadır Microsoft Azure StorSimple sürüm (güncelleştirme 0.1)."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>StorSimple 8000 serisi güncelleştirme 0,1 sürüm notları – Ekim 2014
## <a name="overview"></a>Genel Bakış
Sürüm Notları aşağıdaki hello hello kritik açık sorunlar StorSimple 8000 serisi güncelleştirme 0.1 Ekim 2014'te yayımlanan için belirleyin. Bunlar ayrıca hello StorSimple yazılım listesi ve bu sürümde dahil Bellenim güncelleştirmeleri içerir. Merhaba StorSimple 8000 serisi yayın sürümü Temmuz 2014'te genel olarak kullanılabilir yapıldı ve toosoftware sürüm 6.3.9600.17312 karşılık gelen sonra hello ilk sürüm budur.  

Tarama ve hello cihaz yüklendikten hemen sonra kullanılabilir güncelleştirmeleri uygulamak öneririz. Ayrıca, Otomatik Güncelleştirmeler toodownload üzerinde açmak ve kullanıma sunulduklarında hemen Microsoft'tan yüksek öncelikli güncelleştirmeleri yükleyin. Daha fazla bilgi için bkz. nasıl çok[StorSimple Cihazınızı güncelleştirin](storsimple-update-device.md).  

Lütfen StorSimple çözümünüzde hello güncelleştirmelerini dağıtmadan önce hello Sürüm Notları'nda bulunan hello bilgileri gözden geçirin.  

> [!IMPORTANT]
> * Merhaba StorSimple Yöneticisi hizmeti ve Windows PowerShell için StorSimple tooinstall hello Ekim güncelleştirmeleri kullanın.  
> * Merhaba güncelleştirmeler genellikle yaklaşık 3 saat toocomplete sürer.  
> * Merhaba StorSimple Ekim sürümünü tüm güncelleştirmeleri toohello StorSimple sanal cihazı içermiyor. Hala en son güvenlik düzeltmeleri de dahil olmak üzere tüm kullanılabilir Windows güncelleştirmelerini uygulayabilirsiniz, ancak sürüm hello sanal cihaz için bir değişiklik görmez.  
> 
> 

Önkoşullar emin hello olun ölç önceki tooupdating StorSimple Cihazınızı şunlardır.  

* Güncelleştirmeleri taramadan önce her iki aygıt denetleyicileri çalıştığından emin olun. Her iki denetleyicisi çalışmıyorsa hello tarama başarısız olur. Merhaba denetleyicileri sağlıklı bir durumda olan tooverify gidin çok**donanım durumu** hello altında **Bakım** sayfası. Bileşenleri varsa, **dikkat etmeniz gereken**, başka bir işlem yapmadan önce Microsoft Support başvurun.  
* Sabit IP'ler için her iki denetleyici 0 ve denetleyici 1 yönlendirilebilir ve bunlar hello güncelleştirmeleri toohello aygıt bakım için kullanılan toohello Internet bağlanabilirsiniz emin olun. Merhaba kullanabilirsiniz [Bağlantıyı Sına cmdlet](https://technet.microsoft.com/library/hh849808.aspx) tooping bilinen bir adresi outlook.com, denetleyici hello tooverify gibi hello ağ dışında Ağ dışından bağlantı toohello sahiptir.  
* Bu hello gerekli giden iletişim için StorSimple Cihazınızda giden bağlantı noktaları bulunduğundan emin olun. Daha fazla bilgi için bkz: Merhaba [StorSimple cihazınız için ağ gereksinimleri](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Merhaba aygıt yazılım sürümü (Ekim 2014 güncelleştirmesi) 6.3.9600.17312 eskiyse hello veri 2 ve veri 3 bağlantı noktaları, hello güncelleştirmeden önce etkinleştirilirse, devre dışı bırakın. Başlangıç veri 2 ve veri 3 hello güncelleştirme uygulanırken etkin bağlantı noktalarını değiştirmeden bırakırsanız, kurtarma moduna cihaz denetleyicisi toogo neden olabilir. Lütfen hello ağ arabirimlerini devre dışı bıraktığınızda tüm ilişkili hello birimlerin çevrimdışına alınır ve hello g/ç hello güncelleştirmesi süresi boyunca hello kesilmiş olabilir unutmayın.  

## <a name="whats-new-in-hello-october-release"></a>Merhaba Ekim sürümde yenilikler
Bu güncelleştirme hello aşağıdaki geliştirmeleri içerir:

* Artık, aygıt denetleyicileri hello StorSimple Yöneticisi hizmeti kullanıcı Arabirimi toomanage kullanabilirsiniz. Merhaba yönetim eylemleri içerir, kapatma, yeniden başlatın veya bir denetleyicisinde kapatın. Daha fazla bilgi için çok Git[yönetmek StorSimple cihaz denetleyicilerinin](storsimple-manage-device-controller.md).  
* WAN bant genişliği ayırma tooday haftasını ve gününü zaman birleşimleri göre zamanlayabilirsiniz. Bu, toomake daha iyi WAN bant genişliği kullanımını saatlerde sağlar. Farklı bant genişliği şablonları farklı bir birim kapsayıcıları için izin verilir. Daha fazla bilgi için çok Git[StorSimple bant genişliği şablonlarınızı yönetmeye](storsimple-manage-bandwidth-templates.md).  
* E-posta bildirimleri tooproactively bildir hello yöneticileri ve diğerleri varolan veya büyük olasılıkla yaklaşan sorunları yapılandırabilirsiniz. Daha fazla bilgi için çok Git[uyarı ayarlarını yapılandırmak](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Merhaba Ekim sürümde giderilen sorunlar
Merhaba aşağıdaki tabloda bu güncelleştirmede giderilen sorunlar özetini sağlar.  

| Hayır. | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Ağ arabirimleri |Merhaba önceki sürüm, hello ağ arabirimleri veri 2 ve veri 3 hello yazılımda değiştirildi. Bu güncelleştirmede düzeltilmiştir. Lütfen hello ayarları temizleyin ve hello güncelleştirmeyi yüklemeden önce bu ağ arabirimlerini devre dışı bırakın. Merhaba güncelleştirmeyi yükledikten sonra bu arabirimleri tooreconfigure sahip olur. |Evet |Hayır |
| 2 |Destek Paketi |Windows PowerShell hello çalıştırdıysanız hello önceki sürümde, **verme HcsSupportPackage** cmdlet tooretrieve hello temel kart yönetim denetleyicisi (BMC) günlükleri, hello işlemi uyarı aşağıdaki hello ile başarısız oldu: "Merhaba işlemi bu denetleyicisinde başarılı oldu ancak hello eş denetleyicisi toohello aşağıdaki nedeniyle başarısız oldu hataları. Lütfen hello eş sağlıklı olup ve hello geçerli düğüm toohello eş bağlanabilir olup olmadığını denetleyin." Şimdi bu sorun giderilmiştir. |Evet |Hayır |
| 3 |Cihaz yük devretme |Merhaba önceki sürümde oluştu veri tutarsızlığı olasılığını varsa bir **yedekleme Bul** işi aygıt yük devretme sırasında başarısız oldu. Şimdi bu sorun giderilmiştir. |Evet |Hayır |
| 4 |Cihaz yük devretme |Merhaba önceki sürüm, aygıt yük devretme işleminden sonra yedeklemeler görünür ancak hello ilişkili birim kapsayıcısı hello hedef cihazda mevcut değildi. Şimdi bu sorun giderilmiştir. |Evet |Hayır |
| 5 |Cihaz yük devretme |Merhaba önceki sürümde, listedeki hello bulut yedeklerini bağlantı sorunları bulut olsaydı sağlayabilecek toodata tutarsızlık hello kayıt defterini geri yükleme işlemi sırasında bir hata vardı. |Evet |Hayır |
| 6 |Bellenim güncelleştirme |Merhaba önceki sürümdeki hello aygıt bellenim güncelleştirme işi başarısız oldu ve hello cmdlet'leri tanınabilir değil ve sonuç olarak bu hello güncelleştirme işlemi başarısız oldu belirtilen bir hata görüntülenir. Merhaba denetleyicisi sonra kurtarma moduna geçmiştir. Şimdi bu sorun giderilmiştir. |Evet |Hayır |
| 7 |Yükleme |Doğru yükleme sırasında görüntüsü değil hello aygıt tarafından kaynaklanan hataları şimdi düzeltildi. |Evet |Hayır |
| 8 |Fabrika sıfırlaması |Fabrika sıfırlaması için hello bellenim denetimi artık isteğe bağlı olarak atlayabilirsiniz. Bu, hello önceki sürümünden farklıdır. |Evet |Hayır |
| 9 |Fabrika sıfırlaması |Fabrika sıfırlaması cmdlet'ini çalıştırdığınızda hello önceki sürümde, yalnızca bazı donanım bileşenleri için bellenim sürümü denetimleri yapıldı. Ek bellenim denetimleri hello hello sıfırlama toofail neden olabilecek hello işlemindeki ilk yeniden başlatma işleminden sonra yapıldı. Bu düzeltme, tüm hello bellenim denetimleri hello Fabrika sıfırlaması cmdlet'ini çalıştırdığınızda ve hello önce ilk sistem yeniden yaptığını sağlar. |Evet |Hayır |
| 10 |Depolama hesabı anahtar döndürme |Merhaba **Invoke-HcsmServiceDataEncryptionKeyChange** kullanıcı tooenter hello hizmet verileri şifreleme anahtarı istemleri hello artık cmdlet kullanılan toorotate hello depolama hesabı anahtarları. Bu, hangi hello hizmet verileri şifreleme anahtarı bir satır içi parametre olarak geçirilen hello önceki sürümünden farklıdır. |Evet |Hayır |
| 11 |24 saat içinde geri dönme |Olağanüstü durum kurtarma sırasında hello temizleme hello kaynak aygıtta düzgün bir şekilde, neden geri dönme toofail gerçekleşmedi. Bu, bu sürümde düzeltilmiştir. |Evet |Hayır |

## <a name="known-issues-in-hello-october-release"></a>Merhaba Ekim sürümdeki bilinen sorunlar
Aşağıdaki tablonun hello bu sürümdeki bilinen sorunlara özetini sağlar.

| Hayır. | Özellik | Sorun | Yorumlar/geçici çözüm | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrika sıfırlaması |Bazı durumlarda, bir Fabrika sıfırlaması gerçekleştirdiğinizde hello StorSimple cihazı takılmış ve bu iletisini görüntüler: **sıfırlama toofactory devam ediyor (aşama 8)**. Merhaba cmdlet sürerken CTRL + C tuşlarına basın bu olur. |Fabrika sıfırlamasına başlatıldıktan sonra CTRL + C tuşlarına değil. Bu durumda zaten varsa, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 2 |Fabrika sıfırlaması |GA tooOctober 2014 sürümünden güncelleştirilmiş bir StorSimple cihazı Fabrika sıfırlaması yapın. |Bu işlem yalnızca bir düzeltme eki yüklüyse çalışır. Microsoft Support tooget bu gerekli bir düzeltme eki başvurun. |Evet |Hayır |
| 3 |Disk çekirdek |Hiçbir disk çekirdek kaynaklanan hello EBOD muhafazası 8600 aygıtının diskleri Hello çoğunluğu bağlantısı kesildiyse nadir durumlarda, ardından hello depolama havuzu çevrimdışı olur. Merhaba diskleri bağlanırlar olsa bile çevrimdışı kalır. |Tooreboot hello aygıt gerekir. Merhaba sorun devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 4 |Bulut anlık görüntü hataları |Nadir durumlarda, bir bulut anlık görüntüsü hello hatasıyla başarısız olabilir **maksimum yedekleme sınırına ulaşıldı**. Merhaba 255 çevrimiçi kopyada aşarsa bu gerçekleşir aynı aygıttan, hello silindi aynı özgün birimi. | |Evet |Evet |
| 5 |Yanlış denetleyici kimliği |Bir denetleyici değiştirme gerçekleştirildiğinde, denetleyici 0 denetleyicisi 1 olarak görünebilirler. Merhaba görüntü hello eş düğümden yüklendiğinde denetleyicisi değiştirme sırasında hello denetleyici kimliği başlangıçta hello eş denetleyicinin kimliği olarak gösterebilir Nadir durumlarda, bu davranış bir sistem yeniden başlatıldıktan sonra görülebilir. |Hiçbir kullanıcı eylemi gerekli değildir. Merhaba denetleyicisi değiştirme işlemi tamamlandıktan sonra bu durum kendisini çözümleyin. |Evet |Hayır |
| 6 |Cihaz izleme grafikleri |Hello StorSimple Yöneticisi hizmeti, hello cihaz izleme grafikleri basit çalışmıyor veya NTLM kimlik doğrulaması hello proxy sunucusu yapılandırmasını hello cihaz için etkinleştirilir. |Bu kimlik doğrulama tooNONE ayarlanır, StorSimple Yöneticisi hizmetine kayıtlı hello cihaz için Hello web proxy yapılandırması değiştirin. toodo StorSimple Set-HcsWebProxy cmdlet'i için bu, çalışma hello hello Windows PowerShell. |Evet |Evet |
| 7 |Depolama hesapları |Merhaba depolama hizmeti toodelete hello depolama hesabı kullanarak desteklenmeyen bir senaryodur. Bu kullanıcı verileri alınamıyor tooa durum götürür. | |Evet |Evet |
| 8 |Cihaz yük devretme |Aynı kaynak aygıt toodifferent hedef cihazlar desteklenmiyor hello birim kapsayıcıdan birden çok yük. |Yük devretme tek ölü aygıt toomultiple aygıtlardan veri sahipliği kaybetmek hello birim kapsayıcıları ilk aygıt üzerinden başarısız hello üzerinde hale getirir. Bu tür bir yük devretme sonrasında, bu birim kapsayıcıları görünür veya hello Klasik Azure portalında görüntülediğinizde farklı şekilde davranır. |Evet |Hayır |
| 9 |Yükleme |SharePoint yükleme için StorSimple bağdaştırıcısı sırasında tooprovide cihaz IP hello yükleme toofinish sırada başarıyla gerekir. | |Evet |Hayır |
| 10 |Web proxy |Web proxy yapılandırması varsa hello olarak HTTPS protokolü, belirtilen sonra aygıtı hizmeti iletişimi etkilenecek ve hello aygıt çevrimdışı. Destek paketleri aygıtınızda önemli miktarda kaynak tüketen hello işlemde de oluşturulur. |Belirtilen protokol hello gibi Hello web proxy URL'Sİ'ın HTTP olduğundan emin olun. Hakkında daha fazla bilgi çok[cihazınız için web Proxy'yi Yapılandır](storsimple-configure-web-proxy.md). |Evet |Hayır |
| 11 |Web proxy |Yapılandırma ve web proxy bir kayıtlı cihazda etkinleştirirseniz, Cihazınızda toorestart hello etkin denetleyicisine ihtiyacınız vardır. | |Evet |Hayır |
| 12 |Yüksek bulut gecikme süresi ve yüksek g/ç iş yükü |StorSimple Cihazınızı çok yüksek bulut gecikme (saniye sırasını) ve yüksek g/ç iş yükü bileşimini karşılaştığında, düzeyi düşürülmüş bir duruma hello aygıt birimleri gidin ve hello g/ç "cihaz hazır değil" hatası ile başarısız. |Toomanually yeniden başlatma hello cihaz denetleyicilerinin gerekir veya bir aygıt yük devretme toorecover bu durumdan gerçekleştirin. |Evet |Hayır |

## <a name="physical-device-updates-in-hello-october-release"></a>Merhaba Ekim sürümdeki fiziksel aygıt güncelleştirmeleri
Bu güncelleştirmeler uygulanan tooa fiziksel aygıt olduğunda hello yazılım sürüm too6.3.9600.17312 değiştirin. Aksi belirtilmediği sürece, bu sürüm notları hello StorSimple cihazı tooall modellerinin uygulayın. Bu güncelleştirmeler hakkında daha fazla bilgi için bkz: [Ekim 2014 fiziksel Gereci yazılım güncelleştirmesi için Microsoft Azure StorSimple Gereci](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Seri Bağlı SCSI (SAS) denetleyicisi ve bellenim güncelleştirmeleri hello Ekim sürümde
Bu sürüm hello sürücü ve fiziksel cihazınızın hello SAS denetleyicisinde hello bellenim güncelleştirir. Merhaba SAS denetleyicisi güncelleştirmesi hakkında daha fazla bilgi için bkz: [Microsoft Azure StorSimple Gereci LSI SAS denetleyicileri için Ekim 2014 güncelleştirmesi](http://support.microsoft.com/kb/2987020).   

Bu sürüm ayrıca hello aygıt donanım bileşenleriyle birlikte güvenilirlik sorunlarını ele toplu üretici yazılımı güncelleştirmesi için geçerlidir. Merhaba bellenim güncelleştirme hakkında daha fazla bilgi için bkz: [Microsoft Azure StorSimple Gereci Ekim 2014 üretici yazılımı güncelleştirmesi](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Sanal cihaz güncelleştirmeleri hello Ekim sürümde
Bu sürüm hello sanal cihaz için herhangi bir güncelleştirme içermiyor. Bu güncelleştirmeyi uyguladıktan sanal cihazı hello yazılımı sürümü değişmez.

