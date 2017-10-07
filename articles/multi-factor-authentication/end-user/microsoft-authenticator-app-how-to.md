---
title: "cep telefonları için aaaMicrosoft Authenticator uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooupgrade toohello en son sürümünü Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Merhaba Microsoft Authenticator uygulaması ile çalışmaya başlama
Merhaba Microsoft Authenticator uygulaması bir ek düzeyi iş veya Okul hesabınızda güvenlik sunar (örneğin, bsimon@contoso.com) veya Microsoft hesabınızı (örneğin, bsimon@outlook.com).

Merhaba uygulaması iki yoldan biriyle çalışır:

* **Bildirim**. Merhaba uygulama, yetkisiz erişim tooaccounts önlemek ve bildirim tooyour akıllı telefon veya tablet ileterek sahte işlemleri durdurun yardımcı olabilir. Yalnızca hello bildirim görüntüleyin ve işlem meşru ise seçin **doğrula**. Aksi takdirde, seçebileceğiniz **reddetme**. 
* **Doğrulama kodu**. Merhaba uygulaması bir OAuth doğrulama kodu toogenerate bir yazılım belirteci olarak kullanılabilir. Kullanıcı adınızı ve parolanızı girdikten sonra oturum açma hello ekranına hello uygulama tarafından sağlanan hello kodu girin. Merhaba doğrulama kodu ikinci bir form kimlik doğrulaması sağlar.

Merhaba Microsoft Authenticator uygulaması hello Azure Authenticator uygulamasını yerini alır. Hello Azure Authenticator uygulamasını hala çalışıyor, ancak toomove toohello yeni Microsoft Authenticator uygulaması karar verirseniz, bu makale size yardımcı olabilir.  

## <a name="opt-in-for-two-step-verification"></a>İki aşamalı doğrulama için kabul

Merhaba Microsoft Authenticator uygulamasını kendi başına çalışmaz. Her kullanıcı adı ve parola ile oturum çalıştırdıktan sonra ikinci bir doğrulama yöntemi için hesapları tooprompt yapılandırın. 

Bir iş veya Okul hesabı için genellikle toochoose bu özellik kendiniz elde etmezsiniz. Bunun yerine, bir güvenlik yöneticisi sizin adınıza kabul eder ve bunu tooregister doğrulama yöntemlerini hesabınız için size bildirir. Bu senaryo tooyou geçerliyse, daha fazla bilgi edinin [ne Azure çok faktörlü kimlik doğrulaması için beni anlamına gelmez](multi-factor-authentication-end-user.md).

