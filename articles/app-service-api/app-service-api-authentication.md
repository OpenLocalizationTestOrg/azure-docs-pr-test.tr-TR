---
title: "aaaAuthentication ve Azure uygulama hizmetinde API uygulamaları için yetkilendirme | Microsoft Docs"
description: "Azure App Service API uygulamaları için sağladığı hello kimlik doğrulama ve yetkilendirme hizmetleri hakkında bilgi edinin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Kimlik doğrulama ve yetkilendirme Azure uygulama hizmetinde API uygulamaları için
## <a name="overview"></a>Genel Bakış
> [!NOTE]
> Bu konu geçirilen tooa birleştirilmiş olacaktır [App Service kimlik doğrulama / yetkilendirme](../app-service/app-service-authentication-overview.md) Web, mobil ve API Apps kapsayan konu.
> 
> 

Azure uygulama hizmeti sunar yerleşik kimlik doğrulama ve yetkilendirme hizmetleri uygulayan [OAuth 2.0](#oauth) ve [Openıd Connect](#oauth). Bu makalede hello Hizmetleri ve Azure uygulama hizmetinde API uygulamaları için kullanılabilir seçenekler açıklanmaktadır.

Aşağıdaki diyagramda hello App Service kimlik doğrulama anahtarı bazı özellikleri gösterilmektedir:

* Herhangi bir dil veya App Service tarafından desteklenen framework birlikte çalıştığı anlamına gelen API istekleri preprocesses.
* Bu, ne kadar kimlik doğrulaması çalışmak için çeşitli seçenekler istediğiniz toodo kendi kodunuzu sağlar.
* Son kullanıcı ve hizmet hesabı kimlik doğrulaması için çalışır. 
* Beş kimlik sağlayıcılarını destekler: Azure Active Directory, Facebook, Google, Twitter ve Microsoft Account.
* Bu works Merhaba, aynı, API uygulamaları, Web uygulamaları ve mobil uygulamalar için.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Dil belirsiz
App Service kimlik doğrulama işleme istekleri hello kimlik doğrulama özelliklerini çalıştığını herhangi bir dil veya framework ile yazılmış API uygulamaları için anlamına gelir, API uygulamanızın düşmeden önce gerçekleşir.  API'nizi, ASP.NET, Java, Node.js veya uygulama hizmetini destekleyen framework dayanabilir.

Uygulama hizmeti hello HTTP isteğinin yetkilendirme üst bilgisinde hello JSON web token (JWT) aktarır ve herhangi bir dil veya framework yazılan kod, gereken hello bilgileri hello belirteç alabilir. Ayrıca, uygulama hizmeti daha kolay en yaygın olarak kullanılan toohello talep hello aşağıdaki gibi bazı özel üstbilgileri ayarlayarak erişmenizi:

* X-MS-İSTEMCİ-ASIL ADI
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Merhaba kullanabileceğiniz bir .NET API `Authorize` özniteliği ve kolayca yazabilirsiniz hassas yetkilendirme için kod dayanarak talepleri talep bilgileri sizin için .NET sınıflarda doldurulduğundan.

## <a name="multiple-protection-options"></a>Birden çok koruma seçenekleri
Uygulama hizmeti API uygulamanızı ulaşmasını anonim HTTP isteklerini engelleyebilirsiniz, tüm isteklerinde geçirin ve bunları içeren isteklerin belirteçleri doğrulamak veya tüm istekleri herhangi bir eylem üzerlerinde bırakmadan sağlayabilirsiniz:

1. Yalnızca kimliği doğrulanmış istekler tooreach API uygulamanızı sağlar.
   
    Anonim İstek tarayıcıdan aldıysanız, uygulama hizmeti hello kimlik doğrulama sağlayıcısı için tooa oturum açma sayfasına yönlendirir (Azure AD, Google, Twitter, vb.), seçtiğiniz. 
   
    Bu seçenek, toowrite tüm kimlik doğrulama kodu hiç uygulamanızda gerekmeyen ve hello en önemli talep hello HTTP üstbilgilerinde sağlandığından yetkilendirme kodu basitleştirilmiştir.
2. API uygulamanız tüm istekleri tooreach izin ancak kimliği doğrulanmış istekler doğrulamak ve kimlik doğrulama bilgilerini hello HTTP üstbilgisinde geçirirsiniz.
   
    Bu seçenek anonim istekler işleme daha fazla esneklik sağlar, ancak tooprevent anonim kullanıcıların API'nizi kullanmasını istiyorsanız toowrite koda sahip. Merhaba en popüler talep HTTP isteklerini hello üstbilgilerinde geçirilir olduğundan, yetkilendirme kodu oldukça basittir.
3. Hiçbir eylemde hello isteklerinde kimlik bilgileri, tüm istekleri tooreach API'nizi olanak sağlar.
   
    Bu seçenek, kimlik doğrulama ve yetkilendirme tamamen tooyour uygulama kodu yukarı hello görevlerin bırakır.

Merhaba, [Azure portal](https://portal.azure.com/), hello seçeneğini hello üzerinde istediğiniz **kimlik doğrulama / yetkilendirme** dikey.

![](./media/app-service-api-authentication/authblade.png)

1 ve 2 seçenekleri için Aç **App Service kimlik doğrulaması**ve hello **istek kimliği doğrulanmamış olduğunda eylem tootake** aşağı açılan listesinde seçin **oturum** veya **İsteğine izin ver (hiçbir işlem)**.  Seçerseniz **oturum**, toochoose bir kimlik doğrulama sağlayıcısına sahip ve bu sağlayıcıyı yapılandırın.

![](./media/app-service-api-authentication/actiontotake.png)

Hakkında ayrıntılı bilgi için tooconfigure kimlik doğrulaması, bkz: [nasıl tooconfigure App Service uygulama toouse Azure Active Directory oturum açma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Merhaba makale tooAPI uygulamalar gibi mobil uygulamaları için geçerlidir ve diğer kimlik doğrulama sağlayıcıları tooother makaleler hello için bağlar.

## <a id="internal"></a>Hizmet hesabı kimlik doğrulaması
Uygulama hizmeti kimlik doğrulama gibi iç senaryoları bir API uygulaması tooanother API uygulaması'ndan arama için çalışır. Bu senaryoda, son kullanıcı kimlik bilgilerini yerine bir hizmet hesabı için kimlik bilgilerini kullanarak, bir belirteç alırsınız. Bir hizmet hesabı olarak da bilinen olan bir *hizmet sorumlusu* Azure Active Directory ve kimlik doğrulaması kullanarak bu tür bir hesabınız olarak da bilinen bir hizmet senaryodur. 

Hizmetten hizmete senaryoları için Azure Active Directory kullanarak API uygulaması adında hello koruyun ve hello API uygulamasını çağırmayı gerektiğinde bir AAD hizmet sorumlusu yetkilendirme belirteci sağlamak. Belirteç hello istemci Kimliğini ve istemci hello AAD uygulaması ' gizli sağlayarak alın. Özel yalnızca Azure Kod hello Mobile Services Zumo belirteci işlemek için kullanılan toobe true gibi gerekli değildir. ASP.NET API apps kullanarak bu senaryoyu örneği hello öğretici kapsamında [API uygulamaları için hizmet asıl kimlik doğrulaması](app-service-api-dotnet-service-principal-auth.md).

Uygulama hizmeti kimlik doğrulama kullanmadan toohandle hizmet senaryo istiyorsanız, istemci sertifikalarını veya temel kimlik doğrulaması kullanabilirsiniz. Azure istemci sertifikaları hakkında daha fazla bilgi için bkz: [nasıl tooConfigure TLS karşılıklı kimlik doğrulaması Web uygulamaları için](../app-service-web/app-service-web-configure-tls-mutual-auth.md). ASP.NET, temel kimlik doğrulaması hakkında daha fazla bilgi için bkz: [ASP.NET Web API 2 kimlik doğrulaması filtrelerini](http://www.asp.net/web-api/overview/security/authentication-filters).

Hizmet hesabı kimlik doğrulamasını bir App Service logic app tooan API uygulaması içinde açıklanan özel bir durum olduğu [Logic apps ile App Service üzerinde barındırılan özel API'nizi kullanma](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Mobil istemci kimlik doğrulaması
Hakkında bilgi için bkz: Merhaba toohandle kimlik doğrulaması mobil istemcilerden [mobil uygulamaları için kimlik doğrulama belgelerine](../app-service-mobile/app-service-mobile-ios-get-started-users.md). App Service kimlik doğrulaması çalışır hello mobil uygulamaları ve API apps ile aynı şekilde.

## <a name="more-information"></a>Daha fazla bilgi
Kimlik doğrulama ve yetkilendirme Azure App Service hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Genişleyen App Service kimlik doğrulama / yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Nasıl tooconfigure App Service uygulama toouse Azure Active Directory oturum açma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (içeren bağlantılar hello sayfanın üst kısmındaki hello diğer kimlik doğrulama sağlayıcıları için.) 

OAuth 2.0, Openıd Connect ve JSON Web belirteçleri (JWT) hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.

* [OAuth 2.0 ile çalışmaya başlama](http://shop.oreilly.com/product/0636920021810.do "OAuth 2.0 ile çalışmaya başlama") 
* [Giriş tooOAuth2, Openıd Connect ve Pluralsight indirmelere (JWT) - JSON Web belirteçleri](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Derleme ve ASP.NET - Pluralsight indirmelere birden çok istemci RESTful API'si güvenliğini sağlama](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Azure Active Directory hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.

* [Azure AD senaryoları](http://aka.ms/aadscenarios)
* [Azure AD Geliştirici Kılavuzu](http://aka.ms/aaddev)
* [Azure AD örnekleri](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, API uygulamaları için kullanabileceğiniz bir App Service kimlik doğrulama ve yetkilendirme özelliklerini açıklandığı. Merhaba alınırken hello sonraki Öğreticisi seri gösterir nasıl tooimplement [App Service API Apps kullanıcı kimlik doğrulaması](app-service-api-dotnet-user-principal-auth.md).

