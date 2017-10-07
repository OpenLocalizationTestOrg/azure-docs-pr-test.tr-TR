---
title: "aaaStorSimple 8000 güncelleştirme 0.2 sürüm notları | Microsoft Docs"
description: "Ocak 2015 Hello yeni özellikler ve düzeltmeler, açık sorunlar ve hello için kullanılabilir geçici çözümler açıklanmaktadır Microsoft Azure StorSimple sürüm (güncelleştirme 0.2)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>StorSimple 8000 serisi güncelleştirme 0.2 sürüm notları - Ocak 2015
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello kritik açık sorunlar hello Ocak 2015 sürümü, Microsoft Azure StorSimple için belirleyin. Bunlar ayrıca hello StorSimple yazılım listesi ve bu sürümde dahil Bellenim güncelleştirmeleri içerir. Merhaba StorSimple 8000 serisi yayın sürümü Temmuz 2014'te genel olarak kullanılabilir yaptıktan sonra bu hello ikinci sürümüdür.

Bu güncelleştirme hello fiziksel aygıt yazılım sürümü hello Ekim Update'ten değiştirmez. Toobe sürüm 6.3.9600.17312 devam eder. Merhaba sanal cihaz görüntüsü tarafından kullanılan hello görüntüsü bu sürümde değiştirildi. Bu nedenle, 20/1/2015 tarihinden sonra oluşturulan tüm hello yeni sanal cihazların Merhaba sürüm 6.3.9600.17361 gösterilir.  

Lütfen aşağıdaki hello sürüm notları hello Ocak 2015 güncelleştirmesi içinde yer alan bilgilerle hello gözden geçirin.

