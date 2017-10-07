---
title: "aaaStorSimple 8000 serisi güncelleştirme 4 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler, sorunlar ve geçici çözümler için StorSimple 8000 serisi güncelleştirme 4 açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>StorSimple 8000 serisi güncelleştirme 4 sürüm notları

## <a name="overview"></a>Genel Bakış

Merhaba aşağıdaki sürüm notları hello yeni özellikleri açıklar ve hello kritik açık sorunlar için StorSimple 8000 serisi güncelleştirme 4 tanımlayın. Ayrıca bu sürümde dahil hello StorSimple yazılım güncelleştirmelerinin bir listesini içerir. 

Güncelleştirme 4, sürüm (GA) ya da güncelleştirme 0.1 güncelleştirme 3.1 kullanan uygulanan tooany StorSimple cihazı olabilir. Güncelleştirme 4 ile ilişkili hello aygıt 6.3.9600.17820 sürümüdür.

Lütfen StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello sürümde bulunan hello bilgileri gözden geçirin.

> [!IMPORTANT]
> * Güncelleştirme 4 aygıt yazılımı, USM üretici yazılımı, LSI sürücü ve bellenim, disk üretici yazılımı, Storport ve Spaceport, güvenlik ve diğer işletim sistemi güncelleştirmelerini sahiptir. Bu güncelleştirme yaklaşık 4 saat tooinstall sürer. Disk bellenim güncelleştirme kesintiye uğratan güncelleştirme ve cihazınız için bir kapalı kalma süresi ile sonuçlanır. Cihazınız güncel güncelleştirme 4 tookeep uygulamanızı öneririz. 
> * Yeni sürümler için güncelleştirmelerinin göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Birkaç gün bekleyin ve ardından güncelleştirmeleri taramak üzere yeniden bunlar olarak yakında kullanılabilir hale gelecektir.

## <a name="whats-new-in-update-4"></a>Güncelleştirme 4'te Yenilikler

Merhaba aşağıdaki anahtar geliştirmeler ve hata düzeltmeleri güncelleştirme 4'te yapıldı.

* **Daha Akıllı otomatik alan geri kazanma algoritmaları** – güncelleştirme 4 hello otomatik alan geri kazanma algoritmaları Gelişmiş tooadjust hello alan geri kazanma olan beklenen hello üzerinde temel döngüleri iadesi hello bulutta kullanılabilir alanı. 

* **Yerel olarak sabitlenmiş birimleri için performans geliştirmeleri** – güncelleştirme 4, yerel olarak sabitlenmiş birimlerin yüksek veri alımı (veri karşılaştırılabilir toovolume boyutu) sahip senaryolarda hello performans iyileştirilmiştir.

