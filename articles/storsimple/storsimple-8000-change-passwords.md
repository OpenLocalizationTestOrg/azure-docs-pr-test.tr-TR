---
title: "aaaChange StorSimple parolalarınızı | Microsoft Docs"
description: "Nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti toochange StorSimple Snapshot Manager ve cihaz Yöneticisi parolalarınızı açıklar."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>StorSimple parolalarınızı Hello StorSimple cihaz Yöneticisi hizmeti toochange kullanın

## <a name="overview"></a>Genel Bakış
Azure portal hello **aygıt ayarları** seçeneği StorSimple cihaz Yöneticisi hizmeti tarafından yönetilen bir StorSimple cihazda yapılandırabilirsiniz tüm hello aygıt parametrelerini içerir. Bu öğretici hello nasıl kullanabileceğinizi açıklar **güvenlik** altında seçeneği **aygıt ayarları** toochange aygıt yöneticinize veya StorSimple Snapshot Manager parolası.

## <a name="change-hello-device-administrator-password"></a>Değişiklik hello cihaz Yöneticisi parolası
Windows PowerShell arabirimi tooaccess hello StorSimple cihazı kullanmak için gerekli tooenter bir cihaz Yöneticisi parolası olur. Bir hizmetle Hello ilk StorSimple cihaz kaydedildiğinde hello varsayılan bu arabirimin paroladır *Parola1*. Verilerinizin Hello güvenlik için bu parolayı gerekli toochange olan hello kayıt işleminin hello sonuna. Bu parolayı değiştirmeden hello kayıt işleminden çıkmak olamaz. Daha fazla bilgi için bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Merhaba Windows PowerShell arabirimi üzerinden kayıt sırasında ilk ayarlandı hello parola hello Azure portal daha sonra değiştirilebilir. Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello gerçekleştirin.

#### <a name="toochange-hello-device-administrator-password"></a>toochange hello cihaz Yöneticisi parolası
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**.

2. Merhaba Tablo listesi aygıtları gelen, seçin ve hello cihaz parolasını tıklatın toochange düşündüğünüz.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Merhaba, **ayarları** dikey penceresinde çok Git**Aygıt Ayarları > Güvenlik**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **parola** toochange hello cihaz Yöneticisi parolası.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. Merhaba, **parola** dikey penceresinde 8 too15 karakterler içeren bir yönetici parolasını belirtin. Merhaba parola 3 veya daha çok büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi olmalıdır.

6. Merhaba parolayı onaylayın.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Tıklatın **kaydetmek** tıklatıp onaylamanız istendiğinde, **Evet**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

Merhaba cihaz Yöneticisi parolası şimdi güncelleştirilmesi gerekir. Bu değiştirilmiş parola tooaccess hello Windows PowerShell arabirimi kullanabilirsiniz.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Merhaba StorSimple Snapshot Manager parolasını ayarlayın
StorSimple Snapshot Manager yazılımı Windows ana bilgisayarınıza bulunur ve StorSimple Cihazınızı hello form yerel ve bulut anlık görüntüleri toomanage yedeklerini yöneticilerinin sağlar.

StorSimple anlık görüntü Yöneticisi'nde bir aygıt yapılandırma sırasında sizden istenir tooprovide hello aygıt IP adresi ve parola tooauthenticate depolama cihazı.

Ayarlayabilir veya hello parola için StorSimple Snapshot Manager hello Azure portal değiştirin. Aşağıdaki adımları tooset hello gerçekleştirmek veya hello StorSimple Snapshot Manager parolasını değiştirin.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>tooset hello StorSimple Snapshot Manager parolası
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**.

2. Merhaba Tablo listesi aygıtları gelen, seçin ve hello aygıtı tıklatın StorSimple Snapshot Manager parolasını tooset düşündüğünüz veya değiştirin.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Merhaba, **ayarları** dikey penceresinde çok Git**Aygıt Ayarları > Güvenlik**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **parola** tooset ya da değişiklik hello StorSimple Snapshot Manager parolası.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. Merhaba, **parola** dikey penceresinde, 14 veya 15 karakter olan bir parola girin. 3 veya daha çok büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi hello parola içerdiğinden emin olun.

6. Merhaba parolayı onaylayın.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Tıklatın **kaydetmek** tıklatıp onaylamanız istendiğinde, **Evet**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

Merhaba StorSimple Snapshot Manager parolası şimdi güncelleştirilmesi gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-8000-security.md).
* Daha fazla bilgi edinmek [cihaz yapılandırmanızı değiştirme](storsimple-8000-modify-device-config.md).
* Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).

