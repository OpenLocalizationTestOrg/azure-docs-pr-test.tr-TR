---
title: "aaaStorSimple 8000 yayın sürümü sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikleri, açık sorunlar ve hello için kullanılabilir geçici çözümler Temmuz 2014 açıklamaktadır Microsoft Azure StorSimple sürüm."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>StorSimple 8000 serisi yayımlanan sürümü sürüm notları - Temmuz 2014
## <a name="overview"></a>Genel Bakış
Merhaba izleyin sürüm notları tanımlamak hello kritik açık sorunlar hello StorSimple 8000 serisi için Microsoft Azure StorSimple Temmuz 2014 genel kullanılabilirlik (GA) sürümü. Bu sürüm toosoftware sürüm 6.3.9600.17215 karşılık gelir.  

Aksi belirtilmediği sürece, bu sürüm notları hello StorSimple cihazı tooall modellerinin uygulayın. Merhaba sürüm notları sürekli olarak güncelleştirilir; Bunlar, çözüm gerektiren kritik sorunlar bulundukça olarak eklenir. Microsoft Azure StorSimple çözümünüzün dağıtmadan önce aşağıdaki bilgilerle hello göz önünde bulundurun.  

## <a name="known-issues-in-this-release"></a>Bu sürümdeki bilinen sorunlar
Aşağıdaki tablonun hello bu sürümdeki bilinen sorunlara özetini sağlar.  

| Hayır. | Özellik | Sorun | Yorumlar/geçici çözüm | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrika sıfırlaması |Bazı durumlarda, bir Fabrika sıfırlaması gerçekleştirdiğinizde hello StorSimple cihazı takılmış ve bu iletisini görüntüler: **sıfırlama toofactory devam ediyor (aşama 8)**. Merhaba cmdlet sürerken CTRL + C tuşlarına basın bu olur. |Fabrika sıfırlamasına başlatıldıktan sonra CTRL + C tuşlarına değil. Bu durumda zaten varsa, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 2 |Disk çekirdek |Hiçbir disk çekirdek kaynaklanan hello EBOD muhafazası 8600 aygıtının diskleri Hello çoğunluğu bağlantısı kesildiyse nadir durumlarda, ardından hello depolama havuzu çevrimdışı olur. Merhaba diskleri bağlanırlar olsa bile çevrimdışı kalır. |Tooreboot hello aygıt gerekir. Merhaba sorun devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |Evet |Hayır |
| 3 |Bulut anlık görüntü hataları |Nadir durumlarda, bir bulut anlık görüntüsü hello hatasıyla başarısız olabilir **maksimum yedekleme sınırına ulaşıldı**. Merhaba 255 çevrimiçi kopyada aşarsa bu gerçekleşir aynı aygıttan, hello silindi aynı özgün birimi. | |Evet |Evet |
| 4 |Yanlış denetleyici kimliği |Bir denetleyici değiştirme gerçekleştirildiğinde, denetleyici 0 denetleyicisi 1 olarak görünebilirler. Merhaba görüntü hello eş düğümden yüklendiğinde denetleyicisi değiştirme sırasında hello denetleyici kimliği başlangıçta hello eş denetleyicinin kimliği olarak gösterebilir Nadir durumlarda, bu davranış bir sistem yeniden başlatıldıktan sonra görülebilir. |Hiçbir kullanıcı eylemi gerekli değildir. Merhaba denetleyicisi değiştirme işlemi tamamlandıktan sonra bu durum kendisini çözümleyin. |Evet |Hayır |
| 5 |Cihaz izleme grafikleri |Hello StorSimple Yöneticisi hizmeti, hello cihaz izleme grafikleri basit çalışmıyor veya NTLM kimlik doğrulaması hello proxy sunucusu yapılandırmasını hello cihaz için etkinleştirilir. |Bu kimlik doğrulama tooNONE ayarlanır, StorSimple Yöneticisi hizmetine kayıtlı hello cihaz için Hello web proxy yapılandırması değiştirin. toodo StorSimple Set-HcsWebProxy cmdlet'i için bu, çalışma hello hello Windows PowerShell. |Evet |Evet |
| 6 |Depolama hesapları |Merhaba depolama hizmeti toodelete hello depolama hesabı kullanarak desteklenmeyen bir senaryodur. Bu kullanıcı verileri alınamıyor tooa durum götürür. | |Evet |Evet |
| 7 |Yeniden çalışma |Olağanüstü Durum Kurtarma (DR) 24 saat içinde yeniden çalışma desteklenmez. | |Evet |Hayır |
| 8 |Cihaz yük devretme |Aynı kaynak aygıt toodifferent hedef cihazlar desteklenmiyor hello birim kapsayıcıdan birden çok yük. Yük devretme tek ölü aygıt toomultiple aygıtlardan veri sahipliği kaybetmek hello birim kapsayıcıları ilk aygıt üzerinden başarısız hello üzerinde hale getirir. Bu tür bir yük devretme sonrasında, bu birim kapsayıcıları görünür veya hello Klasik Azure portalında görüntülediğinizde farklı şekilde davranır. | |Evet |Hayır |
| 9 |Yükleme |SharePoint yükleme için StorSimple bağdaştırıcısı sırasında tooprovide cihaz IP hello yükleme toofinish için başarıyla gerekir. | |Evet |Hayır |
| 10 |Ağ arabirimleri |Veri 2 ve veri 3 ağ arabirimleri hello yazılımda değiştirildi. |Bu arabirimleri tooconfigure gereksiniminiz varsa lütfen Microsoft Support başvurun. |Evet |Hayır |

