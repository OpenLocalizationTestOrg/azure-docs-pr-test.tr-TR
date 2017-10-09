---
title: "aaaChange parolalar aracılığıyla StorSimple Aygıt Yöneticisi'ni | Microsoft Docs"
description: "Nasıl toouse hello StorSimple Yöneticisi hizmet toochange StorSimple Snapshot Manager ve cihaz Yöneticisi parolalarınızı açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>StorSimple parolalarınızı Hello StorSimple Yöneticisi hizmet toochange kullanın
## <a name="overview"></a>Genel Bakış
Klasik Azure portalı hello **yapılandırma** sayfası bir StorSimple Yöneticisi hizmeti tarafından yönetilen bir StorSimple cihazda yapılandırabilirsiniz tüm hello aygıt parametrelerini içerir. Bu öğretici hello nasıl kullanabileceğinizi açıklar **yapılandırma** toochange aygıt yöneticinize veya StorSimple Snapshot Manager parolası sayfasında.

## <a name="change-hello-device-administrator-password"></a>Değişiklik hello cihaz Yöneticisi parolası
Windows PowerShell arabirimi tooaccess hello StorSimple cihazı kullanmak için gerekli tooenter bir cihaz Yöneticisi parolası olur. Bir hizmetle Hello ilk StorSimple cihaz kaydedildiğinde hello varsayılan bu arabirimin paroladır *Parola1*. Verilerinizin Hello güvenlik için bu parolayı gerekli toochange olan hello kayıt işleminin hello sonuna. Bu parolayı değiştirmeden hello kayıt işleminden çıkmak olamaz. Daha fazla bilgi için bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Merhaba Windows PowerShell arabirimi üzerinden kayıt sırasında ilk ayarlandı hello parola hello Klasik Azure portalı daha sonra değiştirilebilir. Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello gerçekleştirin.

#### <a name="toochange-hello-device-administrator-password"></a>toochange hello cihaz Yöneticisi parolası
1. Merhaba Klasik Portalı'nda tıklatın **aygıtları** > **yapılandırma** cihazınız için.
2. Toohello aşağı **cihaz Yöneticisi parolasını** bölümü. 8 too15 karakterler içeren bir yönetici parolasını belirtin. Merhaba parola 3 veya daha çok büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi olmalıdır.
3. Merhaba parolayı onaylayın.
4. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.

Merhaba cihaz Yöneticisi parolası şimdi güncelleştirilmesi gerekir. Bu değiştirilmiş parola tooaccess hello Windows PowerShell arabirimi kullanabilirsiniz.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Merhaba StorSimple Snapshot Manager parolasını değiştirme
StorSimple Snapshot Manager yazılımı Windows ana bilgisayarınıza bulunur ve StorSimple Cihazınızı hello form yerel ve bulut anlık görüntüleri toomanage yedeklerini yöneticilerinin sağlar.

StorSimple anlık görüntü Yöneticisi'nde bir aygıt yapılandırma sırasında sizden istenir tooprovide hello aygıt IP adresi ve parola tooauthenticate depolama cihazı. Bu parolayı ilk hello Windows PowerShell arabirimi üzerinden yapılandırılır. Daha fazla bilgi için bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Merhaba Windows PowerShell arabirimi üzerinden kayıt sırasında ilk ayarlandı hello parola sonra hello Klasik portal üzerinden değiştirilebilir. Aşağıdaki adımları toochange hello StorSimple Snapshot Manager parolası hello gerçekleştirin.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>toochange hello StorSimple Snapshot Manager parolası
1. Merhaba Klasik Portalı'nda tıklatın **aygıtları** > **yapılandırma** cihazınız için.
2. Toohello aşağı **StorSimple Snapshot Manager** bölümü. 14 veya 15 karakter olan bir parola girin. 3 veya daha çok büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi hello parola içerdiğinden emin olun.
3. Merhaba parolayı onaylayın.
4. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.

Merhaba StorSimple Snapshot Manager parolası şimdi güncelleştirilmesi gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-security.md).
* Daha fazla bilgi edinmek [cihaz yapılandırmanızı değiştirme](storsimple-modify-device-config.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

