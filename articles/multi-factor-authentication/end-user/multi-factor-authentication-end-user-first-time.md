---
title: "İş veya Okul hesabım için iki aşamalı doğrulamayı yukarı aaaSet | Microsoft Docs"
description: "Şirketiniz Azure multi-Factor Authentication yapılandırdığında, iki aşamalı doğrulama kaydınızı istendiğinde toosign olacaktır. Bilgi nasıl tooset bunun. "
services: multi-factor-authentication
keywords: "nasıl toouse azure dizini, active directory hello bulutta active directory Öğreticisi"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 69b04f74f6b28d0bcd94ca649b51092d9d139581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Hesabımı iki aşamalı doğrulama için ayarlama
İki aşamalı doğrulama, diğer kişilerin toobreak için daha zor hale getirerek hesabınızın korunmasına yardımcı olan bir ek güvenlik adımdır. Bu makaleyi okuduğunuz, büyük olasılıkla bir e-posta yöneticinizden iş veya Okul çok faktörlü kimlik doğrulaması hakkında aldığınız. Veya belki de toosign çalışmış ve ek güvenlik doğrulaması yukarı tooset soran bir ileti alındı. Hello durumda **hello otomatik kayıt işlemini tamamlayıncaya kadar oturum açamazsınız**.

Bu makale, ayarladığınız yardımcı olur, **iş veya Okul hesabı**. Tooenable iki aşamalı doğrulama için kendi kişisel Microsoft hesabını istiyorsanız, bkz: [iki basamaklı doğrulama hakkında](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Hesabınızı ayarlama

BT departmanınız iki aşamalı doğrulama kullanarak toostart gerektirdiğinde bildiren bir ekran görürsünüz **yöneticiniz bu hesabı ek güvenlik doğrulaması için ayarlamanızı zorunlu kıldı**:

![Kurulum](./media/multi-factor-authentication-end-user-first-time/first.png)

başlatıldı, tooget seçin **şimdi ayarlayın.**

Oturum açtığınızda bu gibi bir ekran görmüyorsanız hello içindeki yönergeleri izleyin [iki aşamalı doğrulama için ayarlarınızı yönetme](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) doğrulama seçeneklerinizi yöneteceğiniz toofind hello Ayarları sayfası. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Oturum açma işlemleri tooverify nasıl istediğinize karar verin

Merhaba ilk soru hello kayıt işleminde olduğunu nasıl doğrulamamızı toocontact istersiniz. Merhaba tabloda hello seçenekleri göz atın ve her yöntemi için hello bağlantılar toogo toohello kurulum adımlarını kullanın.

| İletişim yöntemi | Açıklama |
| --- | --- |
| [Mobil uygulama](#use-a-mobile-app-as-the-contact-method) |- **Doğrulama için bildirim alırsınız.** Bu seçenek, akıllı telefon veya tablet bildirim toohello Doğrulayıcı uygulama iter. Merhaba bildirim görüntüleyin ve işlem meşru ise seçin **kimlik doğrulama** hello uygulama. İş veya Okul kimlik doğrulaması yapmak için önce bir PIN girmeniz gerekebilir.<br>- **Doğrulama kodunu kullanın.** Bu modda, her 30 saniyede güncelleştiren bir doğrulama kodu hello authenticator uygulaması oluşturur. Oturum açma hello arabiriminde Hello en güncel doğrulama kodunu girin.<br>Merhaba Microsoft Authenticator uygulaması için kullanılabilir [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), ve [iOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Cep telefonu araması veya SMS](#use-your-mobile-phone-as-the-contact-method) |- **Telefon araması** sağladığınız bir otomatik sesli arama toohello telefon numarasını yerleştirir. Merhaba aramayı yanıtlayın ve # hello telefon tuş tooauthenticate tuşuna basın.<br>- **SMS mesajı** bir doğrulama kodu içeren bir kısa mesaj sona erer. Merhaba metin hello isteminde, aşağıdaki toohello SMS mesajı yanıtlayın veya oturum açma hello arabirimine sağlanan hello doğrulama kodunu girin. |
| [Ofis telefonu araması](#use-your-office-phone-as-the-contact-method) |Sağladığınız bir otomatik sesli arama toohello telefon numarasını yerleştirir. Yanıt hello çağırın ve # tuşuna bastığında hello telefon tuş tooauthenticate. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Bir mobil uygulama hello iletişim yönteminiz olarak kullanma
Bu yöntemi kullanarak, telefon veya Tabletinizi Doğrulayıcı uygulama yüklemenizi gerektirir. Merhaba bu makaledeki adımları için kullanılabilir hello Microsoft Authenticator uygulaması dayalı [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), ve [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Seçin **mobil uygulama** hello aşağı açılan listeden.
2. Şunlardan birini seçin **doğrulama için bildirimlerin** veya **doğrulama kodunu kullan**seçeneğini belirleyip **ayarlanan**.

   ![Ek güvenlik doğrulama ekranı](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. Telefon veya tablet, hello uygulamasını açın ve seçin  **+**  tooadd bir hesap. (Üç nokta seçin Android cihazlarda, ardından hello **hesabı eklemek**.)
4. Bir iş veya Okul hesabı tooadd istediğinizi belirtin. telefonunuzda Hello QR kodu tarayıcı açar. Kameranızı düzgün çalışmıyorsa, tooenter şirketinizin bilgilerini el ile seçebilirsiniz. Daha fazla bilgi için bkz: [hesap el ile eklemek](#add-an-account-manually).  
5. Merhaba mobil uygulama yapılandırma hello ekranlı görünen hello QR kodu resmini tarayın.  Seçin **Bitti** tooclose hello QR kodu ekran.  

   ![QR kodu ekranı](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Merhaba telefonda etkinleştirme sona erdiğinde, seçin **kişi benim**.  Bu adım, bir bildirim veya bir doğrulama kodu tooyour telefon gönderir. Seçin **doğrulayın**.  
7. Şirketiniz, oturum açma doğrulama onaylamak için bir PIN gerektiriyorsa, bunu girin.

   ![Bir PIN girme kutusu](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. PIN girişi tamamlandıktan sonra Seç **Kapat**. Bu noktada Doğrulamanızın başarılı olması.
9. Erişim tooyour mobil uygulamayı kaybetmeniz durumunda cep telefonu numaranızı girin öneririz. Merhaba aşağı açılan listeden ülkenizi belirtin ve cep telefonu numaranızı hello kutusunu sonraki toohello ülke adı girin. Seçin **sonraki**.
10. Bu noktada, tarayıcı olmayan uygulamaları Outlook 2010 gibi veya daha eski veya Apple cihazlarda hello yerel e-posta uygulaması için uygulama parolaları yukarı istendiğinde tooset var. Bazı uygulamalar iki aşamalı doğrulamayı desteklemeyen olmasıdır. Bu uygulamaları kullanmıyorsanız tıklatın **Bitti** ve hello adımları hello kalanını atlayın.
11. Bu uygulamalar kullanıyorsanız, kopyalama hello uygulama parolası sağlanan ve normal parolanız yerine uygulamanıza yapıştırın. Merhaba kullanabileceğiniz birden fazla uygulama için aynı uygulama parolası. Daha fazla bilgi için [Yardım ile uygulama parolaları].
12. **Bitti**’ye tıklayın.

### <a name="add-an-account-manually"></a>Hesap el ile Ekle
Tooadd bir hesabı toohello mobil uygulamasını el ile Merhaba QR reader'ı kullanarak yerine isterseniz şu adımları izleyin.

1. Select hello **hesabını el ile girin** düğmesi.  
2. Gösteren aynı sayfa üzerinde hello hello sağlanan barkod Hello kodu ve hello URL'yi girin. Bu bilgileri hello gider **kod** ve **URL** hello mobil uygulama kutuları.

    ![Kurulum](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Merhaba etkinleştirme sona erdiğinde seçin **kişi benim**. Bu adım, bir bildirim veya bir doğrulama kodu tooyour telefon gönderir. Seçin **doğrulayın**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Merhaba iletişim yönteminiz olarak cep telefonunuza kullanın
1. Seçin **kimlik doğrulama telefon** hello aşağı açılan listeden.  

    ![Kurulum](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Merhaba aşağı açılan listeden ülkenizi seçin ve cep telefonu numaranızı girin.
3. Cep telefonunuz ile - metin veya arama toouse tercih hello yöntemi seçin.
4. Seçin **kişi benim** tooverify telefon numaranızı. Seçtiğiniz hello modunun bağlı olarak bir metin göndermek veya çağırın. Merhaba ekranında hello yönergelerini izleyin ve ardından **doğrula**.
5. Bu noktada, tarayıcı olmayan uygulamaları Outlook 2010 gibi veya daha eski veya Apple cihazlarda hello yerel e-posta uygulaması için uygulama parolaları yukarı istendiğinde tooset var. Bazı uygulamalar iki aşamalı doğrulamayı desteklemeyen olmasıdır. Bu uygulamaları kullanmıyorsanız tıklatın **Bitti** ve hello adımları hello kalanını atlayın.
6. Bu uygulamalar kullanıyorsanız, kopyalama hello uygulama parolası sağlanan ve normal parolanız yerine uygulamanıza yapıştırın. Merhaba kullanabileceğiniz birden fazla uygulama için aynı uygulama parolası. Daha fazla bilgi için [Yardım ile uygulama parolaları].
7. **Bitti**’ye tıklayın.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Merhaba iletişim yönteminiz olarak ofis telefonunuza kullanın
1. Seçin **ofis telefonu** hello açılan gelen  

    ![Kurulum](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. Merhaba telefon numarası kutusu şirket iletişim bilgileri ile otomatik olarak doldurulur. Merhaba numarası eksik veya yanlış ise, yöneticinizden toomake değişiklikleri isteyin.
3. Seçin **kişi benim** tooverify telefon numaranızı ve biz çağıracaktır numaranızı. Merhaba ekranında hello yönergelerini izleyin ve ardından **doğrula**.
4. Bu noktada, tarayıcı olmayan uygulamaları Outlook 2010 gibi veya daha eski veya Apple cihazlarda hello yerel e-posta uygulaması için uygulama parolaları yukarı istendiğinde tooset var. Bazı uygulamalar iki aşamalı doğrulamayı desteklemeyen olmasıdır. Bu uygulamaları kullanmıyorsanız tıklatın **Bitti** ve hello adımları hello kalanını atlayın.
5. Bu uygulamalar kullanıyorsanız, kopyalama hello uygulama parolası sağlanan ve normal parolanız yerine uygulamanıza yapıştırın. Merhaba kullanabileceğiniz birden fazla uygulama için aynı uygulama parolası. Daha fazla bilgi için bkz: [uygulama parolaları nedir](multi-factor-authentication-end-user-app-passwords.md).
6. **Bitti**’ye tıklayın.

## <a name="next-steps"></a>Sonraki adımlar
* Tercih edilen seçeneklerinizi değiştirin ve [iki aşamalı doğrulama için ayarlarınızı yönetme](multi-factor-authentication-end-user-manage-settings.md)
* Ayarlanan [uygulama parolaları](multi-factor-authentication-end-user-app-passwords.md) iki aşamalı doğrulamayı desteklemeyen yerel cihaz uygulamaları için.
* Merhaba denetleyin [Microsoft Authenticator uygulaması](microsoft-authenticator-app-how-to.md) bile hücre hizmeti olmadığında hızlı ve güvenli kimlik doğrulaması.
