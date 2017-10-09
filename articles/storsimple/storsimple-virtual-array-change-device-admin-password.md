---
title: "aaaChange StorSimple sanal dizinin cihaz Yönetici parolasının | Microsoft Docs"
description: "Nasıl toouse ya da hello Azure portal veya StorSimple sanal dizinin web kullanıcı Arabirimi toochange hello cihaz Yöneticisi parolası açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Merhaba StorSimple sanal dizinin cihaz Yöneticisi parolasını StorSimple cihaz Yöneticisi aracılığıyla değiştirme

## <a name="overview"></a>Genel Bakış

Kullandığınızda hello Windows PowerShell arabirimi tooaccess StorSimple sanal dizinin Merhaba, gerekli tooenter bir cihaz Yöneticisi parolası olur. Merhaba StorSimple cihazı ilk sağlandığında ve başlatılan hello varsayılan paroladır *Parola1*. Verilerinizin Hello güvenlik için hello oturum ilk kez ve hello varsayılan parola süre sonu bu parola gerekli toochange olur.

Merhaba aygıt, üretim ortamınızda dağıtıldıktan sonra herhangi bir zamanda ya da hello yerel web kullanıcı Arabirimi veya hello Azure portal toochange hello cihaz Yöneticisi parolası de kullanabilirsiniz. Bu makalede bu yordamların her biri açıklanmıştır.

 ![Aygıtları dikey penceresi](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Hello Azure portal toochange hello parolayı kullanın

Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello Azure portal aracılığıyla hello gerçekleştirin.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>hello Azure portal aracılığıyla toochange hello cihaz Yöneticisi parolası

1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **Yönetim** 'yi tıklatın **aygıtları**. Merhaba açılır **aygıtları** tüm StorSimple sanal dizinin aygıtlarını listeler dikey.

2. Merhaba, **aygıtları** dikey penceresinde parola değişikliği gerektirir hello aygıtı çift tıklatın.

3. Merhaba, **ayarları** , cihazınız için dikey tıklayın **güvenlik**.

4. Merhaba, **güvenlik ayarları** dikey penceresinde, aşağıdaki hello:
   
   1. Toohello aşağı **cihaz Yöneticisi parolasını** bölümü. 8 too15 karakterler içeren bir yönetici parolasını belirtin.
   2. Merhaba parolayı onaylayın.
   3. Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.

Merhaba cihaz Yöneticisi parolası şimdi güncelleştirildi. Bu değiştirilmiş parola tooaccess hello aygıt yerel olarak kullanabilirsiniz.

![Güvenlik ayarları dikey penceresi](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Merhaba yerel web kullanıcı Arabirimi toochange hello parolayı kullanın

Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello yerel web kullanıcı Arabirimi aracılığıyla hello gerçekleştirin.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>Merhaba yerel web kullanıcı Arabirimi aracılığıyla toochange hello cihaz Yöneticisi parolası

1. Merhaba yerel web kullanıcı Arabirimi, tıklatın **Bakım** > **parola değişikliği** cihazınız için.
   
    ![Parola1 değiştirme](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Merhaba girin **geçerli parola**.
3. Sağlayan bir **yeni parola**. Merhaba parola en az 8 karakter uzunluğunda olmalıdır. 3'hello aşağıdaki 4'ün içermelidir: büyük harf, küçük harfler, sayısal ve özel karakter.
   
    Parolanız olamaz Not hello son 24 parola hello aynıdır.
4. Merhaba parola tooconfirm yeniden girin.
   
    ![Parola2 değiştirme](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Merhaba sayfasının Hello altında tıklatın **Uygula**. Merhaba yeni parola şimdi uygulanır. Merhaba parola değiştirme başarısız olursa, aşağıdaki hata hello bakın:
   
    ![parola hatası](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Merhaba parola başarıyla güncelleştirildikten sonra size bildirilir. Daha sonra bu değiştirilmiş parola tooaccess hello aygıt yerel olarak kullanabilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[StorSimple sanal dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

