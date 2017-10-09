---
title: aaaChange hello StorSimple cihaz modunu | Microsoft Docs
description: "Merhaba StorSimple cihaz modlarını tanımlar ve açıklar nasıl StorSimple toochange için Windows PowerShell toouse hello aygıt modu."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>StorSimple Cihazınızda hello aygıt modu Değiştir
Bu makale, StorSimple Cihazınızı çalışabilir çeşitli modlar hello kısa bir açıklamasını sağlar. StorSimple Cihazınızı üç modda çalışabilir: normal, Bakım ve kurtarma. 

Bu makaleyi okuduktan sonra şunları öğrenmiş olacaksınız:

* Hangi hello StorSimple cihaz modlar
* Hangi modun çıkışı toofigure hello StorSimple cihazı nasıl bulunduğu
* Nasıl normal toomaintenance modundan toochange ve *tersi*

Yönetim görevleri yukarıda Hello yalnızca StorSimple cihazınızın hello Windows PowerShell arabirimi gerçekleştirilebilir.

## <a name="about-storsimple-device-modes"></a>StorSimple cihaz modları hakkında
StorSimple Cihazınızı normal, Bakım veya kurtarma modunda çalışır. Bu modların her birinde kısaca aşağıda açıklanmıştır.

### <a name="normal-mode"></a>Normal modda
Bu, hello normal çalışma modu için tam olarak yapılandırılmış bir StorSimple cihazı olarak tanımlanır. Varsayılan olarak, Cihazınızı normal modda olmalıdır.

### <a name="maintenance-mode"></a>Bakım modu
Bazen hello StorSimple cihazı bakım moduna geçirildi toobe gerekebilir. Bu mod hello cihazda tooperform bakım izin verir ve bu toodisk bellenim ilgili gibi kesintiye uğratan güncelleştirmeleri yükleyin.

StorSimple için yalnızca hello Windows PowerShell aracılığıyla bakım moduna hello sistem koyabilirsiniz. Tüm g/ç istekleri bu modda duraklatıldı. Geçici olmayan rasgele erişim belleği (NVRAM) veya hizmet kümeleme hello gibi hizmetleri de durdurulur. Girin ya da bu modundan çıkmak hem hello denetleyicileri yeniden başlatılır. Hello Bakım modu çıktığınızda, tüm hello Hizmetleri devam eder ve iyi durumda olmalıdır. Bu birkaç dakika sürebilir.

> [!NOTE]
> **Bakım modu yalnızca düzgün çalışan bir aygıtta desteklenir. İçinde bir veya iki hello denetleyicilerinin çalışmıyor bir aygıtta desteklenmiyor.**
> </br>
> 
> 

### <a name="recovery-mode"></a>Kurtarma moduna
Kurtarma moduna "Ağ desteği ile Windows güvenli modda" olarak tanımlanabilir. Kurtarma moduna hello Microsoft Support ekibi prosese ve bunları tooperform tanılama hello sistemde sağlar. Merhaba birincil kurtarma moduna tooretrieve hello sistem günlüklerini hedefidir.

Sisteminizi kurtarma moduna girer, sonraki adımlar için Microsoft Support başvurmanız gerekir. Daha fazla bilgi için çok Git[Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).

> [!NOTE]
> **Kurtarma modunda hello aygıt yerleştirilemiyor. Merhaba aygıt hatalı bir durumda, kurtarma moduna tooget hello aygıt Microsoft Support personeli inceleyebilirsiniz onu bir duruma çalışır.**
> 
> 

## <a name="determine-storsimple-device-mode"></a>StorSimple cihaz modunu belirler
#### <a name="toodetermine-hello-current-device-mode"></a>toodetermine hello geçerli aygıt modu
1. Merhaba adımları izleyerek toohello cihaz seri konsoluna oturum [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Merhaba başlık iletisi hello seri konsol menüsünde hello cihazın bakın. Bu ileti açıkça hello cihazın Bakım veya kurtarma modunda olup olmadığını belirtir. Selamlama iletisine toohello sistem modu ilgili belirli bir bilgi içermiyorsa hello aygıt normal modda çalışır.

## <a name="change-hello-storsimple-device-mode"></a>Merhaba StorSimple cihaz modunu değiştirme
Merhaba StorSimple cihazı bakım modundan (normal modda) tooperform bakım yerleştirin veya Bakım modu güncelleştirmeleri yükleyin. Aşağıdaki yordamlar tooenter veya çıkış Bakım modu hello gerçekleştirin.

> [!IMPORTANT]
> Bakım modu girmeden önce hello erişerek her iki cihaz denetleyicilerinin sağlıklı olduğunu doğrula **donanım durumu** hello üzerinde **Bakım** hello Klasik Azure portalı sayfasında. Bir veya iki hello denetleyicisi iyi durumda olmayan, Microsoft Support hello sonraki adımlar için başvurun. Daha fazla bilgi için çok Git[Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).
> 
> 

#### <a name="tooenter-maintenance-mode"></a>tooenter Bakım modu
1. Merhaba adımları izleyerek toohello cihaz seri konsoluna oturum [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde, hello sağlayın **cihaz Yöneticisi parolası**. Merhaba varsayılan parola: `Password1`.
3. Merhaba komut istemine yazın 
   
    `Enter-HcsMaintenanceMode`
4. Bu Bakım modu bildiren bir uyarı iletisi tüm g/ç istekleri kesintiye ve hello bağlantı toohello Klasik Azure portalı sever ve onaylamanız istenir görürsünüz. Tür **Y** tooenter Bakım modu.
5. Hem denetleyicileri yeniden başlatılır. Merhaba yeniden başlatma tamamlandıktan sonra hello aygıt bakım modunda olduğunu gösteren başka bir ileti görüntülenir.

#### <a name="tooexit-maintenance-mode"></a>tooexit Bakım modu
1. Toohello cihaz seri konsoluna oturum açın. Cihazınızı bakım modunda olduğundan hello başlık iletisi doğrulayın.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Exit-HcsMaintenanceMode`
3. Bir uyarı iletisi ve bir onay iletisi görüntülenir. Tür **Y** tooexit Bakım modu.
4. Hem denetleyicileri yeniden başlatılır. Merhaba yeniden başlatma tamamlandıktan sonra hello aygıtın normal modda olduğunu gösteren başka bir ileti görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[normal ve Bakım modu güncelleştirmeleri uygulamak](storsimple-update-device.md) , StorSimple Cihazınızda.

