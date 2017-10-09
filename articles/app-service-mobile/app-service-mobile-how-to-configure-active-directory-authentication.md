---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Azure Active Directory kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Azure Active Directory kimlik doğrulaması."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Nasıl tooconfigure App Service uygulama toouse Azure Active Directory oturum açma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu, nasıl gösterir tooconfigure Azure App Services toouse Azure Active Directory kimlik doğrulama sağlayıcısı olarak.

## <a name="express"></a>Yapılandırma Azure hızlı ayarları kullanarak Active Directory
1. Merhaba, [Azure portal], tooyour uygulama gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama/yetkilendirme**.
2. Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, hello anahtar çok kapatma**üzerinde**.
3. Tıklatın **Azure Active Directory**ve ardından **Express** altında **yönetim modu**.
4. Tıklatın **Tamam** tooregister hello uygulama Azure Active Directory'de. Bu yeni bir kayıt oluşturur. Toochoose var olan bir kaydı yerine istiyorsanız, **mevcut uygulamayı Seç** arayın ve sonra Kiracı içinde önceden oluşturduğunuz bir kayıt hello adı.
   Merhaba kayıt tooselect onu ve tıklatın **Tamam**. Ardından **Tamam** hello Azure Active Directory ayarları dikey.
   
   ![][0]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
5. Azure Active Directory tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Azure Active Directory ile oturum aç**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış yeniden yönlendirilen tooAzure Active Directory kimlik doğrulaması için isteklerdir.
6. **Kaydet** düğmesine tıklayın.

Artık uygulamanızı hazır toouse Azure Active Directory kimlik doğrulaması için bulunur.

## <a name="advanced"></a>(Alternatif yöntem) el ile Azure Active Directory ile gelişmiş ayarları yapılandır
Ayrıca yapılandırma ayarlarını tooprovide tercih edebilirsiniz el ile. Azure'da oturum hello Kiracı toouse istediğiniz hello AAD kiracısı farklıysa, bu tercih edilen hello çözümdür. toocomplete hello yapılandırma, ilk Azure Active Directory'de bir kayıt oluşturmalısınız ve ardından hello kayıt ayrıntıları tooApp hizmet bazıları sağlamalısınız.

### <a name="register"></a>Azure Active Directory ile uygulamanızı kaydetme
1. Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin. Kopyalama, **URL**. Azure Active Directory uygulamanız bu tooconfigure kullanır.
2. İçinde toohello oturum [Klasik Azure portalı] ve çok gidin**Active Directory**.
   
    ![][2]
3. Dizininizi seçin ve ardından hello seçin **uygulamaları** sekmesini hello üstünde. Tıklatın **ekleme** hello alt toocreate yeni bir uygulama kaydı sırasında.
4. Tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
5. İçinde uygulama Ekleme Sihirbazı Merhaba, girin bir **adı** uygulama ve tıklatın hello için **Web uygulaması ve/veya Web API** türü. Toocontinue'ye tıklayın.
6. Merhaba, **oturum açma URL** kutusunda, daha önce kopyaladığınız hello uygulama URL'sini yapıştırın. Hello aynı URL'yi girin **uygulama kimliği URI'si** kutusu. Toocontinue'ye tıklayın.
7. Merhaba uygulaması eklendiğinde hello tıklatın **yapılandırma** sekmesi. Merhaba Düzenle **yanıt URL'si** altında **çoklu oturum açma** toobe hello URL hello yolu ile eklenen, uygulamanızın */.auth/login/aad/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Merhaba HTTPS şeması kullandığınızdan emin olun.
   
    ![][3]
