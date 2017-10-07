---
title: "aaaAzure Active Directory kod örnekleri | Microsoft Docs"
description: "Azure Active Directory kod örnekleri, senaryo tarafından düzenlenen bir dizini."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Azure Active Directory kod örnekleri
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Microsoft Azure Active Directory (Azure AD) tooadd kimlik doğrulama ve yetkilendirme tooyour web uygulamaları ve web API'leri kullanabilirsiniz. Bu bölümde, nasıl yapıldığını göster toosamples ve uygulamalarınızda kullanabileceğiniz kod parçacıkları bağlar. Ayrıntılı okuma Bul Hello kod örnek sayfada-bana gereksinimleri, yükleme ve Kurulum Yardım konuları. Ve hello kritik bölümler anlamak açıklamalı toohelp hello kodudur.

Her bir örnek türü için toounderstand hello temel senaryo için Azure AD kimlik doğrulama senaryoları bakın.

Github'da tooour örnekleri katkıda: [Microsoft Azure Active Directory örnekler ve belgeler](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>Web tarayıcısı tooWeb uygulama
Bu örnekler nasıl toowrite yönlendiren bir web uygulaması hello kullanıcının tarayıcı toosign Göster tooAzure AD bunları.

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| C# / .NET |[WebApp Openıdconnect DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Azure AD kiracısı tooauthenticate kullanıcıların Openıd Connect (ASP.Net Openıd Connect OWIN ara yazılımı) kullanın. |
| C# / .NET |[Çok kullanıcılı Openıdconnect DotNet WebApp](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Tooauthenticate kullanıcılardan Openıd Connect (ASP.Net Openıd Connect OWIN ara yazılımı) birden çok Azure AD kiracılarıyla kullanan bir çok kiracılı .NET MVC web uygulaması. |
| C# / .NET |[WebApp WSFederation DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |WS-Federasyon (ASP.Net WS-Federasyon OWIN ara yazılımı) tooauthenticate kullanıcıların Azure AD kiracısı kullanın. |

## <a name="single-page-application-spa"></a>Tek sayfalı uygulama (SPA)
Bu örnek toowrite bir tek sayfa uygulaması Azure AD ile güvenliği nasıl gösterir.  

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| JavaScript, C# / .NET |[SinglePageApp DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Bir ASP.NET web API'si arka uç ile uygulanan JavaScript ve Azure AD toosecure AngularJS tabanlı tek sayfa uygulaması için ADAL kullanır. |

