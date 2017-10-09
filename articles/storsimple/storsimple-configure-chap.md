---
title: "StorSimple 8000 serisi cihaz için CHAP aaaConfigure | Microsoft Docs"
description: "Nasıl tooconfigure hello karşılıklı kimlik doğrulama protokolü (CHAP) StorSimple cihazında açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>StorSimple cihazınız için CHAP yapılandırma
Bu öğretici nasıl tooconfigure StorSimple cihazınız için CHAP açıklanmaktadır. Bu makalede ayrıntılı hello yordam StorSimple 1200 aygıtların yanı sıra tooStorSimple 8000 serisi geçerlidir.

CHAP karşılıklı kimlik doğrulama protokolü için anlamına gelir. Itanium tabanlı sistemler için sunucuları toovalidate hello kimliği uzak istemci tarafından kullanılan bir kimlik doğrulama düzeni değil. Merhaba doğrulama bir paylaşılan parola veya gizli temel alır. CHAP tek yönlü olabilir (tek yönlü) veya karşılıklı (çift yönlü). Merhaba hedef Başlatıcı doğruladığında tek yönlü CHAP türüdür. Karşılıklı veya ters CHAP hello diğer yandan hello hedef hello Başlatıcı kimlik doğrulaması ve hello Başlatıcı hello hedef kimlik doğrulaması yapmak gerektirir. Başlatıcı kimlik doğrulaması olmadan hedef kimlik doğrulaması uygulanabilir. Ancak, yalnızca başlatıcı kimlik doğrulaması aynı zamanda uygulanırsa, hedef kimlik doğrulama uygulanabilir. 

En iyi uygulama, CHAP tooenhance iSCSI güvenlik kullanmanızı öneririz.

> [!NOTE]
> IPSec StorSimple cihazlarda şu anda desteklenmiyor aklınızda bulundurun.
> 
> 

Merhaba StorSimple cihazı Hello CHAP ayarları yolları aşağıdaki hello yapılandırılabilir:

* Tek yönlü veya tek yönlü kimlik doğrulaması
* Çift yönlü veya karşılıklı veya ters kimlik doğrulaması

Her durumda, hello portal hello cihaz ve hello sunucu iSCSI Initiator yazılımı için yapılandırılmış toobe gerekir. Merhaba bu yapılandırma için ayrıntılı adımlar öğreticiyi izleyerek hello açıklanmıştır.

## <a name="unidirectional-or-one-way-authentication"></a>Tek yönlü veya tek yönlü kimlik doğrulaması
Tek yönlü kimlik doğrulamada hello hedef hello Başlatıcı kimliğini doğrular. Bu kimlik doğrulama hello StorSimple cihaz ve hello iSCSI Initiator yazılımı hello konaktaki hello CHAP Başlatıcı ayarları yapılandırmanız gerekir. StorSimple cihazınız için ayrıntılı yordamlar hello ve Windows ana bilgisayar sonraki açıklanmıştır.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure cihazınız için tek yönlü kimlik doğrulama
1. Merhaba hello üzerinde Klasik Azure portalı içinde **aygıtları** hello sayfasında, **yapılandırma** sekmesi.
   
    ![CHAP Başlatıcı](./media/storsimple-configure-chap/IC740943.png)
2. Aşağı kaydırın, bu sayfada ve hello **CHAP Başlatıcı** bölümü:
   
   1. CHAP başlatıcı için bir kullanıcı adı sağlayın.
   2. CHAP başlatıcı için bir parola sağlayın.
      
    > [!IMPORTANT]
    > Merhaba CHAP kullanıcı adı 233'den az karakter içermelidir. Merhaba CHAP parolası 12 ile 16 arasında karakter olması gerekir. Uzun bir kullanıcı adı ve parola kimlik doğrulama hatası hello Windows ana bilgisayarda sonuçlanır.
   
   3. Merhaba parolayı onaylayın.
3. **Kaydet** düğmesine tıklayın. Bir onay iletisi görüntülenir. Tıklatın **Tamam** toosave hello değişiklikleri.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>tooconfigure tek yönlü kimlik doğrulama hello Windows ana bilgisayar sunucusu
1. Merhaba Windows ana bilgisayar sunucusunda hello iSCSI başlatıcısı başlatın.
2. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello aşağıdaki adımları gerçekleştirin:
   
   1. Merhaba tıklatın **bulma** sekmesi.
      
       ![iSCSI başlatıcısı özellikleri](./media/storsimple-configure-chap/IC740944.png)
   2. Tıklatın **Portal Bul**.
3. Merhaba, **Hedef Portal Bul** iletişim kutusunda:
   
   1. Cihazınızı Hello IP adresini belirtin.
   2. Tıklatın **Gelişmiş**.
      
       ![Hedef portalı Bul](./media/storsimple-configure-chap/IC740945.png)
4. Merhaba, **Gelişmiş ayarları** iletişim kutusunda:
   
   1. Select hello **CHAP'yi etkinleştir oturum** onay kutusu.
   2. Merhaba, **adı** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello kullanıcı adı.
   3. Merhaba, **hedef gizli** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello parola.
   4. **Tamam** düğmesine tıklayın.
      
       ![Gelişmiş ayarlar genel](./media/storsimple-configure-chap/IC740946.png)