8. **Kaydet** düğmesine tıklayın. Ardından kopya hello **istemci kimliği** hello uygulaması. Uygulama toouse yapılandıracak bu daha sonra.
9. Merhaba altındaki komut çubuğunda, **uç noktalarını görüntüle**ve ardından kopyalama hello **Federasyon meta veri belgesi** URL ve belge ya da bir tarayıcıda tooit gidin indirme.
10. Merhaba kök içinde **EntityDescriptor** öğesi olması gerekir bir **Entityıd** özniteliği hello formun `https://sts.windows.net/` ("Kiracı kimliği" olarak adlandırılır) bir GUID belirli tooyour Kiracı tarafından izlenen. Bu değer kopyalama - olarak hizmet verecektir, **veren URL'si**. Uygulama toouse yapılandıracak bu daha sonra.

### <a name="secrets"></a>Eklemek Azure Active Directory bilgileri tooyour uygulama
1. Merhaba edilene [Azure portal], tooyour uygulama gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama/yetkilendirme**.
2. Merhaba kimlik doğrulama/yetkilendirme özelliği etkin değilse hello anahtar çok kapatma**üzerinde**.
3. Tıklatın **Azure Active Directory**ve ardından **Gelişmiş** altında **yönetim modu**. Merhaba istemci kimliği yapıştırın ve veren URL'si, daha önce edindiğiniz değeri. Daha sonra, **Tamam**'a tıklayın.
   
   ![][1]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
4. Azure Active Directory tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Azure Active Directory ile oturum aç**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış yeniden yönlendirilen tooAzure Active Directory kimlik doğrulaması için isteklerdir.
5. **Kaydet** düğmesine tıklayın.

Artık uygulamanızı hazır toouse Azure Active Directory kimlik doğrulaması için bulunur.

## <a name="optional-configure-a-native-client-application"></a>(İsteğe bağlı) Yerel istemci uygulaması yapılandırın
Azure Active Directory tooregister yerel istemciler, eşleme izinleri üzerinde daha fazla denetim sağlayan sağlar. Hello gibi bir kitaplık kullanılarak tooperform oturumları istiyorsanız bu gereksinim **Active Directory kimlik doğrulama Kitaplığı**.

1. Çok gidin**Active Directory** hello içinde [Klasik Azure portalı].
2. Dizininizi seçin ve ardından hello seçin **uygulamaları** sekmesini hello üstünde. Tıklatın **ekleme** hello alt toocreate yeni bir uygulama kaydı sırasında.
3. Tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
4. İçinde uygulama Ekleme Sihirbazı Merhaba, girin bir **adı** uygulama ve tıklatın hello için **yerel istemci uygulaması** türü. Toocontinue'ye tıklayın.
5. Merhaba, **yeniden yönlendirme URI'si** kutusuna, sitenizin girin */.auth/login/done* hello HTTPS şeması kullanarak uç nokta. Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*. Bir Windows uygulaması oluşturma, bunun yerine hello kullanırsanız [SID paketini](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) URI hello gibi.
6. Merhaba yerel uygulaması eklendiğinde hello tıklatın **yapılandırma** sekmesi. Hello bulur **istemci kimliği** ve bu değeri not edin.
7. Merhaba sayfa toohello aşağı **izinleri tooother uygulamaları** 'ye tıklayın **uygulama eklemek**.
8. Daha önce kaydettiğiniz hello web uygulaması için arama ve hello artı simgesine tıklayın. Merhaba onay tooclose hello iletişim'ye tıklayın. Merhaba web uygulaması bulunamadı, tooits kayıt gidin ve yeni bir yanıt URL'si (örn., hello HTTP sürümü geçerli URL'niz) eklemek bulamazsa, Kaydet'i tıklatın ve ardından bu adımları yineleyin - Merhaba uygulaması hello listesinde göstermelidir.
9. Yeni eklediğiniz hello yeni girişte hello açmak **izinlere temsilci** açılır ve seçin **erişim (appName)**. Daha sonra **Kaydet**'e tıklayın.

Uygulama hizmeti uygulamanızı erişebileceğiniz bir yerel istemci uygulaması artık yapılandırdınız.

## <a name="related-content"></a>İlgili içerik
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[Azure portal]: https://portal.azure.com/
[Klasik Azure portalı]: https://manage.windowsazure.com/
[alternative method]:#advanced
