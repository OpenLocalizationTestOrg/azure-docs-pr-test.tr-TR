---
title: "Uygulama Hizmetleri uygulamanız için Azure Active Directory kimlik doğrulamasını yapılandırma"
description: "Uygulama Hizmetleri uygulamanız için Azure Active Directory kimlik doğrulaması yapılandırma konusunda bilgi edinin."
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
ms.openlocfilehash: fe007fa8640d5641f29dc88f8f3a8ca52a1ca8ae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-azure-active-directory-login"></a>App Service uygulamanızı Azure Active Directory oturum açma bilgilerini kullanacak şekilde yapılandırma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu Azure uygulama Azure Active Directory kimlik doğrulama sağlayıcısı olarak kullanmak üzere nasıl yapılandırılacağını gösterir.

## <a name="express"></a>Yapılandırma Azure hızlı ayarları kullanarak Active Directory
1. İçinde [Azure portal], uygulamanıza gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama/yetkilendirme**.
2. Kimlik doğrulama / yetkilendirme özelliği etkin değil, anahtar etkinleştirmek **üzerinde**.
3. Tıklatın **Azure Active Directory**ve ardından **Express** altında **yönetim modu**.
4. Tıklatın **Tamam** uygulama Azure Active Directory'ye kaydetmek için. Bu yeni bir kayıt oluşturur. Bunun yerine var olan bir kaydı seçmek istiyorsanız, tıklatın **mevcut uygulamayı Seç** arayın ve sonra Kiracı içinde önceden oluşturduğunuz bir kayıt adı.
   Seçin ve kaydın tıklatın **Tamam**. Ardından **Tamam** Azure Active Directory ayarlar dikey penceresinde.
   
   ![][0]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi üzere site içeriğini ve API'lerini kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
5. (İsteğe bağlı) Sitenize yalnızca Azure Active Directory tarafından kimliği doğrulanmış kullanıcılar için erişimi kısıtlamak üzere koyulan **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** için **Azure Active Directory ile oturum aç**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler kimlik doğrulaması için Azure Active Directory'ye yönlendirilir.
6. **Kaydet** düğmesine tıklayın.

Şimdi uygulamanıza kimlik doğrulaması için Azure Active Directory'yi kullanmak hazırsınız.

## <a name="advanced"></a>(Alternatif yöntem) el ile Azure Active Directory ile gelişmiş ayarları yapılandır
Ayrıca yapılandırma ayarlarını sağlamak seçebileceğiniz el ile. Kullanmak istediğiniz bir AAD kiracısı ile Azure'da oturum Kiracı farklı ise, bu tercih edilen bir çözümdür. Yapılandırmayı tamamlamak için önce bir kayıt Azure Active Directory'de oluşturmanız gerekir ve ardından kayıt ayrıntıları bazıları App Service'e sağlamanız gerekir.

### <a name="register"></a>Azure Active Directory ile uygulamanızı kaydetme
1. Oturum [Azure portal]ve uygulamanıza gidin. Kopyalama, **URL**. Azure Active Directory Uygulamanızı yapılandırmak için bunu kullanır.
2. Oturum [Klasik Azure portalı] gidin **Active Directory**.
   
    ![][2]
3. Dizininizi seçin ve ardından **uygulamaları** üst sekmesini. Tıklatın **eklemek** altındaki yeni bir uygulama kaydı oluşturun.
4. Tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
5. Uygulama Ekleme Sihirbazı'nda girin bir **adı** tıklatın ve uygulama için **Web uygulaması ve/veya Web API** türü. Devam etmek için'ye tıklayın.
6. İçinde **oturum açma URL** kutusunda, daha önce kopyaladığınız uygulama URL'sini yapıştırın. Bu aynı URL'yi girin **uygulama kimliği URI'si** kutusu. Devam etmek için'ye tıklayın.
7. Uygulama eklendiğinde tıklatın **yapılandırma** sekmesi. Düzen **yanıt URL'si** altında **çoklu oturum açma** URL yolu ile eklenen, uygulamanızın olması */.auth/login/aad/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/aad/callback`. HTTPS şeması kullandığınızdan emin olun.
   
    ![][3]
