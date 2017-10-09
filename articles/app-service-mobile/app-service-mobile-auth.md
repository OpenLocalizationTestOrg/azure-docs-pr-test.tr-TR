---
title: aaaAuthentication ve Azure Mobile Apps yetkilendirme | Microsoft Docs
description: "Kavramsal başvurusu ve genel bakış hello kimlik doğrulama / yetkilendirme özelliğini Azure Mobile Apps için"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Azure Mobile Apps’te Kimlik Doğrulama ve Yetkilendirme
## <a name="what-is-app-service-authentication--authorization"></a>App Service kimlik doğrulaması nedir / yetkilendirme?
> [!NOTE]
> Bu konu geçirilen tooa birleştirilmiş olacaktır [App Service kimlik doğrulama / yetkilendirme](../app-service/app-service-authentication-overview.md) Web, mobil ve API Apps kapsayan konu.
> 
> 

App Service kimlik doğrulama / yetkilendirme hello uygulama arka uçta gerekli kod değişikliğine kullanıcılar, uygulama toolog sağlayan bir özelliktir. Bir kolay bir yolu tooprotect, uygulama ve iş ile kullanıcı başına veri sağlar.

Uygulama hizmeti, federe kimlik kullanan bir 3. taraf **kimlik sağlayıcısı** ("IDP") hesaplarını depolayan ve kullanıcıların kimliğini doğrular ve hello uygulamanın kullandığı bu kimliği kendi yerine. Uygulama hizmeti hello kutusu dışında beş kimlik sağlayıcılarını destekler: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, ve *Twitter*. Bu destek, uygulamalarınız için başka bir kimlik sağlayıcısı veya kendi özel kimlik çözümü ile tümleştirerek genişletebilirsiniz.

Son kullanıcılarınızın nasıl oturum seçeneklerini sağlayabilmesi için uygulamanız bu kimlik sağlayıcıları herhangi bir sayıda yararlanabilirsiniz.

Hemen kullanmaya tooget istiyorsanız, lütfen aşağıdaki öğreticiler hello birine bakın:

* [Kimlik doğrulama tooyour iOS uygulaması ekleyin]
* [Kimlik doğrulama tooyour Xamarin.iOS uygulaması ekleyin]
* [Kimlik doğrulama tooyour Xamarin.Android uygulaması ekleyin]
* [Kimlik doğrulaması tooyour Windows uygulaması Ekle]

## <a name="how-authentication-works"></a>Kimlik doğrulaması nasıl çalışır
Merhaba kimlik sağlayıcılardan birini kullanarak sipariş tooauthenticate içinde önce uygulamanız hakkında tooconfigure hello kimlik sağlayıcısı tooknow gerekir. Merhaba kimlik sağlayıcısı sonra kimlikleri ve geri toohello uygulama sağladığınız gizli sağlayacaktır. Bu hello güven ilişkisi tamamlandıktan ve uygulama hizmeti toovalidate sağlanan kimlikleri tooit sağlar.

Bu adımlar aşağıdaki konularda hello ayrıntılı olarak açıklanmaktadır:

* [Nasıl tooconfigure uygulama toouse Azure Active Directory oturum açma]
* [Nasıl tooconfigure uygulama toouse Facebook oturum açma]
* [Nasıl tooconfigure uygulama toouse Google oturum açma]
* [Nasıl tooconfigure uygulama toouse Microsoft Account oturum açma]
* [Nasıl tooconfigure uygulama toouse Twitter oturum açma]

Her şeyi hello arka uçta yapılandırıldıktan sonra istemci toolog değiştirebilirsiniz. Burada iki yaklaşım vardır:

* Tek satırlık bir kod kullanarak, kullanıcılar hello Mobile Apps istemci SDK oturum sağlar.
* Erişim tooApp hizmet kazanmak ve belirtilen kimlik sağlayıcısı tooestablish kimliği tarafından yayımlanan SDK yararlanın.

> [!TIP]
> Çoğu uygulama sağlayıcısı SDK tooget yerel-duyguyu'açığa fazla oturum açma deneyimi ve tooleverage yenileme desteği ve başka bir sağlayıcıya özgü avantajları kullanmanız gerekir.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>SDK sağlayıcı olmadan kimlik doğrulaması nasıl çalışır
SDK sağlayıcı yukarı tooset istemiyorsanız, sizin için Mobile Apps tooperform hello oturum açma izin verebilirsiniz. Merhaba Mobile Apps istemci SDK'sı seçme ve eksiksiz hello oturum açma web görünümü toohello sağlayıcısının açılır. Bazen bloglar ve forumlar görürsünüz bu tooas hello "sunucu akış" başvurulan veya hello sunucu itibaren "akış sunucusu yönlendirilmiş" Merhaba oturum açma yönetme ve hello istemci SDK hello sağlayıcı belirteci hiçbir zaman alır.

Merhaba kod hello kimlik doğrulaması öğreticide her platform için bu akışı kapsamdaki toostart gerekli. Sonunda hello hello akış, bir uygulama hizmeti belirteci hello istemci SDK'sı vardır ve otomatik olarak eklenen tooall istekleri toohello arka uç hello belirteç olur.

