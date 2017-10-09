---
title: aaaAuthentication ve Azure App Service'te yetkilendirme | Microsoft Docs
description: "Kavramsal başvurusu ve genel bakış hello kimlik doğrulama / yetkilendirme özelliğini Azure uygulama hizmeti"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde kimlik doğrulaması ve yetkilendirme
## <a name="what-is-app-service-authentication--authorization"></a>App Service kimlik doğrulaması nedir / yetkilendirme?
App Service kimlik doğrulama / yetkilendirme, uygulama toosign kullanıcılar için bir yol sağlar ve böylece hello uygulama arka uçta toochange koduna sahip değilseniz bir özelliktir. Bir kolay bir yolu tooprotect, uygulama ve iş ile kullanıcı başına veri sağlar.

Uygulama hizmeti bir üçüncü taraf kimlik sağlayıcısı hesapları depolar ve kullanıcıların kimliğini doğrulayan Federal Kimlik kullanır. Böylece Hello uygulama toostore bu bilgileri yok Merhaba uygulaması üzerinde hello sağlayıcının kimlik bilgilerini kullanır. Uygulama hizmeti hello kutusu dışında beş kimlik sağlayıcılarını destekler: Azure Active Directory, Facebook, Google, Microsoft Account ve Twitter. Uygulamanız bu kimlik sağlayıcıları tooprovide herhangi bir sayıda kullanıcılarınızın seçenekleri ile nasıl oturum için kullanabilirsiniz. tooexpand hello yerleşik destek, başka bir kimlik sağlayıcısı tümleştirebilir veya [kendi özel kimlik çözümü][custom-auth].

Hemen kullanmaya tooget istiyorsanız, aşağıdaki öğreticiler hello birine bakın:

