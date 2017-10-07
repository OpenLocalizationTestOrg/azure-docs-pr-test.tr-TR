---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Twitter kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Twitter kimlik doğrulaması."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Nasıl tooconfigure App Service uygulama toouse Twitter oturum açma
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Twitter bir kimlik doğrulama sağlayıcısı olarak.

Bu konudaki toocomplete hello yordamı, bir doğrulanmış e-posta adresi ve telefon numarası olan bir Twitter hesabı olması gerekir. Yeni bir Twitter hesabı toocreate Git çok<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Twitter ile uygulamanızı kaydetme
1. Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin. Kopyalama, **URL**. Twitter uygulamanız bu tooconfigure kullanır.
2. Toohello gidin [Twitter geliştiriciler] Web sitesi, Twitter hesabı kimlik bilgilerinizle oturum açın ve tıklatın **yeni uygulama oluşturma**.
3. Merhaba türü **adı** ve **açıklama** yeni uygulamanız için. Uygulamanızın Yapıştır **URL** hello için **Web sitesi** değeri. Ardından, hello **geri çağırma URL'si**, hello Yapıştır **geri çağırma URL'si** daha önce kopyaladığınız. Merhaba yolunun ile mobil uygulama ağ geçidi budur */.auth/login/twitter/callback*. Örneğin, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Merhaba HTTPS şeması kullandığınızdan emin olun.
4. Merhaba alt hello sayfasında hello koşullarını okuyup kabul edin. Ardından **Twitter uygulamanızı oluşturma**. Bu kayıtları hello uygulama hello uygulama ayrıntılarını görüntüler.
5. Hello tıklatın **ayarları** sekmesi, onay **bu uygulama kullanılan toobe toosign Twitter oturum izin**, ardından **güncelleştirme ayarlarını**.
6. Select hello **anahtarları ve erişim belirteçleri** sekmesi. Merhaba değerlerini Not **tüketici anahtarı (API anahtarı)** ve **tüketici gizli anahtarı (API gizli)**.
   
   > [!NOTE]
   > Merhaba tüketici gizli bir önemli güvenlik kimlik bilgisidir. Bu gizli kimseyle paylaşmayın değil veya uygulamanızla dağıtabilirsiniz.
   > 
   > 

## <a name="secrets"></a>Ekleme Twitter bilgi tooyour uygulama
1. Merhaba edilene [Azure portal], tooyour uygulama gidin. Tıklatın **ayarları**ve ardından **kimlik doğrulama / yetkilendirme**.
2. Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, hello anahtar çok kapatma**üzerinde**.
3. Tıklatın **Twitter**. Daha önce edindiğiniz değerleri Hello uygulama kimliği ve uygulama gizli anahtarı yapıştırın. Daha sonra, **Tamam**'a tıklayın.
   
   ![][1]
   
   Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz. Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.
4. Twitter tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Twitter**. Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış kimlik doğrulaması için yeniden yönlendirilen tooTwitter isteklerdir.
5. **Kaydet** düğmesine tıklayın.

Artık uygulamanızı kimlik doğrulaması için hazır toouse Twitter bulunur.

## <a name="related-content"></a>İlgili içerik
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter geliştiriciler]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure portal]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