### <a name="how-authentication-with-a-provider-sdk-works"></a>Kimlik doğrulama sağlayıcısı SDK ile nasıl çalışır
Bir sağlayıcı SDK ile çalışmaya hello oturum açma deneyimi toointeract daha sıkı işletim sistemi hello uygulamayı çalıştıran hello platformuyla sağlar. Bu ayrıca, bir sağlayıcı belirteci ve çok daha kolay tooconsume graph API kolaylaştırır ve hello kullanıcı deneyimini özelleştirme hello istemci üzerindeki bazı kullanıcı bilgileri sunar. Bazen bloglar ve forumlar bu başvurulan tooas hello "istemci akışı" görürsünüz veya "istemci yönlendirilmiş akış" kod itibaren hello istemcide hello oturum açma işleme ve erişim tooa sağlayıcı belirteci hello istemci kodu sahip.

Bir sağlayıcı belirteç alındığında, doğrulama için hizmet tooApp gönderilen toobe gerekir. Sonunda hello hello akış, bir uygulama hizmeti belirteci hello istemci SDK'sı vardır ve otomatik olarak eklenen tooall istekleri toohello arka uç hello belirteç olur. Bu nedenle seçerseniz hello Geliştirici da bir başvuru toohello sağlayıcı belirteci tutabilirsiniz.

## <a name="how-authorization-works"></a>Yetkilendirme nasıl çalışır?
App Service kimlik doğrulama / yetkilendirme için birkaç seçenek sunar **istek kimliği doğrulanmamış olduğunda eylem tootake**. Kodunuzu belirli bir istek alırsa önce hello isteği kimlik doğrulaması uygulama hizmeti onay toosee varsa ve yoksa reddetmek ve yeniden denemeden önce toohave hello kullanıcı oturum açma denemesi.

Kimliği doğrulanmamış toohave istenmesine hello kimlik sağlayıcıları tooone bir seçenektir. Bir web tarayıcısında bu hello kullanıcı tooa yeni sayfa gerçekten kalırsınız. Ancak, mobil istemciniz bu şekilde yönlendirilemez ve kimliği doğrulanmamış yanıtları, bir HTTP alacağı *401 Yetkisiz* yanıt. Bu verildiğinde, hello ilk istek, istemci her zaman toohello oturum açma uç noktası olmalıdır ve daha sonra yapabilirsiniz tooany diğer API'lerini çağırır. Oturum açmayı önce başka bir API toocall çalışırsanız, istemci bir hata alırsınız.

Toohave daha ayrıntılı olarak istiyorsanız hangi uç noktaları kimlik doğrulaması gerektiren denetiminde, aynı zamanda çekme "hiçbir eylem (isteğine izin ver)" kimliği doğrulanmamış istekler için. Bu durumda, tüm kimlik doğrulama kararları ertelenmiş tooyour uygulama kodu. Bu ayrıca, özel yetkilendirme kurallarına göre tooallow erişim toospecific kullanıcıları sağlar.

## <a name="documentation"></a>Belgeler
öğreticiler Göster nasıl aşağıdaki hello tooadd kimlik doğrulaması tooyour mobil istemcilerin uygulama hizmetini kullanarak:

* [Kimlik doğrulama tooyour iOS uygulaması ekleyin]
* [Kimlik doğrulama tooyour Xamarin.iOS uygulaması ekleyin]
* [Kimlik doğrulama tooyour Xamarin.Android uygulaması ekleyin]
* [Kimlik doğrulaması tooyour Windows uygulaması Ekle]

öğreticiler Göster nasıl aşağıdaki hello tooconfigure uygulama hizmeti tooleverage farklı kimlik doğrulama sağlayıcıları:

* [Nasıl tooconfigure uygulama toouse Azure Active Directory oturum açma]
* [Nasıl tooconfigure uygulama toouse Facebook oturum açma]
* [Nasıl tooconfigure uygulama toouse Google oturum açma]
* [Nasıl tooconfigure uygulama toouse Microsoft Account oturum açma]
* [Nasıl tooconfigure uygulama toouse Twitter oturum açma]

Toouse kimlik sistemi dışında isterseniz burada da hello yararlanabilirsiniz sağlanan olanları hello [Önizleme hello .NET sunucusu SDK özel kimlik doğrulama desteği](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Kimlik doğrulama tooyour iOS uygulaması ekleyin]: app-service-mobile-ios-get-started-users.md
[Kimlik doğrulama tooyour Xamarin.iOS uygulaması ekleyin]: app-service-mobile-xamarin-ios-get-started-users.md
[Kimlik doğrulama tooyour Xamarin.Android uygulaması ekleyin]: app-service-mobile-xamarin-android-get-started-users.md
[Kimlik doğrulaması tooyour Windows uygulaması Ekle]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Nasıl tooconfigure uygulama toouse Azure Active Directory oturum açma]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Nasıl tooconfigure uygulama toouse Facebook oturum açma]: app-service-mobile-how-to-configure-facebook-authentication.md
[Nasıl tooconfigure uygulama toouse Google oturum açma]: app-service-mobile-how-to-configure-google-authentication.md
[Nasıl tooconfigure uygulama toouse Microsoft Account oturum açma]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Nasıl tooconfigure uygulama toouse Twitter oturum açma]: app-service-mobile-how-to-configure-twitter-authentication.md
