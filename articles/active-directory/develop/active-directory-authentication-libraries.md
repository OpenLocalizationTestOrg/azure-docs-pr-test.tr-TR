---
title: "Active Directory kimlik doğrulama kitaplıkları aaaAzure | Microsoft Docs"
description: "Hello Azure AD Authentication Library (ADAL) sağlayan istemci uygulaması geliştiricileri tooeasily kullanıcılar toocloud kimlik doğrulaması veya şirket içi Active Directory (AD) ve API çağrıları güvenliğini sağlamak için erişim belirteci alın."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Azure Active Directory kimlik doğrulama kitaplıkları
Hello Azure Active Directory Authentication Library (ADAL) etkinleştirir istemci uygulaması geliştiricileri tooeasily kullanıcılar toocloud kimlik doğrulaması veya şirket içi Active Directory (AD) ve API çağrıları güvenliğini sağlamak için erişim belirteci alın. ADAL kimlik doğrulaması özellikler sayesinde geliştiriciler için gibi kolaylaştırır:
 - zaman uyumsuz yöntem çağrıları için destek
 - depoları belirteçleri erişmek ve yenileme belirteçlerini yapılandırılabilir bir belirteç önbelleği
 - bir erişim belirtecinin süresi ve yenileme belirteci kullanılabilir olduğunda otomatik belirteci yenileme
 - ve daha fazlası
 
Çoğu hello karmaşıklık işleme, ADAL iş mantığı geliştiriciler odaklanmanıza yardımcı olur ve kolayca kaynakları, Uzman güvenlik olmadan güvenli hale getirme.

ADAL çeşitli platformlarda kullanılabilir.

### <a name="client-libraries"></a>İstemci Kitaplıkları

| Platform | Kitaplık | İndir | Kaynak kodu | Örnek | Başvuru
| --- | --- | --- | --- | --- | --- |
| .NET istemci, Windows mağazası, UWP, Xamarin iOS ve Android |.NET (Önizleme) için MSAL |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Masaüstü uygulaması](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Başvuru](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL JavaScript (Önizleme) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Tek sayfa uygulaması](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Başvuru](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL iOS (Önizleme) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS uygulaması](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Başvuru](https://azuread.github.io/docs/objc/) |
| Android |MSAL Android (Önizleme) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android uygulaması](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Başvuru](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| .NET istemci, Windows mağazası, UWP, Xamarin iOS ve Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Masaüstü uygulaması](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Başvuru](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| .NET istemci, Windows mağazası, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Masaüstü uygulaması](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[Tek sayfa uygulaması](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[iOS uygulaması](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Başvuru](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Merhaba merkezi deposu](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Android uygulaması](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Java web uygulaması](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Sunucu kitaplıkları 

| Platform | Kitaplık | İndir | Kaynak kodu | Örnek | Başvuru
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN için AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[MVC uygulama](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN Openıdconnect için |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Web Uygulaması](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Web API](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |WS-Federasyon için OWIN |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[MVC Web uygulaması](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |.NET 4.5 kimlik Protokolü uzantıları |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |.NET 4.5 için JWT işleyicisi |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Senaryolar

ADAL içinde kullanılabilir uzaktaki bir kaynağa erişen istemci kimlik doğrulaması için üç yaygın senaryolar şunlardır:  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Aygıtta çalışan bir yerel istemci uygulaması, kullanıcıların kimlik doğrulaması 

Bu senaryoda, bir geliştirici tooaccess web API'si gibi Azure AD tarafından güvenli hale getirilmiş bir uzak kaynak gerektiren bir WPF istemci uygulaması sahiptir. Kendisi bir Azure aboneliğine sahip nasıl tooinvoke hello Aşağı Akış web API'si bilir ve hello Azure bilir web API'si kullanan hello AD Kiracı. Sonuç olarak, kendisinin ADAL toofacilitate kimlik doğrulaması Azure AD ile tam olarak hello kimlik doğrulama deneyimi tooADAL için temsilci seçme ya da kullanıcı kimlik bilgilerini açıkça işleme kullanabilirsiniz. ADAL kolay tooauthenticate hello kullanıcı kolaylaştırır, Azure AD'den bir erişim belirteci ve yenileme belirteci edinmek ve hello erişim belirteci toomake istekleri toohello web API'sini kullanın.

Kimlik doğrulama tooAzure AD kullanarak bu senaryoyu gösteren bir kod örneği için bkz: [yerel istemci WPF uygulaması tooWeb API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Bir web sunucusunda çalışan bir gizli istemci kimlik doğrulaması

Bu senaryoda, bir geliştirici web API'si gibi Azure AD tarafından güvenli hale getirilmiş bir uzak kaynak tooaccess gereken sunucu üzerinde çalışan bir uygulama sahiptir. Kendisi bir Azure aboneliğine sahip, nasıl tooinvoke hello aşağı akış hizmeti bilir ve hello Azure AD Kiracı hello web API'si kullanan bilir. Sonuç olarak, kendisine açıkça hello uygulamanın kimlik bilgileri işleyerek Azure AD ile ADAL toofacilitate kimlik doğrulaması kullanabilirsiniz. ADAL hello uygulamanın istemci kimlik bilgileri kullanılarak kolay tooretrieve Azure AD'den bir belirteç yapar ve sonra bu belirteci toomake istekleri toohello web API kullanın. ADAL de hello hello ömrü yönetme tanıtıcıları belirteci, önbelleğe alma ve gerektiği gibi yenileme erişebilirsiniz. Bu senaryo gösteren bir kod örneği için bkz: [arka plan programı konsol uygulaması tooWeb API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Bir kullanıcı adına bir sunucu üzerinde çalışan bir gizli istemci kimlik doğrulaması 

Bu senaryoda, bir geliştirici web API'si gibi Azure AD tarafından güvenli hale getirilmiş bir uzak kaynak tooaccess gereken sunucu üzerinde çalışan bir uygulama sahiptir. Merhaba isteği ayrıca bir Azure AD kullanıcı adına yapılan toobe gerekir. Kendisi bir Azure aboneliğine sahip, nasıl tooinvoke hello Aşağı Akış web API'si bilir ve hello Azure AD Kiracı hello hizmeti kullanan bilir. Merhaba kullanıcı kimliği doğrulanmış toohello web uygulaması eklendiğinde, Merhaba uygulaması Azure AD'den hello kullanıcı için bir yetkilendirme kodu alabilirsiniz. Merhaba web uygulaması, daha sonra bir erişim belirteci ve yenileme belirteci Azure AD'den hello uygulamayla ilişkili hello yetkilendirme kodu ve istemci kimlik bilgilerini kullanarak bir kullanıcı adına ADAL tooobtain kullanabilirsiniz. Merhaba web uygulaması hello erişim belirteci elinde eklendiğinde, hello belirteç süresi doluncaya kadar hello web API'si çağırabilirsiniz. Merhaba belirtecinin süresi dolduğunda, hello web uygulamasını daha önce alındı hello yenileme belirtecini kullanarak ADAL tooget yeni bir erişim belirteci kullanabilirsiniz. Bu senaryo gösteren bir kod örneği için bkz: [Native client tooWeb API tooWeb API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Ayrıca Bkz.

- [Azure Active Directory Geliştirici Kılavuzu hello](active-directory-developers-guide.md)
- [Azure Active directory için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md)
- [Azure Active Directory kod örnekleri](active-directory-code-samples.md)
