---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Google kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Google kimlik doğrulaması."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Nasıl tooconfigure App Service uygulama toouse Google oturum açma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Google kimlik doğrulama sağlayıcısı olarak.

Bu konudaki toocomplete hello yordamı, doğrulanmış e-posta adresine sahip bir Google hesabı olması gerekir. Yeni bir Google hesabı toocreate Git çok[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Google ile uygulamanızı kaydetme
1. Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin. Kopyalama, **URL**, hangi Google uygulamanızı sonraki tooconfigure kullanın.
2. Toohello gidin [Google API'leri](http://go.microsoft.com/fwlink/p/?LinkId=268303) Web sitesi, Google hesabı kimlik bilgilerinizle oturum tıklatın **proje oluştur**, sağlayın bir **proje adı**, ardından  **Oluşturma**.
3. Altında **sosyal API'leri** tıklatın **Google + API** ve ardından **etkinleştirmek**.
4. Sol gezinti, hello içinde **kimlik bilgileri** > **OAuth izni ekran**seçeneğini belirleyip, **e-posta adresi**, girin bir **Ürünadı**, tıklatıp **kaydetmek**.
5. Merhaba, **kimlik bilgileri** sekmesini tıklatın, **kimlik bilgileri oluşturma** > **OAuth istemci kimliği**seçeneğini belirleyip **Web uygulaması**.
6. Yapıştır hello uygulama hizmeti **URL** , daha önce kopyalanır **yetkili JavaScript çıkış**, ardından, yeniden yönlendirme yapıştırın URI **yeniden yönlendirme URI'si yetkili**. URI'dir hello URL hello yolu ile eklenen, uygulamanızın yeniden yönlendirme hello */.auth/login/google/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/google/callback`. Merhaba HTTPS şeması kullandığınızdan emin olun. Sonra **Oluştur**’a tıklayın.
7. Merhaba sonraki ekranda, kimliği ve istemci gizli anahtarı hello istemci hello değerlerini not edin.

    > [!IMPORTANT]
    > Merhaba gizli bir önemli güvenlik kimlik bilgisidir. Bu gizli kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.


## <a name="secrets"></a>Ekleme Google bilgi tooyour uygulama
1. Merhaba edilene [Azure portal], tooyour uygulama gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama / yetkilendirme**.
2. Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, hello anahtar çok kapatma**üzerinde**.
3. Tıklatın **Google**. Daha önce edindiğiniz hello uygulama kimliği ve uygulama gizli anahtarı değerler içinde yapıştırın ve isteğe bağlı olarak uygulamanızın gerektirdiği herhangi bir kapsam etkinleştirin. Daha sonra, **Tamam**'a tıklayın.
   
   ![][1]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
4. Google tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Google**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış kimlik doğrulaması için yeniden yönlendirilen tooGoogle isteklerdir.
5. **Kaydet** düğmesine tıklayın.

Artık uygulamanızı kimlik doğrulaması için hazır toouse Google bulunur.

## <a name="related-content"></a>İlgili içerik
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure portal]: https://portal.azure.com/