Kişisel bir hesap için kendiniz için iki aşamalı doğrulamayı yukarı tooset gerekir. Bir Microsoft hesabınız varsa, bu adımları kullanılabilir olan [iki basamaklı doğrulama hakkında](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

Microsoft olmayan hesapların ile Merhaba Microsoft Authenticator de kullanabilirsiniz. Bunlar hello özelliği iki aşamalı doğrulama dışında bir şey çağırabilir ancak mümkün toofind olması gereken güvenlik veya oturum açma ayarları altında. 

## <a name="install-hello-app"></a>Merhaba uygulamasını yükleyin
Merhaba Microsoft Authenticator uygulaması için kullanılabilir [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), ve [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Hesapları toohello uygulama Ekle
Tooadd toohello Microsoft Authenticator uygulamasını istediğiniz her hesap için aşağıdaki yordamlarını hello birini kullanın:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Kişisel bir Microsoft hesabı toohello uygulamasını ekleme

Kişisel bir Microsoft hesabı (bir toosign kullanmak tooOutlook.com içinde Xbox, Skype, vb.), tüm toodo sahip olduğu hello Microsoft Authenticator uygulaması tooyour hesabında oturum açın.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Bir iş veya Okul hesabı toohello uygulamasını hello QR kodu tarayıcı kullanarak
1. Toohello güvenlik doğrulama ayarları ekranına gidin.  Hakkında bilgi için tooget toothis ekran bkz [güvenlik ayarlarınızı değiştirme](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Merhaba sonraki çok onay kutusunu**Doğrulayıcı uygulama** seçip **yapılandırma**.

    ![Merhaba Yapılandır düğmesine hello güvenlik doğrulama ayarları ekranı](./media/authenticator-app-how-to/azureauthe.png)

    Bu bir QR kodu içeren bir ekrana getirir.

    ![Merhaba QR kodu sağlar ekranı](./media/authenticator-app-how-to/barcode2.png)
3. Açık hello Microsoft Authenticator uygulaması. Merhaba üzerinde **hesapları** ekran, select  **+** ve ardından iş veya Okul hesabı tooadd istediğinizi belirtin.
4. Merhaba kamera tooscan hello QR kodu kullanın ve ardından **Bitti** tooclose hello QR kodu ekran.

    Kameranızı düzgün çalışmıyorsa, yapabilecekleriniz [hello QR kodu ve URL'yi elle girin](#add-an-account-to-the-app-manually).

5. Hello uygulama hesap adınızı ile bunun altındaki altı rakamlı bir kod gösterdiğinde bitirdiniz. 

    ![Hesapları ekranı](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Bir hesabı toohello uygulamasını el ile Ekle
1. Toohello güvenlik doğrulama ayarları ekranına gidin.  Hakkında bilgi için tooget toothis ekran bkz [güvenlik ayarlarınızı değiştirme](multi-factor-authentication-end-user-manage-settings.md).
2. Seçin **yapılandırma**.

    ![Merhaba Yapılandır düğmesine hello güvenlik doğrulama ayarları ekranı](./media/authenticator-app-how-to/azureauthe.png)

    Bu bir QR kodu içeren bir ekrana getirir.  Merhaba kodu ve URL unutmayın.

    ![Merhaba QR kodu ve URL sağlayan ekran](./media/authenticator-app-how-to/barcode2.png)
3. Açık hello Microsoft Authenticator uygulaması. Merhaba üzerinde **hesapları** ekran, select  **+** ve ardından iş veya Okul hesabı tooadd istediğinizi belirtin.

4. Merhaba tarayıcıda seçin **kodu el ile girmeniz**.

    ![QR kodu taraması için ekran](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Hello uygulama uygun kutulara hello Hello kodu ve hello URL'yi girin ve ardından **son**.

    ![Kod ve URL girme ekran](./media/authenticator-app-how-to/manual.png)

6. Hello uygulama hesap adınızı ile bunun altındaki altı rakamlı bir kod gösterdiğinde bitirdiniz.

    ![Hesapları ekranı](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Touch ID kullanarak bir hesap toohello uygulama ekleyin
Touch ID ios'ta Hello Microsoft Authenticator uygulaması destekler  Azure çok faktörlü kimlik doğrulaması kuruluşlar toorequire cihazlar için bir PIN verir. Touch ID ile iOS kullanıcıları tooenter bir PIN gerek yoktur. Bunun yerine, bunlar parmak izini tarayabilir ve seçin **Onayla**.

Touch ID Microsoft Authenticator ile ayarlama basit bir işlemdir. Bir PIN ile normal doğrulama sınamasını tamamlayın. Cihazınızı Touch ID destekliyorsa, Microsoft Authenticator onu otomatik olarak o hesap için ayarlar.

![Touch ID kurulumunun doğrulama](./media/authenticator-app-how-to/touchid1.png)

Noktasındaki İleri, bunu olduğunuzda, oturum açma, tooverify gerekli alınan hello anında iletme bildirimini seçin ve PIN'İNİZİ girmek yerine parmak izinizi tarama.

![Anında iletme bildirimi](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Oturum açtığınızda hello uygulama kullanma

Hesabınızı toohello uygulama eklendikten sonra istendiğinde toodo test doğrulama toomake her şeyin doğru şekilde yapılandırıldığından emin olabilir. Bundan sonra tamamladınız! Merhaba sonraki sefer oturum açtığınızda kadar toodo başka bir şey gerekmez.

Merhaba uygulamada doğrulama kodları toouse seçerseniz, toosee Başlat hello giriş sayfasında bunları. Bir gereksinim duyduğunuzda, böylece her zaman yeni bir kod sahip oldukları her 30 saniyede değiştirin. Ancak oturum açın ve bir doğrulama kodu istendiğinde tooenter olduğu kadar toodo onlarla herhangi bir şey gerekmez.  
