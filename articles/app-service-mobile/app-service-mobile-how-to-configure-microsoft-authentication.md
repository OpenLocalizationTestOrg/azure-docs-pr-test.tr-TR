---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Microsoft Account kimlik doğrulaması"
description: "Bilgi nasıl tooconfigure Microsoft Account kimlik uygulama hizmetleri uygulamanız için."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Nasıl tooconfigure App Service uygulama toouse Microsoft Account oturum açma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Microsoft Account bir kimlik doğrulama sağlayıcısı olarak. 

## <a name="register-microsoft-account"></a>Microsoft hesabı ile uygulamanızı kaydetme
1. Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin. Kopyalama, **URL**, daha sonra uygulamanızı tooconfigure Microsoft Account kullanırsınız.
2. Toohello gidin [uygulamalarım] sayfasında hello Microsoft Account Developer Center'da ve oturum Microsoft hesabınızla gerekiyorsa.
3. Tıklatın **bir uygulama ekleyin**, bir uygulama adı yazın ve tıklayın **uygulaması oluşturma**.
4. Merhaba Not **uygulama kimliği**, daha sonra ihtiyacınız olacak şekilde. 
5. "Platformları altında" **eklemek Platform** ve "Web"'i seçin.
6. "Yeniden yönlendirme URI'ler" tedarik hello uç nokta altında uygulamanız için ardından **kaydetmek**. 
   
   > [!NOTE]
   > URI'dir hello URL hello yolu ile eklenen, uygulamanızın, yeniden yönlendirme */.auth/login/microsoftaccount/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Merhaba HTTPS şeması kullandığınızdan emin olun.
   
7. "Uygulama parolaları" altında tıklatın **yeni bir parola oluşturmak**. Görünen hello değeri not edin. Merhaba sayfayı çıktıktan sonra bir yeniden görüntülenmeyecek.

    > [!IMPORTANT]
    > Merhaba, önemli güvenlik kimlik bilgisi paroladır. Merhaba parolanızı kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.

## <a name="secrets"></a>Microsoft hesabı Ekle bilgi tooyour uygulama hizmeti uygulaması
1. Merhaba edilene [Azure portal], tooyour uygulama gidin, tıklatın **ayarları** > **kimlik doğrulama / yetkilendirme**.
2. Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, bu geçiş **üzerinde**.
3. Tıklatın **Microsoft hesabı**. Daha önce edindiğiniz hello uygulama kimliği ve parola değerler içinde yapıştırın ve isteğe bağlı olarak uygulamanızın gerektirdiği herhangi bir kapsam etkinleştirin. Daha sonra, **Tamam**'a tıklayın.
   
    ![][1]
   
    Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
4. Microsoft hesabı tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Microsoft Account**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler yönlendirilir tooMicrosoft hesabı için kimlik doğrulaması.
5. **Kaydet** düğmesine tıklayın.

Artık uygulamanızı kimlik doğrulaması için hazır toouse Microsoft Account bulunur.

## <a name="related-content"></a>İlgili içerik
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[uygulamalarım]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure portal]: https://portal.azure.com/
