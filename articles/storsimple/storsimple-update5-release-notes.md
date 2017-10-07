---
title: "aaaStorSimple 8000 serisi güncelleştirme 5 sürüm notları | Microsoft Docs"
description: "Merhaba yeni özellikler, sorunlar ve geçici çözümler için StorSimple 8000 serisi güncelleştirme 5 açıklar."
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>StorSimple 8000 serisi güncelleştirme 5 sürüm notları

## <a name="overview"></a>Genel Bakış

Merhaba aşağıdaki sürüm notları hello yeni özellikleri açıklar ve hello kritik açık sorunlar için StorSimple 8000 serisi güncelleştirme 5 tanımlayın. Ayrıca bu sürümde dahil hello StorSimple yazılım güncelleştirmelerinin bir listesini içerir.

Güncelleştirme 5 güncelleştirme 4 ile güncelleştirme 0.1 çalıştıran uygulanan tooany StorSimple cihazı olabilir. Güncelleştirme 5 ile ilişkili hello aygıt 6.3.9600.17845 sürümüdür.

StorSimple çözümünüzde hello dağıtmadan önce notları güncelleştirme hello yayın içinde yer alan hello bilgileri gözden geçirin.

> [!IMPORTANT]
> * Güncelleştirme 5 aygıt yazılımı, disk bellenim, işletim sistemi güvenlik ve diğer işletim sistemi güncelleştirmelerini sahiptir. Bu güncelleştirme yaklaşık 4 saat tooinstall sürer. Disk bellenim güncelleştirme kesintiye uğratan güncelleştirme ve cihazınız için bir kapalı kalma süresi ile sonuçlanır. Cihazınız güncel güncelleştirme 5 tookeep uygulamanızı öneririz.
> * Yeni sürümler için güncelleştirmelerinin göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Birkaç gün bekleyin ve ardından güncelleştirmeleri taramak üzere bu güncelleştirmeleri yeniden olarak yakında kullanılabilir hale gelecektir.

## <a name="whats-new-in-update-5"></a>Güncelleştirme 5'teki yenilikler

Merhaba aşağıdaki anahtar geliştirmeler ve hata düzeltmeleri güncelleştirme 5'te yapıldı.

* **StorSimple cihaz Yöneticisi hizmeti ile Azure Active Directory (AAD) tooauthenticate kullanımını** – gelen güncelleştirme 5'ten başlayarak, Azure Active Directory olduğu hello StorSimple cihaz Yöneticisi hizmeti ile kullanılan tooauthenticate. Merhaba eski kimlik doğrulama mekanizması aralık 2017 kullanım dışı kalacaktır. Tüm hello kullanıcılar hello yeni kimlik doğrulaması URL'lerini kendi güvenlik duvarı kuralları eklemeniz gerekir. Daha fazla bilgi için çok Git[hello ağ gereksinimleri, StorSimple cihazınız için listelenen kimlik doğrulaması URL'lerini](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Merhaba kimlik doğrulaması URL'sini hello güvenlik duvarı kurallarında bulunmuyorsa hello kullanıcılar StorSimple cihazını hello hizmetiyle kimlik doğrulaması yapamıyor kritik bir uyarı görürsünüz. Merhaba kullanıcılar bu uyarıyı görürseniz, tooinclude hello yeni kimlik doğrulaması URL'sini ihtiyaç duyar. Daha fazla bilgi için çok Git[uyarıları ağ StorSimple](storsimple-8000-manage-alerts.md#networking-alerts).

* **StorSimple anlık görüntü Yöneticisi'nin yeni sürümü** -StorSimple anlık görüntü Yöneticisi'nin yeni bir sürüme güncelleştirme 5 ile serbest bırakılır. Toothis sürüm güncelleştirmenizi öneririz. Bu sürümü veya sonraki sürümü, güncelleştirme 3'ü çalıştıran tüm hello StorSimple cihazlar ile uyumlu değildir. Daha fazla bilgi için çok Git[StorSimple Snapshot Manager dağıtmak](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Güncelleştirme 5'te giderilen sorunlar

Merhaba aşağıdaki tabloda güncelleştirme 5'te düzeltilen sorunlardan özetini sağlar.

| Hayır | Özellik | Sorun | Toophysical aygıt uygular | Toovirtual aygıt uygular |
| --- | --- | --- | --- | --- |
| 1 |Windows PowerShell uzaktan iletişim |Merhaba önceki sürümde, kullanıcı uzak bağlantı toohello StorSimple bulut uygulaması Windows PowerShell aracılığıyla tooestablish çalışırken bir hata alırsınız. Bu sorun kök neden oldu ve bu sürümde sabit. |Hayır |Evet |
| 2 |Bant genişliği şablonları |Önceki sürümde, hangi hello aygıtı için yapılandırılan daha düşük bant genişliği ile sonuçlandı bant genişliği şablonları ile ilgili bir sorun oluştu. Bu sorun, bu sürümde çözümlenir. |Evet |Evet |
| 3 |Yük devretme |Çok sayıda birimleri aygıtla güncelleştirme 4 ile birlikte çalışan tooanother aygıt üzerinden başarısız olduğunda önceki sürümde tooapply hello erişim denetimi kayıtları çalışırken hello işlemi başarısız olur. Bu sürümde bu sorun düzeltilmiştir. |Evet |Evet |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Önceki sürümlerden güncelleştirme 5'te bilinen sorunlar

Güncelleştirme 5'te yeni bilinen bir sorun vardır. Önceki sürümlerden tooUpdate 5 üzerinden taşınan sorunların listesi için çok Git[güncelleştirme 3 Sürüm Notları](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Seri Bağlı SCSI (SAS) denetleyicisi ve bellenim güncelleştirmeleri güncelleştirme 5

Bu sürüm, SAS denetleyicisi ve LSI sürücü ve bellenim güncelleştirmeleri vardır. Tooinstall bu güncelleştirmeleri nasıl görürüm hakkında daha fazla bilgi için [güncelleştirme 5 yükleme](storsimple-8000-install-update-5.md) , StorSimple Cihazınızda.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Güncelleştirme 5 StorSimple bulut uygulaması güncelleştirmeleri

Bu güncelleştirme uygulanan toohello StorSimple bulut uygulaması (olarak da bilinen hello sanal cihaz) olamaz. Yeni bulut cihazları hello güncelleştirme 5 görüntü kullanılarak oluşturulan toobe gerekir. Hakkında bilgi için toocreate StorSimple bulut uygulaması Git çok[dağıtma ve StorSimple bulut uygulaması yönetmek](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Sonraki adım

Nasıl çok öğrenin[güncelleştirme 5 yükleme](storsimple-8000-install-update-5.md) , StorSimple Cihazınızda.