## <a name="native-application-tooweb-api"></a>Yerel uygulama tooWeb API
Bu kod örnekleri, web API çağırma toobuild yerel istemci uygulamaları Azure AD tarafından güvenliği nasıl gösterir. Kullandıkları [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) ve [OAuth 2.0 Azure AD'de](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| Javascript |[NativeClient MultiTarget Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Apache Cordova toobuild web API'si çağıran ve Azure AD kimlik doğrulaması için kullandığı bir Apache Cordova uygulaması için Hello ADAL eklentisini kullanın. |
| C# / .NET |[NativeClient DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Azure AD kullanarak bir web API'si çağıran bir .NET WPF uygulaması korunmaktadır. |
| C# / .NET |[NativeClient WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Web API'si çağıran bir Windows mağazası uygulaması, Azure AD ile güvenli hale getirilir. |
| C# / .NET |[Webapı çok kullanıcılı WindowsStore NativeClient](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Çok kiracılı web Azure AD ile güvenli hale getirilen API'si çağrılırken bir Windows mağazası uygulaması. |
| C# / .NET |[Webapı OnBehalfOf DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Merhaba özgün kullanıcı adına bir belirteç tooact alır ve ardından kullanan bir web API'si çağıran bir yerel istemci uygulaması, başka bir web API belirteci toocall hello. |
| C# / .NET |[NativeClient WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Web API'si çağıran bir Windows Phone 8.1 için Windows mağazası uygulaması, Azure AD tarafından korunmaktadır. |
| ObjC |[NativeClient iOS](https://github.com/Azure-Samples/active-directory-ios) |Web API'si çağıran bir iOS uygulamasına Azure AD için kimlik doğrulaması gerektirir. |
| C# / .NET |[Webapı ManuallyValidateJwt DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |OWIN ara yazılımı kullanmak yerine bir web API, mantığı tooprocess bir JWT belirteci içeren yerel istemci uygulaması. |
| C# / Xamarin |[NativeClient Xamarin Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |İçin kimlik doğrulama kitaplığı (ADAL) toohello yerel Azure AD bağlama bir Xamarin Android kitaplığı hello. |
| C# / Xamarin |[NativeClient Xamarin iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Xamarin bağlama toohello yerel Azure AD Authentication Library (ADAL) iOS için. |
| C# / Xamarin |[NativeClient MultiTarget DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Beş platformları hedefler ve web API'si çağıran bir Xamarin projeyi Azure AD tarafından korunmaktadır. |
| C# / .NET |[NativeClient gözetimsiz-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Etkileşimli olmayan kimlik doğrulaması gerçekleştiren ve bir web API'si çağıran bir yerel uygulamayı Azure AD tarafından korunmaktadır. |

## <a name="web-application-tooweb-api"></a>Web uygulama tooWeb API
Bu kod örnekleri Göster kullanma [OAuth 2.0 Azure AD'de](https://msdn.microsoft.com/library/azure/dn645545.aspx) web API çağırma toobuild web uygulamaları Azure AD tarafından güvenli.

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| C# / .NET |[WebApp Webapı Openıdconnect DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Merhaba oturum açmış kullanıcının izinleriyle web API'si çağırma. |
| C# / .NET |[WebApp-Webapı-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Merhaba uygulamanın izinlerle web API'si çağırma. |
| C# / .NET |[WebApp-Webapı-OAuth2-Userıdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Yetkilendirme ile ekleme [OAuth 2.0 Azure AD'de](https://msdn.microsoft.com/library/azure/dn645545.aspx) web API'si çağırabilirsiniz şekilde tooan varolan web uygulaması. |
| JavaScript |[Webapı Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |API koruma için Azure AD ile tümleşik bir REST API hizmeti ayarlayın. Bir Web API ile bir Node.js sunucusu içerir. |
| C# / .NET |[WebApp-Webapı-çok kullanıcılı-Openıdconnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Çok kiracılı MVC web tooauthenticate kullanıcılardan Openıd Connect (ASP.Net Openıd Connect OWIN ara yazılımı) Azure AD kiracısı kullanan uygulama. Bir yetkilendirme kodu tooinvoke hello grafik API'sini kullanır. |

## <a name="server-or-daemon-application-tooweb-api"></a>Sunucu veya arka plan programı uygulama tooWeb API
Bu kod örnekleri nasıl toobuild bir arka plan programı veya sunucu uygulaması, kaynakları bir web API kullanarak alır Göster [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) ve [OAuth 2.0 Azure AD'de](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| C# / .NET |[Arka plan programı DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Bir konsol uygulaması web API'si çağırır. Merhaba istemci kimlik bilgileri bir parola değil. |
| C# / .NET |[Arka plan programı CertificateCredential DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Web API'si çağıran bir konsol uygulaması. Merhaba istemci kimlik bilgileri bir sertifikadır. |

## <a name="calling-azure-ad-graph-api"></a>Azure AD grafik API'si çağırma
Bu kod örneği Göster çağrı toobuild uygulamaları Azure AD Graph API tooread ve yazma dizin verilerini nasıl hello.

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| Java |[WebApp GraphAPI Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Merhaba grafik API'si tooaccess Azure AD directory veri kullanan bir web uygulaması. |
| PHP |[WebApp GraphAPI PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Merhaba grafik API'si tooaccess Azure AD directory veri kullanan bir web uygulaması. |
| C# / .NET |[WebApp GraphAPI DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Merhaba grafik API'si tooaccess Azure AD directory veri kullanan bir web uygulaması. |
| C# / .NET |[ConsoleApp GraphAPI DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Bu konsol uygulamasını ortak okuma ve yazma çağrıları toohello grafik API'si gösterir ve nasıl tooexecute kullanıcı lisansı atama ve kullanıcının küçük resim fotoğrafı ve bağlantıları güncelleştirme gösterir. |
| C# / .NET |[GraphAPI DiffQuery DotNet ConsoleApp](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Merhaba grafik API'si tooget içinde düzenli hello fark sorgusu kullanan bir konsol uygulaması Azure AD kiracısı toouser nesneleri değiştirir. |
| C# / .NET |[WebApp GraphAPI DirectoryExtensions DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Bir MVC uygulaması grafik API'si sorguları toogenerate basit şirket kuruluş şeması kullanır. |
| PHP |[WebApp GraphAPI DirectoryExtensions PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Uzantı hello grafik API'si tooregister çağırır ve ardından okuma, güncelleştirme ve hello uzantısı öznitelik değerlerini silin PHP uygulaması. |

## <a name="authorization"></a>Yetkilendirme
Bu kod örnekleri Göster nasıl toouse yetkilendirme için Azure AD.

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| C# / .NET |[WebApp GroupClaims DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Rol tabanlı erişim denetimi (RBAC) Azure AD ile tümleşik bir uygulamada Azure Active Directory grup talepleri kullanarak gerçekleştirin. |
| C# / .NET |[WebApp RoleClaims DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Azure Active Directory uygulama rolleri Azure AD ile tümleşik bir uygulama kullanarak rol tabanlı erişim denetimi (RBAC) gerçekleştirin. |

## <a name="legacy-walkthroughs"></a>Eski izlenecek yollar
Bu izlenecek yollar biraz daha eski teknolojiyi kullanır, ancak yine de ilgi olabilir.

| Dil/Platform | Örnek | Açıklama |
| --- | --- | --- |
| C# / .NET |[Microsoft Azure AD uygulama rolü ve ACL tabanlı yetkilendirme](http://go.microsoft.com/fwlink/?LinkId=331694) |Rol tabanlı yetkilendirme (RBAC) ve ACL tabanlı bir yetkilendirme Azure AD ile tümleşik bir uygulamada gerçekleştirin. |
| C# / .NET |[AAL - Windows mağazası uygulama tooREST hizmeti - kimlik doğrulama](http://go.microsoft.com/fwlink/?LinkId=330605) |Kullanım [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) (önceki adıyla AAL) için Windows mağazası Beta tooadd kullanıcı kimlik doğrulaması özellikleri tooa Windows mağazası uygulaması. |
| C# / .NET |[Tarayıcı iletişim kutusu üzerinden aad'ye - yerel uygulama tooREST service - ADAL kimlik doğrulaması](http://go.microsoft.com/fwlink/?LinkId=259814) |Kullanım [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) tooadd kullanıcı kimlik doğrulaması özellikleri tooa WPF istemci. |
| C# / .NET |[Tarayıcı iletişim kutusu üzerinden ACS ile - yerel uygulama tooREST service - ADAL kimlik doğrulaması](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Kullanım [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) ve [erişim denetimi hizmeti 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) tooadd kullanıcı kimlik doğrulaması özellikleri tooa WPF istemci. |
| C# / .NET |[ADAL - Server tooServer kimlik doğrulaması](http://go.microsoft.com/fwlink/?LinkId=259816) |Kullanım [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) bir sunucu tarafı işlem tooan MVC4 Web API REST hizmeti gelen toosecure hizmeti çağrıları. |
| C# / .NET |[Oturum açma Web uygulaması kullanarak Azure tooYour ekleme AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Bir .NET uygulama tooperform web çoklu oturum açma Azure AD kuruluş dizininizin karşı yapılandırın. |
| C# / .NET |[Azure AD ile çok Kiracılı Web uygulamaları geliştirme](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Azure AD tooadd toohello çoklu oturum açma ve dizin erişim yetenekleri bir .NET uygulama toowork birden çok kuruluşta kullanın. |
| JAVA |[Azure AD grafik API'si için Java örnek uygulama](http://go.microsoft.com/fwlink/?LinkId=263969) |Merhaba grafik API'si tooaccess dizin verilerini Azure AD'den kullanın. |
| PHP |[Azure AD grafik API'si için PHP örnek uygulama](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Merhaba grafik API'si tooaccess dizin verilerini Azure AD'den kullanın. |
| C# / .NET |[Azure AD Graph API için örnek uygulama](http://go.microsoft.com/fwlink/?LinkID=262648) |Merhaba grafik API'si tooaccess dizin verilerini Azure AD'den kullanın. |
| C# / .NET |[Azure AD Graph fark sorgu için örnek uygulama](http://go.microsoft.com/fwlink/?LinkId=275398) |Azure AD kiracısı hello grafik API'si tooget düzenli değişiklikleri toouser nesneleri Hello fark sorgu kullanın. |
| C# / .NET |[Azure AD için çok Kiracılı bulut uygulaması tümleştirmek için örnek uygulama](http://go.microsoft.com/fwlink/?LinkId=275397) |Çok kiracılı uygulama Azure AD ile tümleştirin. |
| C# / .NET |[Bir Windows mağazası uygulaması ve Azure AD kullanarak REST Web hizmeti güvenli hale getirme](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Basit bir web API kaynak ve Azure AD kullanarak bir Windows mağazası istemci uygulaması oluşturabilir ve hello [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md). |
| C# / .NET |[Merhaba grafik API'si tooQuery Azure AD kullanma](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Microsoft .NET uygulama toouse hello Azure AD Graph API tooaccess verileri Azure AD Kiracı dizini yapılandırın. |

## <a name="see-also"></a>Ayrıca bkz.
##### <a name="other-resources"></a>Diğer Kaynaklar
[Azure Active Directory Geliştirici Kılavuzu](active-directory-developers-guide.md)

[Azure AD Graph API kavramsal ve başvurusu](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Azure AD Graph API Yardımcısı kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