> [!IMPORTANT]
> * Bu güncelleştirme Windows Update'te kullanılabilir değil ve diğer güncelleştirmeleri gibi yüklenemez. Merhaba güncelleştirmeleri hello Klasik Azure portalı kullanarak uyguladıysanız bile Cihazınızı Bu güncelleştirme almazsınız. Bu güncelleştirme, yalnızca 20 Ocak 2015 tarihinden sonra oluşturulan toovirtual aygıtları uygulanır. 
> * Merhaba StorSimple Ocak sürümünü tüm güncelleştirmeleri toohello StorSimple fiziksel cihazı içermiyor. Yine de tüm kullanılabilir Windows güncelleştirmelerini toohello sanal aygıt uygulayabilir, de dahil olmak üzere en son güvenlik düzeltmeleri, ancak sürüm hello StorSimple fiziksel cihazı için bir değişiklik görmez.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Merhaba Ocak sürümde yenilikler
Bu güncelleştirme, bir düzeltme içerir. ilgili toohello birimleri hello sanal cihazda çevrimdışı duruma geçiyor. (Bkz [bu sürümde giderilen sorunlar](#issues-fixed-in-the-january-release).)  

Merhaba güncelleştirme, yeni özellikler ve işlevsellik içermiyor.  

## <a name="issues-fixed-in-hello-january-release"></a>Merhaba Ocak sürümde giderilen sorunlar
Merhaba aşağıdaki tabloda bu güncelleştirmede giderilen hello sorun açıklanmaktadır.

| Hayır. | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Çevrimdışı duruma geçiyor birimleri |Yüksek bulut gecikmeleri kalıcı olması için birkaç dakika zaman hello StorSimple sanal cihazı birimleri hello konaklarda çevrimdışı olur. Bu düzeltmeyi hello eşiği bulut gecikmeleri, böylece hello birimleri çevrimdışı toogo konaklarda neden olacağından hello durumlarda en aza indirmek için artırır. |Hayır |Evet |

## <a name="known-issues-in-hello-january-release"></a>Merhaba Ocak sürümdeki bilinen sorunlar
Aşağıdaki tablonun hello bu sürümdeki bilinen sorunlara özetini sağlar.

| Hayır. | Özellik | Sorun | Yorumlar/geçici çözüm | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrika sıfırlaması |Bazı durumlarda, bir Fabrika sıfırlaması gerçekleştirdiğinizde hello StorSimple cihazı takılmış ve bu iletisini görüntüler: **sıfırlama toofactory devam ediyor (aşama 8).** Merhaba cmdlet sürerken CTRL + C tuşlarına basın bu olur. |Fabrika sıfırlamasına başlatıldıktan sonra CTRL + C tuşlarına değil. Bu durumda zaten varsa, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 2 |Disk çekirdek |Hiçbir disk çekirdek kaynaklanan hello EBOD muhafazası 8600 aygıtının diskleri Hello çoğunluğu bağlantısı kesildiyse nadir durumlarda, ardından hello depolama havuzu çevrimdışı olur. Merhaba diskleri bağlanırlar olsa bile çevrimdışı kalır. |Tooreboot hello aygıt gerekir. Merhaba sorun devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 3 |Bulut anlık görüntü hataları |Nadir durumlarda, bir bulut anlık görüntüsü hello hatasıyla başarısız olabilir **maksimum yedekleme sınırına ulaşıldı**. Merhaba 255 çevrimiçi kopyada aşarsa bu gerçekleşir aynı aygıttan, hello silindi aynı özgün birimi. | |Evet |Evet |
| 4 |Yanlış denetleyici kimliği |Bir denetleyici değiştirme gerçekleştirildiğinde, denetleyici 0 denetleyicisi 1 olarak görünebilirler. Merhaba görüntü hello eş düğümden yüklendiğinde denetleyicisi değiştirme sırasında hello denetleyici kimliği başlangıçta hello eş denetleyicinin kimliği olarak gösterebilir  Nadir durumlarda, bu davranış bir sistem yeniden başlatıldıktan sonra görülebilir. |Hiçbir kullanıcı eylemi gerekli değildir. Merhaba denetleyicisi değiştirme işlemi tamamlandıktan sonra bu durum kendisini çözümleyin. |Evet |Hayır |
| 5 |Cihaz izleme grafikleri |Hello StorSimple Yöneticisi hizmeti, hello cihaz izleme grafikleri basit çalışmıyor veya NTLM kimlik doğrulaması hello proxy sunucusu yapılandırmasını hello cihaz için etkinleştirilir. |Bu kimlik doğrulama tooNONE ayarlanır, StorSimple Yöneticisi hizmetine kayıtlı hello cihaz için Hello web proxy yapılandırması değiştirin. toodo StorSimple Set-HcsWebProxy cmdlet'i için bu, çalışma hello hello Windows PowerShell. |Evet |Evet |
| 6 |Depolama hesapları |Merhaba depolama hizmeti toodelete hello depolama hesabı kullanarak desteklenmeyen bir senaryodur. Bu kullanıcı verileri alınamıyor tooa durum götürür. | |Evet |Evet |
| 7 |Cihaz yük devretme |Aynı kaynak aygıt toodifferent hedef cihazlar desteklenmiyor hello birim kapsayıcıdan birden çok yük. |Yük devretme tek ölü aygıt toomultiple aygıtlardan veri sahipliği kaybetmek hello birim kapsayıcıları ilk aygıt üzerinden başarısız hello üzerinde hale getirir. Bu tür bir yük devretme sonrasında, bu birim kapsayıcıları görünür veya hello Klasik Azure portalında görüntülediğinizde farklı şekilde davranır. |Evet |Hayır |
| 8 |Yükleme |SharePoint yükleme için StorSimple bağdaştırıcısı sırasında tooprovide cihaz IP hello yükleme toofinish sırada başarıyla gerekir. | |Evet |Hayır |
| 9 |Web proxy |Web proxy yapılandırması varsa hello olarak HTTPS protokolü, belirtilen sonra aygıtı hizmeti iletişimi etkilenecek ve hello aygıt çevrimdışı. Destek paketleri aygıtınızda önemli miktarda kaynak tüketen hello işlemde de oluşturulur. |Belirtilen protokol hello gibi Hello web proxy URL'Sİ'ın HTTP olduğundan emin olun. Çok hakkında daha fazla bilgi görmek[cihazınız için web Proxy'yi Yapılandır](storsimple-configure-web-proxy.md). |Evet |Hayır |
| 10 |Web proxy |Yapılandırma ve web proxy bir kayıtlı cihazda etkinleştirirseniz, Cihazınızda toorestart hello etkin denetleyicisine ihtiyacınız vardır. | |Evet |Hayır |
| 11 |Yüksek bulut gecikme süresi ve yüksek g/ç iş yükü |StorSimple Cihazınızı çok yüksek bulut gecikme (saniye sırasını) ve yüksek g/ç iş yükü bileşimini karşılaştığında, düzeyi düşürülmüş bir duruma hello aygıt birimleri gidin ve hello g/ç "cihaz hazır değil" hatası ile başarısız. |Toomanually yeniden başlatma hello cihaz denetleyicilerinin gerekir veya bir aygıt yük devretme toorecover bu durumdan gerçekleştirin. |Evet |Hayır |

## <a name="physical-device-updates-in-hello-january-release"></a>Merhaba Ocak sürümdeki fiziksel aygıt güncelleştirmeleri
Bu güncelleştirmenin herhangi diğer değişiklikleri toohello StorSimple cihazı içermiyor.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Seri Bağlı SCSI (SAS) denetleyicisi ve bellenim güncelleştirmeleri hello Ocak sürümde
Bu sürüm, herhangi bir güncelleştirme toohello seri bağlı SCSI (SAS) denetleyicisi veya hello bellenim içermiyor. Merhaba sürücü güncelleştirmesi hello Ekim 2014 sürümünden oluştu. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Sanal cihaz güncelleştirmeleri hello Ocak sürümde
Bu sürüm hello sanal cihaz için güncelleştirilmiş bir görüntü içerir. 20 Ocak 2015 tarihinden sonra oluşturulan tüm hello sanal cihazlar hello yazılım sürümü 6.3.9600.17361 gösterilir.