* **Heatmap tabanlı geri yükleme** - daha önce hello hello veri bir olağanüstü durum kurtarma (DR), aşağıdaki sürümler, yavaş bir performansıyla sonuçlanır hello erişimi desenleri dayalı hello buluttan geri yüklendi. 

    Yeni bir özellik güncelleştirme 4'te hello Aygıt kullanımı önceki tooDR olduğunda parçaları veri toocreate bir heatmap sık erişilen uygulanır (en fazla kullanılan veri öbekleri sahip yüksek ısı küçük parçalara kullanılan ancak düşük ısı vardır). DR sonra StorSimple kullandığı heatmap tooautomatically geri yükleme hello ve hello bulut hello verilerden rehydrate. 

    Tüm hello geri yüklemeler dayalı heatmap geri yüklemeler sunulmuştur. Nasıl geri yükleme ve rehydration işleri tooquery ve iptal heatmap dayalı daha fazla bilgi için çok Git[StorSimple cmdlet başvurusu için Windows PowerShell](https://technet.microsoft.com/library/dn688168.aspx).

* **StorSimple Tanılama Aracı** – güncelleştirme 4'te, bir StorSimple Tanılama Aracı yükleniyor yayımlanan kolaydır tanılamak için tooallow ve toosystem, ağ, performans ve donanım bileşen durumu ilgili sorunları giderme. Bu araç StorSimple için Windows PowerShell hello çalıştırılır. Daha fazla bilgi için çok Git[StorSimple Tanılama aracını kullanarak sorun giderme](storsimple-8000-diagnostics.md).

* **UI tabanlı StorSimple geçiş aracı** -önceki toothis sürüm, 5000-7000 Serisi veri geçişini gerekli hello kullanıcılar tooexecute hello Azure PowerShell arabirimini kullanarak hello geçiş iş akışının bir parçası. Bu sürümde, bir kolay kullanımlı UI tabanlı StorSimple aracı için destek toofacilitate sunulacağını geçiş hello aynı geçiş iş akışı. Bu aracı kurtarma demet hello birleştirilmesi için de olanak tanır. 

* **FIPS ile ilgili değişiklikleri** - bu başlayarak sürüm, FIPS varsayılan olarak etkinleştirilmiştir tüm hello StorSimple 8000 serisi cihazlar üzerinde hem de Microsoft Azure kamu ve Azure genel bulut hesapları hello için.

* **Değişiklikleri güncelleştirme** - bu sürümde, hatalar ilgili tooupdate hataları sabit.

* **Disk hataları için uyarı** -bu sürümde yaklaşan disk hatalarının hello kullanıcıyı uyarır yeni bir uyarı eklenir. Bu uyarı karşılaşırsanız, Microsoft Support tooship yedek diski başvurun. Daha fazla bilgi için çok Git[donanım uyarıları, StorSimple Cihazınızda](storsimple-manage-alerts.md#hardware-alerts).

* **Denetleyici değiştirme değişiklikleri** -hello kullanıcı tooquery hello hello denetleyicisi değiştirme işleminin durumunu izin veren bir cmdlet bu sürümde eklenir. Daha fazla bilgi için toohello Git [cmdlet tooquery denetleyicisi değiştirme durumu](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Güncelleştirme 4'te giderilen sorunlar

Merhaba aşağıdaki tabloda güncelleştirme 4'te düzeltilen sorunlardan özetini sağlar.    

| Hayır | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Yük devretme |Merhaba, hello yük devretme sonrasında var. önceki sürüm toocleanup gözlenen hello müşteri sitede bir sorunla ilgili. Bu sürümde bu sorun düzeltilmiştir. |Evet |Evet |
| 2 |Yerel olarak sabitlenmiş birimleri |Merhaba önceki sürümde, bir sorun toorelated birim oluşturma birim oluşturma hatalarına neden olan yerel olarak sabitlenmiş birimlerin vardı. Bu sorun kök neden oldu ve bu sürümde sabit. |Evet |Hayır |
| 3 |Destek Paketi |Önceki sürümde System.OutOfMemory özel durum ya da diğer hataları destek paketi oluşturma karşılanamamasına neden olan sorunları ilgili tooSupport paket vardı. Bu sürümde bu hatası düzeltilmiştir. |Evet |Evet |
| 4 |İzleme |Toomonitoring grafiklerde tüketim EB içinde nerede gösterildi yerel olarak sabitlenmiş birimleri var. ilgili bir sorun önceki sürümde. Bu hata, bu sürümde çözümlenir. |Evet |Evet |
| 5 |Geçiş |Önceki sürümde, 5000-7000 Serisi too8000 serisi cihazlar geçişini çeşitli sorunlar ilgili toohello güvenilirliğini vardı. Bu sorunları bu sürümde giderilmiştir. |Evet |Evet |
| 6 |Güncelleştirme |Önceki sürümlerde, bir güncelleştirme hatası varsa, hello denetleyicileri kurtarma moduna geçecek ve bu nedenle hello kullanıcı ile Merhaba güncelleştirme işlemine devam edilemedi toocontact Microsoft Support gerekir. <br> Bu davranış, bu sürümde değiştirildi. Hem hello denetleyicileri sonra hello kullanıcı bir güncelleştirme hatası varsa, çalışan aynı sürüm (güncelleştirme 4), denetleyicileri kurtarma moduna geçmeyecek hello hello. Merhaba kullanıcı bu hatayla karşılaşırsa için biraz bekleyin ve hello güncelleştirmeyi yeniden deneyin öneririz. Merhaba yeniden deneme başarılı. Ardından Hello yeniden deneme başarısız olursa, Microsoft Support başvurmalısınız. |Evet |Evet |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Önceki sürümlerden güncelleştirme 4'te bilinen sorunlar

Güncelleştirme 4'te yeni bilinen bir sorun vardır. Önceki sürümlerden tooUpdate 4 üzerinden taşınan sorunların listesi için çok Git[güncelleştirme 3 Sürüm Notları](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Seri Bağlı SCSI (SAS) denetleyicisi ve bellenim güncelleştirmeleri güncelleştirme 4

Bu sürüm, SAS denetleyicisi ve LSI sürücü ve bellenim güncelleştirmeleri vardır. Tooinstall bu güncelleştirmeleri nasıl görürüm hakkında daha fazla bilgi için [güncelleştirme 4'ü yükleyin](storsimple-install-update-4.md) , StorSimple Cihazınızda.

## <a name="virtual-device-updates-in-update-4"></a>Güncelleştirme 4'te sanal aygıt güncelleştirmeleri

Bu güncelleştirme uygulanan toohello StorSimple bulut uygulaması (olarak da bilinen hello sanal cihaz) olamaz. Yeni sanal cihazların oluşturulan toobe gerekir. 

## <a name="next-step"></a>Sonraki adım

Nasıl çok öğrenin[güncelleştirme 4'ü yükleyin](storsimple-install-update-4.md) , StorSimple Cihazınızda.