5. Merhaba üzerinde **hedefleri** hello sekmesinde **iSCSI başlatıcısı özellikleri** penceresinde hello Aygıt durumu olarak görünmelidir **bağlı**. Bir StorSimple 1200 cihaz kullanıyorsanız, ardından her birim bir iSCSI hedefi olarak aşağıda gösterildiği gibi bağlanır. Bu nedenle, 3-4 arası adımlar, her birim için yinelenen toobe gerekir.
   
    ![Ayrı hedefleri olarak takılı birimleri](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Merhaba iSCSI adını değiştirirseniz, hello yeni ad yeni iSCSI oturumları için kullanılır. Yeni ayarları oturumunuzu kapattığınızda kadar oturumlar var ve oturum açma için tekrar kullanılmaz.
   > 
   > 

Merhaba Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için çok Git[ek hususlar](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Çift yönlü veya karşılıklı kimlik doğrulaması
Çift yönlü kimlik doğrulama, hello hedef hello Başlatıcı kimliğini doğrular ve hello hedef hello Başlatıcı kimliğini doğrular. Bu, hello kullanıcı tooconfigure hello CHAP Başlatıcı ayarları gibi hello hello cihaz ve iSCSI Initiator yazılımı hello konaktaki CHAP ayarları ters gerektirir. Merhaba aşağıdaki yordamlar hello adımları tooconfigure karşılıklı kimlik doğrulaması hello cihazda ve hello Windows ana bilgisayarda açıklar.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure cihazınız karşılıklı kimlik doğrulaması için
1. Merhaba hello üzerinde Klasik Azure portalı içinde **aygıtları** hello sayfasında, **yapılandırma** sekmesi.
   
    ![CHAP hedefi](./media/storsimple-configure-chap/IC740948.png)
2. Aşağı kaydırın, bu sayfada ve hello **CHAP hedefi** bölümü:
   
   1. Sağlayan bir **ters CHAP kullanıcı adı** cihazınız için.
   2. Tedarik bir **ters CHAP parolası** cihazınız için.
   3. Merhaba parolayı onaylayın.
3. Merhaba, **CHAP Başlatıcı** bölümü:
   
   1. Sağlayan bir **kullanıcı adı** cihazınız için.
   2. Sağlayan bir **parola** cihazınız için.
   3. Merhaba parolayı onaylayın.
4. **Kaydet** düğmesine tıklayın. Bir onay iletisi görüntülenir. Tıklatın **Tamam** toosave hello değişiklikleri.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>Merhaba Windows tooconfigure çift yönlü kimlik doğrulamasını ana bilgisayar sunucusu
1. Merhaba Windows ana bilgisayar sunucusunda hello iSCSI başlatıcısı başlatın.
2. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello tıklatın **yapılandırma** sekmesi.
3. Tıklatın **CHAP**.
4. Merhaba, **iSCSI Başlatıcı Karşılıklı CHAP parolası** iletişim kutusunda:
   
   1. Türü hello **ters CHAP parolası** hello Klasik Azure portalı yapılandırılmış.
   2. **Tamam** düğmesine tıklayın.
      
       ![iSCSI Başlatıcı Karşılıklı CHAP parolası](./media/storsimple-configure-chap/IC740949.png)
5. Merhaba tıklatın **hedefleri** sekmesi.
6. Merhaba tıklatın **Bağlan** düğmesi. 
7. Merhaba, **tooTarget bağlanmak** iletişim kutusu, tıklatın **Gelişmiş**.
8. Merhaba, **Gelişmiş Özellikler** iletişim kutusunda:
   
   1. Select hello **CHAP'yi etkinleştir oturum** onay kutusu.
   2. Merhaba, **adı** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello kullanıcı adı.
   3. Merhaba, **hedef gizli** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello parola.
   4. Select hello **gerçekleştirme karşılıklı kimlik doğrulaması** onay kutusu.
      
       ![Gelişmiş ayarlar karşılıklı kimlik doğrulaması](./media/storsimple-configure-chap/IC740950.png)
   5. Tıklatın **Tamam** toocomplete hello CHAP yapılandırma

Merhaba Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için çok Git[ek hususlar](#additional-considerations).

## <a name="additional-considerations"></a>Diğer konular
Merhaba **Hızlı Bağlan** özelliği etkinleştirilmiş CHAP sahip bağlantıları desteklemiyor. CHAP etkin olduğunda, hello kullandığınızdan emin olun **Bağlan** hello üzerinde kullanılabilir düğmesi **hedefleri** sekmesini tooconnect tooa hedef.

![Tootarget Bağlan](./media/storsimple-configure-chap/IC740947.png)

Merhaba, **tooTarget bağlanmak** sunulan, select hello iletişim kutusuna **bu sık kullanılan hedefler bağlantı toohello listesine eklemek** onay kutusu. Bu, her zaman hello bilgisayarı yeniden başlatır, girişiminde toorestore hello bağlantı toohello iSCSI sık kullanılan hedefler yapılmasını sağlar.

## <a name="errors-during-configuration"></a>Yapılandırma sırasında hatalar
CHAP yapılandırması doğru değil sonra büyük olasılıkla toosee olduğunuz bir **kimlik doğrulama hatası** hata iletisi.

## <a name="verification-of-chap-configuration"></a>Doğrulama CHAP yapılandırma
CHAP hello aşağıdaki adımları tamamlayarak kullanılmakta olduğunu doğrulayabilirsiniz.

#### <a name="tooverify-your-chap-configuration"></a>tooverify CHAP yapılandırma
1. Tıklatın **sık kullanılan hedefler**.
2. Kimlik doğrulamasının etkin hello hedef seçin.
3. Tıklatın **ayrıntıları**.
   
    ![iSCSI Başlatıcı özellikleri sık kullanılan hedefler](./media/storsimple-configure-chap/IC740951.png)
4. Merhaba, **sık kullanılan hedef ayrıntıları** iletişim kutusu, Not hello hello girişi **kimlik doğrulaması** alan. Merhaba yapılandırma başarılı olup olmadığını, yazması gerekir **CHAP**.
   
    ![Sık kullanılan hedef ayrıntıları](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-security.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

