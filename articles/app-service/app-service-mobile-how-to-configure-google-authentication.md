---
title: "Uygulama Hizmetleri uygulamanız için Google kimlik doğrulamasını yapılandırma"
description: "Uygulama Hizmetleri uygulamanız için Google kimlik doğrulaması yapılandırma konusunda bilgi edinin."
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a>Uygulama hizmeti uygulamanızı Google oturum açma kullanacak şekilde yapılandırma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu Azure App Service Google kimlik doğrulama sağlayıcısı olarak kullanmak üzere yapılandırmak nasıl gösterir.

Bu konudaki yordamı tamamlamak için doğrulanmış e-posta adresine sahip bir Google hesabı olması gerekir. Yeni bir Google hesabı oluşturmak için [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302) adresine gidin.

## <a name="register"></a>Google ile uygulamanızı kaydetme
1. Oturum [Azure portal]ve uygulamanıza gidin. Kopyalama, **URL**, daha sonra Google Uygulamanızı yapılandırmak için kullanın.
2. Gidin [Google API'leri](http://go.microsoft.com/fwlink/p/?LinkId=268303) Web sitesi, Google hesabı kimlik bilgilerinizle oturum tıklatın **proje oluştur**, sağlayın bir **proje adı**, ardından **oluşturma**.
3. Altında **sosyal API'leri** tıklatın **Google + API** ve ardından **etkinleştirmek**.
4. Sol gezinti bölmesinde **kimlik bilgileri** > **OAuth izni ekran**seçeneğini belirleyip, **e-posta adresi**, girin bir **ürün adı**, tıklatıp **kaydetmek**.
5. İçinde **kimlik bilgileri** sekmesini tıklatın, **kimlik bilgileri oluşturma** > **OAuth istemci kimliği**seçeneğini belirleyip **Web uygulaması**.
6. Uygulama hizmeti Yapıştır **URL** , daha önce kopyalanır **yetkili JavaScript çıkış**, ardından, yeniden yönlendirme yapıştırın URI **yeniden yönlendirme URI'si yetkili**. Yeniden yönlendirme URI'si ile yolunun, uygulamanızın URL'dir */.auth/login/google/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/google/callback`. HTTPS şeması kullandığınızdan emin olun. Sonra **Oluştur**’a tıklayın.
7. Sonraki ekranda, istemci kimliği ve istemci gizli anahtarı değerlerini not edin.

    > [!IMPORTANT]
    > Gizli bir önemli güvenlik kimlik bilgisidir. Bu gizli kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.


## <a name="secrets"></a>Uygulamanıza eklemek Google bilgileri
1. Geri [Azure portal], uygulamanıza gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama / yetkilendirme**.
2. Kimlik doğrulama / yetkilendirme özelliği etkin değil, anahtar etkinleştirmek **üzerinde**.
3. Tıklatın **Google**. Daha önce aldığınız uygulama kimliği ve uygulama gizli anahtarı değerler içinde yapıştırın ve isteğe bağlı olarak uygulamanızın gerektirdiği herhangi bir kapsam etkinleştirin. Daha sonra, **Tamam**'a tıklayın.
   
   ![][1]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi üzere site içeriğini ve API'lerini kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
4. (İsteğe bağlı) Sitenize yalnızca Google tarafından kimliği doğrulanmış kullanıcılar için erişimi kısıtlamak üzere koyulan **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** için **Google**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler için Google kimlik doğrulaması için yönlendirilir.
5. **Kaydet** düğmesine tıklayın.

Şimdi uygulamanıza kimlik doğrulaması için Google kullanmak hazırsınız.

## <a name="related-content"></a>İlgili içerik
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure portal]: https://portal.azure.com/

