---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Facebook kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Facebook kimlik doğrulaması."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Nasıl tooconfigure App Service uygulama toouse Facebook oturum açma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Facebook kimlik doğrulama sağlayıcısı olarak.

Bu konudaki toocomplete hello yordamı, doğrulanmış e-posta adresi ve cep telefonu numarası olan bir Facebook hesabı olması gerekir. Yeni bir Facebook hesabıyla toocreate Git çok[facebook.com].

## <a name="register"></a>Facebook ile uygulamanızı kaydetme
1. Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin. Kopyalama, **URL**. Bu tooconfigure Facebook uygulamanızı kullanır.
2. Başka bir tarayıcı penceresinde toohello gidin [Facebook geliştiriciler] Web sitesi ve, Facebook ile oturum açma hesabı kimlik bilgileri.
3. (İsteğe bağlı) Zaten kaydolmadıysanız tıklatın **uygulamaları** > **kaydetmek geliştirici olarak**, ardından hello İlkesi kabul etmek ve hello kayıt adımları izleyin.
4. Tıklatın **uygulamalarım** > **yeni bir uygulama eklemek** > **Web sitesi** > **atlayın ve uygulama kimliği oluşturma**. 
5. İçinde **görünen adı**, türü, uygulamanız için benzersiz bir ad yazın, **ilgili kişi e-posta**, seçin bir **kategori** uygulamanız için ardından **uygulama kimliği oluşturma**ve hello güvenlik denetimi tamamlayın. Bu yeni Facebook uygulamanız için toohello Geliştirici Pano götürür.
6. "Facebook Login" altında tıklatın **Get Started**. Uygulamanızın eklemek **yeniden yönlendirme URI'si** çok**geçerli OAuth yeniden yönlendirme URI'ler**, ardından **Değişiklikleri Kaydet**. 
   
   > [!NOTE]
   > URI'dir hello URL hello yolu ile eklenen, uygulamanızın, yeniden yönlendirme */.auth/login/facebook/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Merhaba HTTPS şeması kullandığınızdan emin olun.
   > 
   > 
7. Merhaba sol gezinti bölmesinde tıklatın **ayarları**. Hello üzerinde **uygulama gizli anahtarı** alan, tıklatın **Göster**, istenen yeniden hello değerlerini not parolanızı sağlayın **uygulama kimliği** ve **uygulama gizli anahtarı**. Bu sonraki tooconfigure Azure'da uygulamanızı kullanın.
   
   > [!IMPORTANT]
   > Merhaba uygulama gizli anahtarı bir önemli güvenlik kimlik bilgisidir. Bu gizli kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.
   > 
   > 
8. Merhaba kullanılan tooregister Merhaba uygulaması olan Facebook hesabıyla hello uygulamasının bir yöneticidir. Bu noktada, yalnızca Yöneticiler bu uygulamasına oturum açabilir. tooauthenticate diğer Facebook hesapları **uygulama gözden geçirme** ve etkinleştirmek **olun < uygulamanızın-adı > ortak** tooenable genel genel Facebook kimlik doğrulamasını kullanarak erişim.

## <a name="secrets"></a>Ekleme Facebook bilgi tooyour uygulama
1. Merhaba edilene [Azure portal], tooyour uygulama gidin. Tıklatın **ayarları** > **kimlik doğrulama / yetkilendirme**, emin olun **App Service kimlik doğrulaması** olan **üzerinde**.
2. Tıklatın **Facebook**, daha önce edindiğiniz hello uygulama kimliği ve uygulama gizli anahtarı değerler içinde yapıştırın, isteğe bağlı olarak, uygulamanız tarafından gerekli herhangi bir kapsam etkinleştirin ve ardından **Tamam**.
   
    ![][0]
   
    Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
3. = (İsteğe bağlı) toorestrict erişim tooyour site tooonly Facebook tarafından kimliği doğrulanmış kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Facebook**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış kimlik doğrulaması için yeniden yönlendirilen tooFacebook isteklerdir.
4. Yapılandırma kimlik doğrulaması yapıldığında tıklatın **kaydetmek**.

Artık uygulamanızı hazır toouse Facebook kimlik doğrulaması için bulunur.

## <a name="related-content"></a>İlgili içerik
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook geliştiriciler]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure portal]: https://portal.azure.com/