8. **Kaydet** düğmesine tıklayın. Ardından kopyalama **istemci kimliği** uygulaması. Uygulamanız bu daha sonra kullanmak üzere yapılandırır.
9. Altındaki komut çubuğunda, **uç noktalarını görüntüle**ve ardından kopyalama **Federasyon meta veri belgesi** URL ve belge ya da bir tarayıcıda gitmek indirme.
10. Kök içinde **EntityDescriptor** öğesi olmamalıdır bir **Entityıd** özniteliği formun `https://sts.windows.net/` bir GUID belirli kiracınıza ("Kiracı kimliği" olarak adlandırılır) ve ardından. Bu değer kopyalama - olarak hizmet verecektir, **veren URL'si**. Uygulamanız bu daha sonra kullanmak üzere yapılandırır.

### <a name="secrets"></a>Uygulamanıza eklemek Azure Active Directory bilgileri
1. Geri [Azure portal], uygulamanıza gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama/yetkilendirme**.
2. Kimlik doğrulama/yetkilendirme özelliği etkin değilse, anahtar etkinleştirmek **üzerinde**.
3. Tıklatın **Azure Active Directory**ve ardından **Gelişmiş** altında **yönetim modu**. Daha önce edindiğiniz istemci kimliği ve veren URL değeri yapıştırın. Daha sonra, **Tamam**'a tıklayın.
   
   ![][1]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi üzere site içeriğini ve API'lerini kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
4. (İsteğe bağlı) Sitenize yalnızca Azure Active Directory tarafından kimliği doğrulanmış kullanıcılar için erişimi kısıtlamak üzere koyulan **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** için **Azure Active Directory ile oturum aç**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler kimlik doğrulaması için Azure Active Directory'ye yönlendirilir.
5. **Kaydet** düğmesine tıklayın.

Şimdi uygulamanıza kimlik doğrulaması için Azure Active Directory'yi kullanmak hazırsınız.

## <a name="optional-configure-a-native-client-application"></a>(İsteğe bağlı) Yerel istemci uygulaması yapılandırın
Azure Active Directory yerel istemcilerini kaydetmek eşleme izinleri üzerinde daha fazla denetim sağlayan sağlar. Bir kitaplık kullanılarak oturumları gerçekleştirmek isterseniz, bu gereksinim **Active Directory kimlik doğrulama Kitaplığı**.

1. Gidin **Active Directory** içinde [Klasik Azure portalı].
2. Dizininizi seçin ve ardından **uygulamaları** üst sekmesini. Tıklatın **eklemek** altındaki yeni bir uygulama kaydı oluşturun.
3. Tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
4. Uygulama Ekleme Sihirbazı'nda girin bir **adı** tıklatın ve uygulama için **yerel istemci uygulaması** türü. Devam etmek için'ye tıklayın.
5. İçinde **yeniden yönlendirme URI'si** kutusuna, sitenizin girin */.auth/login/done* uç noktasını, HTTPS şeması kullanarak. Bu değer benzer olmalıdır *https://contoso.azurewebsites.net/.auth/login/done*. Bir Windows uygulaması kullanmak yerine oluşturuyorsanız [SID paketini](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) URI olarak.
6. Yerel uygulama eklendiğinde tıklatın **yapılandırma** sekmesi. Bul **istemci kimliği** ve bu değeri not edin.
7. Sayfayı aşağı kaydırın **diğer uygulamalara izinler** 'ye tıklayın **uygulama eklemek**.
8. Daha önce kaydettiğiniz web uygulaması için arama ve artı simgesine tıklayın. Onay iletişim kutusunu kapatmak için'ye tıklayın. Web uygulaması bulunamadı, kayıt için gidin ve yeni bir yanıt URL'si (örn., HTTP sürümü geçerli URL'niz) eklemek bulamazsa, Kaydet'i tıklatın ve ardından aşağıdaki adımları tekrarlayın.-uygulama listesinde göstermelidir.
9. Yeni eklediğiniz yeni girişinde açmak **izinlere temsilci** açılır ve seçin **erişim (appName)**. Daha sonra **Kaydet**'e tıklayın.

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