* [Kimlik doğrulama tooyour iOS uygulaması eklemek] [ iOS] (veya [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [Xamarin.Forms], veya [Cordova])
* [Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması][apia-user]
* [Azure App Service - bölüm 2 ile çalışmaya başlama][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Kimlik doğrulaması App Service içinde nasıl çalışır
Merhaba kimlik sağlayıcılardan birini kullanarak sipariş tooauthenticate içinde önce uygulamanız hakkında tooconfigure hello kimlik sağlayıcısı tooknow gerekir. Hello kimlik sağlayıcısı sonra kimliklerini ve parolaları tooApp hizmet sağlamak sağlar. Uygulama hizmeti hello kimlik sağlayıcısından gelen kimlik doğrulama belirteçleri gibi kullanıcı onaylar doğrulayabilmesi bu hello güven ilişkisi tamamlar.

toosign bu sağlayıcıları birini kullanarak bir kullanıcı hello kullanıcı kullanıcılar oturum açtığında bu sağlayıcı için yeniden yönlendirilen tooan uç noktası olmalıdır. Müşterilerin bir web tarayıcısı kullanıyorsanız, uygulama hizmeti otomatik olarak kullanıcılar oturum açtığında tüm kimliği doğrulanmamış kullanıcıların toohello endpoint doğrudan olabilir. Aksi takdirde, toodirect müşterilerinize çok gerekir`{your App Service base URL}/.auth/login/<provider>`, burada `<provider>` değerleri aşağıdaki hello biridir: aad, facebook, google, microsoft ya da twitter. Mobil ve API senaryoları bölümlerde bu makalenin sonraki bölümlerinde açıklanmıştır.

Uygulamanızı bir web tarayıcısı aracılığıyla etkileşim kullanıcılar ayarlayabilir, böylece uygulamanız gezinirken bunlar kimliği doğrulanmış kalabileceği bir tanımlama bilgisi gerekir. Mobile, JSON web token (JWT) gibi diğer istemci türlerini için hangi sunulması gerektiğini hello `X-ZUMO-AUTH` başlık toohello istemci verilir. Merhaba Mobile Apps istemci SDK'ları bu sizin için işler. Alternatif olarak, bir Azure Active Directory kimlik belirtecinin ya da erişim belirteci doğrudan hello eklenebilir `Authorization` üstbilgisi olarak bir [taşıyıcı belirteci](https://tools.ietf.org/html/rfc6750).

Uygulama hizmeti herhangi bir tanımlama bilgisi veya uygulamanızın tooauthenticate kullanıcılar sorunları belirteci doğrular. uygulamanızın, kimlerin erişebileceğini toorestrict hello bkz [yetkilendirme](#authorization) bu makalenin sonraki bölümlerinde bölümü.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Mobil kimlik doğrulama sağlayıcısı SDK ile
Her şeyi hello arka uçta yapılandırıldıktan sonra uygulama hizmeti oturum mobil istemcilerin toosign değiştirebilirsiniz. Burada iki yaklaşım vardır:

* Belirtilen kimlik sağlayıcısı tooestablish kimlik yayımlayan bir SDK'yı kullanın ve erişim tooApp hizmet geçirmesine.
* Tek satırlık bir kod kullandığından, bu hello Mobile Apps istemci SDK kullanıcılar oturum açabilirsiniz.

> [!TIP]
> Çoğu uygulamayı sağlayıcısı SDK tooget kullanıcılar oturum açtığında daha tutarlı bir deneyim, toouse yenileme desteği ve tooget kullanması gereken diğer avantajlar hello sağlayıcının belirtir.
> 
> 

Kullanıcılar oturum açabilir SDK, sağlayıcı kullandığınızda bu hello uygulama hello işletim sistemiyle daha sıkı bir şekilde tümleştirilir tooan deneyimi çalıştırılması. Bu ayrıca, bir sağlayıcı belirteci ve çok daha kolay tooconsume graph API kolaylaştırır ve hello kullanıcı deneyimini özelleştirme hello istemci üzerindeki bazı kullanıcı bilgileri sunar. Bazen bloglar ve forumlar, bu başvurulan tooas hello "istemci akışı" görürsünüz veya erişim tooa sağlayıcı belirteci "istemci yönlendirilmiş akış" sahip kullanıcıları ve hello istemci kodu hello istemci kodu imzalar olduğundan.

Bir sağlayıcı belirteci alındıktan sonra tooApp hizmet doğrulama için gönderilen toobe gerekir. Uygulama hizmeti hello belirteci doğruladıktan sonra uygulama hizmeti toohello istemci döndürülen yeni bir uygulama hizmeti belirteci oluşturur. Merhaba Mobile Apps istemci SDK bu exchange yardımcı yöntemler toomanage sahiptir ve otomatik olarak hello belirteci tooall istekleri toohello uygulama arka uç ekleyin. Bu nedenle seçerseniz geliştiriciler Ayrıca başvuru toohello sağlayıcı belirteci kullanmaya devam edebilir.

### <a name="mobile-authentication-without-a-provider-sdk"></a>SDK sağlayıcı olmadan Mobil kimlik doğrulaması
SDK sağlayıcı yukarı tooset istemiyorsanız, Azure App Service toosign hello Mobile Apps özelliğini izin verebilirsiniz. Merhaba Mobile Apps istemci SDK seçtiğiniz web görünümü toohello sağlayıcısı açın ve hello kullanıcı olarak oturum açın. Bazen bloglar ve forumlar, bu başvurulan tooas hello "sunucu akış" veya "sunucu yönlendirilmiş akış" Merhaba sunucusu kullanıcılar oturum açtığında hello sürecini yönetir ve hello istemci SDK hello sağlayıcı belirteci hiçbir zaman alır çünkü görürsünüz.

Bu akış hello kimlik doğrulaması öğretici her platform için yer aldığı toostart kodu. Sonunda hello hello akış, bir uygulama hizmeti belirteci hello istemci SDK'sı vardır ve otomatik olarak eklenen tooall istekleri toohello uygulama arka uç hello belirteç olur.

### <a name="service-to-service-authentication"></a>Hizmetten hizmete kimlik doğrulaması
Kullanıcıların erişimi tooyour uygulama vermesine karşın, ayrıca kendi API başka bir uygulama toocall güvenebilirsiniz. Örneğin, başka bir web uygulamasında bir API çağrısı bir web uygulaması olabilir. Bu senaryoda, kullanıcı kimlik bilgilerini tooget bir belirteç yerine bir hizmet hesabı kimlik bilgilerini kullanın. Bir hizmet hesabı olarak da bilinen olan bir *hizmet sorumlusu* Azure Active Directory dilinde ve kullandığı kimlik doğrulama bu tür bir hesabınız olarak da bilinen bir hizmet senaryodur.

> [!IMPORTANT]
> Mobil uygulamaları müşteri cihazlarda çalıştığından, mobil uygulamalar yapmak *değil* sayısı güvenilir uygulamalar ve hizmet asıl akış kullanmamanız gerekir. Bunun yerine, önceki ayrıntılı bir kullanıcı akışı kullanmanız gerekir.
> 
> 

Hizmetten hizmete senaryoları için uygulama hizmeti uygulamanızı Azure Active Directory kullanarak koruyabilirsiniz. Merhaba arama uygulaması yalnızca tooprovide hello istemci Kimliğini ve istemci Azure Active Directory'den gizli sağlayarak elde bir Azure Active Directory hizmet asıl yetkilendirme belirteci gerekir. ASP.NET API uygulamaları kullanan bu senaryo örneği hello Öğreticisi tarafından açıklanan [API uygulamaları için hizmet asıl kimlik doğrulaması][apia-service].

App Service kimlik doğrulama toohandle hizmet senaryo toouse istiyorsanız, istemci sertifikalarını veya temel kimlik doğrulaması kullanabilirsiniz. Azure istemci sertifikaları hakkında daha fazla bilgi için bkz: [nasıl tooConfigure TLS karşılıklı kimlik doğrulaması Web uygulamaları için](../app-service-web/app-service-web-configure-tls-mutual-auth.md). ASP.NET, temel kimlik doğrulaması hakkında daha fazla bilgi için bkz: [ASP.NET Web API 2 kimlik doğrulaması filtrelerini](http://www.asp.net/web-api/overview/security/authentication-filters).

Hizmet hesabı kimlik doğrulamasını bir App Service logic app tooan API uygulaması içinde ayrıntılı bir özel durum olan [Logic apps ile App Service üzerinde barındırılan özel API'nizi kullanma](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Yetkilendirme App Service içinde nasıl çalışır
Uygulamanızı erişebilirsiniz hello istekleri üzerinde tam denetime sahiptir. App Service kimlik doğrulama / yetkilendirme herhangi davranışları aşağıdaki hello yapılandırılabilir:

* Yalnızca kimliği doğrulanmış istekler tooreach uygulamanızı sağlar.
  
    Bir tarayıcı adsız bir istek alırsa, uygulama hizmeti tooa sayfasında seçtiğiniz ve böylece kullanıcılar oturum açabilir hello kimlik sağlayıcısı için yönlendirir. Merhaba isteği bir mobil CİHAZDAN geliyorsa, hello yanıt bir HTTP döndürülür *401 Yetkisiz* yanıt.
  
    Bu seçenek ile toowrite tüm kimlik doğrulama kodu hiç uygulamanız gerekmez. Hassas yetkilendirme gerekiyorsa, hello kullanıcı hakkındaki bilgileri kullanılabilir tooyour kodudur.
* Uygulamanız, tüm istekleri tooreach izin ancak kimliği doğrulanmış istekler doğrulamak ve kimlik doğrulama bilgilerini hello HTTP üstbilgisinde geçirirsiniz.
  
    Bu seçenek, yetkilendirme kararları tooyour uygulama kodu erteler. Anonim istekler işleme daha fazla esneklik sağlar, ancak toowrite koda sahip.
* Uygulamanız tüm istekleri tooreach izin ve hiçbir eylemde hello isteklerinde kimlik doğrulama bilgileri.
  
    Bu durumda, kimlik doğrulama hello / yetkilendirme özelliğini kapalıdır. Merhaba, kimlik doğrulama ve yetkilendirme tamamen tooyour uygulama kodu görevlerdir.

Merhaba önceki davranışları hello tarafından denetlenen **istek kimliği doğrulanmamış olduğunda eylem tootake** hello Azure portal seçeneği. Seçerseniz ** ile oturum *sağlayıcı adı* **, tüm istekleri kimlik doğrulaması toobe sahip. **İsteğin (hiçbir işlem) izin** hello yetkilendirme kararı tooyour kodu erteler ancak hala bir kimlik doğrulama bilgilerini sağlar. Toohave istiyorsanız kodunuzun her şeyi işlemek, hello kimlik doğrulaması devre dışı bırak / yetkilendirme özelliği.

## <a name="working-with-user-identities-in-your-application"></a>Kullanıcı kimlikleri, uygulamanızda ile çalışma
Uygulama hizmeti özel üstbilgileri kullanarak bazı kullanıcı bilgileri tooyour uygulaması geçirir. Dış istekleri engelle Bu üstbilgileri ve mevcut ise yalnızca ayarlanacak tarafından App Service kimlik doğrulama / yetkilendirme. Bazı örnek üst bilgiler içerir:

* X-MS-İSTEMCİ-ASIL ADI
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Tüm dil veya framework ile yazılan kod, gereken hello bilgileri bu üstbilgileri elde edebilirsiniz. ASP.NET 4.6 uygulamaları için hello **ClaimsPrincipal** hello uygun değerlerle otomatik olarak ayarlanır.

Uygulamanızı bir HTTP GET hello üzerinde aracılığıyla ek kullanıcı ayrıntıları edinebilirsiniz `/.auth/me` uygulamanızın uç noktası. Merhaba istekle eklemiştir geçerli bir belirteci kullanılıyor hello sağlayıcısı ilişkin ayrıntıları içeren bir JSON yükü dönün, temel alınan sağlayıcı belirteci ve başka bir kullanıcı bilgileri hello. Merhaba mobil uygulamalar sunucusu SDK'ları sağlamak yardımcı yöntemler bu verilerle toowork. Daha fazla bilgi için bkz: [nasıl toouse hello Azure Mobile Apps Node.js SDK'sı](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), ve [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Belgeleri ve ek kaynaklar
### <a name="identity-providers"></a>Kimlik sağlayıcılar
öğreticiler Göster nasıl aşağıdaki hello tooconfigure uygulama hizmeti toouse farklı kimlik doğrulama sağlayıcıları:

* [Nasıl tooconfigure uygulama toouse Azure Active Directory oturum açma][AAD]
* [Nasıl tooconfigure uygulama toouse Facebook oturum açma][Facebook]
* [Nasıl tooconfigure uygulama toouse Google oturum açma][Google]
* [Nasıl tooconfigure uygulama toouse Microsoft Account oturum açma][MSA]
* [Nasıl tooconfigure uygulama toouse Twitter oturum açma][Twitter]

Toouse kimlik sistemi dışında isterseniz burada da hello kullanabilirsiniz sağlanan olanları hello [Önizleme hello Mobile Apps .NET sunucusu SDK özel kimlik doğrulama desteği][custom-auth], web uygulamalarında kullanılabilir mobil uygulamalar, veya API uygulamaları.

### <a name="web-applications"></a>Web uygulamaları
Eğitim aşağıdaki hello nasıl tooadd kimlik doğrulaması tooa web uygulaması göster:

* [Azure App Service - bölüm 2 ile çalışmaya başlama][web-getstarted]

### <a name="mobile-applications"></a>Mobil uygulamalar
öğreticiler aşağıdaki hello kullanarak tooadd kimlik doğrulaması tooyour mobil istemcilerin sunucu yönlendirilmiş akışı nasıl hello göster:

* [Kimlik doğrulama tooyour iOS uygulaması ekleyin][iOS]
* [Kimlik doğrulama tooyour Android uygulama Ekle][Android]
* [Kimlik doğrulaması tooyour Windows uygulaması Ekle][Windows]
* [Kimlik doğrulama tooyour Xamarin.iOS uygulaması eklemek][Xamarin.iOS]
* [Kimlik doğrulama tooyour Xamarin.Android uygulaması eklemek][ Xamarin.Android]
* [Kimlik doğrulama tooyour Xamarin.Forms uygulaması eklemek][Xamarin.Forms]
* [Kimlik doğrulama tooyour Cordova uygulaması eklemek][Cordova]

Hello Azure Active Directory için toouse hello istemci yönlendirilmiş akışı istiyorsanız aşağıdaki kaynakları kullanın:

* [İOS için Hello Active Directory kimlik doğrulama kitaplığı kullanma][ADAL-iOS]
* [Android için Hello Active Directory kimlik doğrulama kitaplığı kullanma][ADAL-Android]
* [Merhaba Active Directory kimlik doğrulama kitaplığı Windows için ve Xamarin kullanın][ADAL-dotnet]

Facebook için toouse hello istemci yönlendirilmiş akışı istiyorsanız kaynakları aşağıdaki hello kullan:

* [İOS için Hello Facebook SDK'sını kullanın](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Hello Twitter için toouse hello istemci yönlendirilmiş akışı istiyorsanız aşağıdaki kaynakları kullanın:

* [İOS için twitter doku kullanma](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Google için toouse hello istemci yönlendirilmiş akışı istiyorsanız kaynakları aşağıdaki hello kullan:

* [İOS için Hello Google oturum açma SDK kullanın](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>API uygulamaları
öğreticiler Göster nasıl aşağıdaki hello tooprotect API uygulamalarınızı:

* [Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması][apia-user]
* [Azure uygulama hizmetinde API uygulamaları için hizmet asıl kimlik doğrulaması][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
