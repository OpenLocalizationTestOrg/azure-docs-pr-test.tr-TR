---
title: "aaaStorSimple 8000 güncelleştirme 0,3 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler ve düzeltmeler, açık sorunlar ve hello için kullanılabilir geçici çözümler Şubat 2015 açıklar Microsoft Azure StorSimple sürüm (güncelleştirme 0.3)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>StorSimple 8000 serisi güncelleştirme 0,3 sürüm notları - Şubat 2015
## <a name="overview"></a>Genel Bakış
Sürüm Notları aşağıdaki hello hello kritik açık sorunlar StorSimple 8000 serisi güncelleştirme 0.3 Şubat 2015'te yayımlanan için belirleyin. Bunlar ayrıca hello StorSimple yazılım listesi ve bu sürümde dahil Bellenim güncelleştirmeleri içerir. Merhaba StorSimple 8000 serisi yayın sürümü Temmuz 2014'te genel olarak kullanılabilir yapıldıktan sonra hello üçüncü sürüm budur.

Bu güncelleştirme hello aygıt yazılım sürümü hello Ocak Update'ten değiştirmez. Toobe sürüm 6.3.9600.17312 devam eder. Merhaba güncelleştirmenin yüklü olduğu hello denetleyerek doğrulayabilirsiniz **son güncelleştirilen** tarih. Başlangıç tarihi 2/10/2015 veya sonraki ise, hello güncelleştirme başarıyla yüklendi.  

Tarama ve StorSimple Cihazınızı yüklendikten hemen sonra kullanılabilir güncelleştirmeleri uygulamak öneririz. Ayrıca, Otomatik Güncelleştirmeler toodownload üzerinde açmak ve kullanıma sunulduklarında hemen Microsoft'tan yüksek öncelikli güncelleştirmeleri yükleyin. Daha fazla bilgi için bkz: [StorSimple Cihazınızı güncelleştirin](storsimple-update-device.md).  

Lütfen StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello sürümde bulunan hello bilgileri gözden geçirin.  

> [!IMPORTANT]
> * StorSimple tooinstall hello Şubat güncelleştirmesi Hello StorSimple Yöneticisi hizmeti ve Windows PowerShell kullanın.   
> * Bu güncelleştirme yaklaşık bir saat tooinstall sürer. Ancak, toplu güncelleştirmeler yüklüyorsanız, hello işlemi yaklaşık 3 saat toocomplete alabilir.  
> * Merhaba StorSimple Şubat sürümünü tüm güncelleştirmeleri toohello StorSimple sanal cihazı içermiyor. Yine de tüm kullanılabilir Windows güncelleştirmelerini toohello sanal aygıt uygulayabilir, de dahil olmak üzere en son güvenlik düzeltmeleri, ancak sürüm hello sanal cihaz için bir değişiklik görmez.  
> 
> 

Bu hello emin olun ölç önceki tooupdating StorSimple Cihazınızı önkoşullarıdır.  

* Güncelleştirmeleri taramadan önce her iki aygıt denetleyicileri çalıştığından emin olun. Her iki denetleyicisi çalışmıyorsa hello tarama başarısız olur. Merhaba denetleyicileri sağlıklı bir durumda olan tooverify gidin çok**donanım durumu** hello altında **Bakım** sayfası. Bileşenleri varsa, **dikkat etmeniz gereken**, başka bir işlem yapmadan önce Microsoft Support başvurun.
* Denetleyici 0 ve denetleyici 1 için sabit IP'ler yönlendirilebilir ve bunlar hello güncelleştirmeleri toohello aygıt bakım için kullanılan gibi toohello Internet bağlanabildiğinizden emin olun. Merhaba kullanabilirsiniz [Bağlantıyı Sına cmdlet](https://technet.microsoft.com/library/hh849808.aspx) tooping bilinen bir adresi outlook.com, denetleyici hello tooverify gibi hello ağ dışında Ağ dışından bağlantı toohello sahiptir.
* 80 ve 443 numaralı bağlantı noktalarını, StorSimple Cihazınızda giden iletişim için kullanılabilir olduğundan emin olun. Daha fazla bilgi için bkz: Merhaba [StorSimple cihazınız için ağ gereksinimleri](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Merhaba aygıt yazılım sürümü (Ekim 2014 güncelleştirmesi) 6.3.9600.17312 eskiyse hello veri 2 ve veri 3 bağlantı noktaları, hello güncelleştirmeden önce etkinleştirilirse, devre dışı bırakın. Başlangıç veri 2 ve veri 3 hello güncelleştirmesini yüklediğinizde etkin bağlantı noktalarını bırakarak cihaz denetleyicisi toogo kurtarma moduna neden olabilir. Lütfen hello ağ arabirimlerini devre dışı bıraktığınızda tüm ilişkili hello birimlerin çevrimdışına alınır ve hello g/ç hello güncelleştirmesi süresi boyunca hello kesilmiş olabilir unutmayın.  

## <a name="whats-new-in-hello-february-release"></a>Merhaba Şubat sürümde yenilikler
Bu güncelleştirme hello GA yayın toohello Ekim 2014 sürümünden yükseltme cihazlarda oluştu hello Fabrika sıfırlaması sorun için bir düzeltme içerir. Daha fazla bilgi için bkz: [bu sürümde giderilen sorunlar](#issues-fixed-in-the-february-release).   

Bu güncelleştirme, yeni özellikler ve işlevsellik içermiyor.  

## <a name="issues-fixed-in-hello-february-release"></a>Merhaba Şubat sürümde giderilen sorunlar
Merhaba aşağıdaki tabloda bu güncelleştirmede giderilen hello sorun açıklanmaktadır.  

| Hayır. | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Fabrika sıfırlaması |Başlangıçta hello GA (sürümünü 6.3.9600.17215) olan bir cihazda bir Fabrika sıfırlaması yüklü ancak güncelleştirilmiş toohello Ekim sürümü (sürüm 6.3.9600.17312) tooperform deneyin. başarısız Hello fabrika ayarlarına sıfırlayıp ve hello aygıt kararsız duruma gelmesine neden olur. |Evet |Hayır |

## <a name="known-issues-in-hello-february-release"></a>Merhaba Şubat sürümdeki bilinen sorunlar
Aşağıdaki tablonun hello bu sürümdeki bilinen sorunlara özetini sağlar.

| Hayır. | Özellik | Sorun | Yorumlar/geçici çözüm | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrika sıfırlaması |Bazı durumlarda, bir Fabrika sıfırlaması gerçekleştirdiğinizde hello StorSimple cihazı takılmış ve bu iletisini görüntüler: **sıfırlama toofactory devam ediyor (aşama 8)**. Merhaba cmdlet sürerken CTRL + C tuşlarına basın bu olur. |Fabrika sıfırlamasına başlatıldıktan sonra CTRL + C tuşlarına değil. Bu durumda zaten varsa, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 2 |Disk çekirdek |Hiçbir disk çekirdek kaynaklanan Hello çoğunluğu hello EBOD muhafazası bir 8600device, diskin bağlantısı kesildiyse nadir durumlarda, ardından hello depolama havuzu çevrimdışı olur. Merhaba diskleri bağlanırlar olsa bile çevrimdışı kalır. |Tooreboot hello aygıt gerekir. Merhaba sorun devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 3 |Bulut anlık görüntü hataları |Nadir durumlarda, bir bulut anlık görüntüsü hello hatasıyla başarısız olabilir **maksimum yedekleme sınırına ulaşıldı**. Merhaba 255 çevrimiçi kopyada aşarsa bu gerçekleşir aynı aygıttan, hello silindi aynı özgün birimi. | |Evet |Evet |
| 4 |Yanlış denetleyici kimliği |Bir denetleyici değiştirme gerçekleştirildiğinde, denetleyici 0 denetleyicisi 1 olarak görünebilirler. Merhaba görüntü hello eş düğümden yüklendiğinde denetleyicisi değiştirme sırasında hello denetleyici kimliği başlangıçta hello eş denetleyicinin kimliği olarak gösterebilir Nadir durumlarda, bu davranış bir sistem yeniden başlatıldıktan sonra görülebilir. |Hiçbir kullanıcı eylemi gerekli değildir. Merhaba denetleyicisi değiştirme işlemi tamamlandıktan sonra bu durum kendisini çözümleyin. |Evet |Hayır |
| 5 |Cihaz izleme grafikleri |Hello StorSimple Yöneticisi hizmeti, hello cihaz izleme grafikleri basit çalışmıyor veya NTLM kimlik doğrulaması hello proxy sunucusu yapılandırmasını hello cihaz için etkinleştirilir. |Bu kimlik doğrulama tooNONE ayarlanır, StorSimple Yöneticisi hizmetine kayıtlı hello cihaz için Hello web proxy yapılandırması değiştirin. toodo StorSimple Set-HcsWebProxy cmdlet'i için bu, çalışma hello hello Windows PowerShell. |Evet |Evet |
| 6 |Depolama hesapları |Merhaba depolama hizmeti toodelete hello depolama hesabı kullanarak desteklenmeyen bir senaryodur. Bu kullanıcı verileri alınamıyor tooa durum götürür. | |Evet |Evet |
| 7 |Cihaz yük devretme |Aynı kaynak aygıt toodifferent hedef cihazlar desteklenmiyor hello birim kapsayıcıdan birden çok yük.    Yük devretme tek ölü aygıt toomultiple aygıtlardan veri sahipliği kaybetmek hello birim kapsayıcıları ilk aygıt üzerinden başarısız hello üzerinde hale getirir. Bu tür bir yük devretme sonrasında, bu birim kapsayıcıları görünür veya hello Klasik Azure portalında görüntülediğinizde farklı şekilde davranır. | |Evet |Hayır |
| 8 |Yükleme |SharePoint yükleme için StorSimple bağdaştırıcısı sırasında tooprovide cihaz IP hello yükleme toofinish sırada başarıyla gerekir. | |Evet |Hayır |
| 9 |Web proxy |Web proxy yapılandırması varsa hello olarak HTTPS protokolü, belirtilen sonra aygıtı hizmeti iletişimi etkilenecek ve hello aygıt çevrimdışı. Destek paketleri aygıtınızda önemli miktarda kaynak tüketen hello işlemde de oluşturulur. |Belirtilen protokol hello gibi Hello web proxy URL'Sİ'ın HTTP olduğundan emin olun. Hakkında daha fazla bilgi çok[cihazınız için web Proxy'yi Yapılandır](storsimple-configure-web-proxy.md). |Evet |Hayır |
| 10 |Web proxy |Yapılandırma ve web proxy bir kayıtlı cihazda etkinleştirirseniz, Cihazınızda toorestart hello etkin denetleyicisine ihtiyacınız vardır. | |Evet |Hayır |
| 11 |Yüksek bulut gecikme süresi ve yüksek g/ç iş yükü |StorSimple Cihazınızı çok yüksek bulut gecikme (saniye sırasını) ve yüksek g/ç iş yükü bileşimini karşılaştığında, düzeyi düşürülmüş bir duruma hello aygıt birimleri gidin ve hello g/ç "cihaz hazır değil" hatası ile başarısız. |Toomanually yeniden başlatma hello cihaz denetleyicilerinin gerekir veya bir aygıt yük devretme toorecover bu durumdan gerçekleştirin. |Evet |Hayır |

## <a name="physical-device-updates-in-hello-february-release"></a>Merhaba Şubat sürümdeki fiziksel aygıt güncelleştirmeleri
Bu güncelleştirme düzeltmeleri hello Fabrika hello GA yayın toohello Ekim 2014 sürümünden yükseltme cihazlarda oluştu sorunu sıfırlayın. Tüm diğer güncelleştirmeleri toohello StorSimple cihazı içermiyor.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Seri Bağlı SCSI (SAS) denetleyicisi ve bellenim güncelleştirmeleri hello Şubat sürümde
Bu sürüm, herhangi bir güncelleştirme toohello seri bağlı SCSI (SAS) denetleyicisi veya hello bellenim içermiyor. Merhaba sürücü güncelleştirmesi hello Ekim 2014 sürümünden oluştu.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Sanal cihaz güncelleştirmeleri hello Şubat sürümde
Bu sürüm hello sanal cihaz için herhangi bir güncelleştirme içermiyor. Bu güncelleştirmeyi uyguladıktan sanal cihazı hello yazılımı sürümü değişmez.

