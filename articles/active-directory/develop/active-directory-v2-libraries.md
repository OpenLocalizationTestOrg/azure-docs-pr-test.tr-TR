---
title: "aaaAzure Active Directory v2.0 kimlik doğrulama kitaplıkları | Microsoft Docs"
description: "Uyumlu istemci kitaplıkları ve sunucu ara yazılım kitaplıkları ve ilgili kitaplık, kaynak ve hello Azure Active Directory v2.0 uç noktası için örnekleri bağlantılar."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Azure Active Directory v2.0 kimlik doğrulama kitaplıkları
Hello Azure Active Directory (Azure AD) v2.0 uç hello endüstri standardı OAuth 2.0 ve Openıd Connect 1.0 protokollerini destekler. Microsoft ve diğer kuruluşlardan çeşitli kitaplıklarından hello v2.0 uç noktası ile kullanabilirsiniz.

Merhaba v2.0 uç noktası kullanan bir uygulama oluşturduğunuzda, bir güvenlik geliştirme yaşam döngüsü (SDL) Metodoloji gibi izleyin Protokolü etki alanı uzmanlar tarafından yazılan kitaplıkları kullanmanızı öneririz [birMicrosofttarafındanizlenenhello] [Microsoft-SDL]. Merhaba protokolleri toohand kod desteği karar verirseniz, SDL Metodoloji izleyin ve Kapat toohello güvenlik konuları hello standartları özellikleri her protokol için dikkat öneririz.

## <a name="types-of-libraries"></a>Tür kitaplıkları
Azure AD v2.0 iki tür kitaplıklarını çalışır:

* **İstemci kitaplıkları**. Yerel istemcileri ve sunucuları Microsoft Graph gibi bir kaynak çağırmak için istemci kitaplıkları tooget erişim belirteçleri kullanın.
* **Sunucu ara yazılım kitaplıkları**. Web uygulamaları, kullanıcı oturum açma için sunucu ara yazılım kitaplıkları kullanabilirsiniz. Web API'leri yerel istemciler veya diğer sunucular tarafından gönderilen sunucu ara yazılımı kitaplıkları toovalidate belirteçlerini kullanın.

## <a name="library-support"></a>Kitaplık desteği
Merhaba v2.0 uç noktası kullandığınızda herhangi bir standartlara uygun kitaplığı seçebilirsiniz, önemli tooknow demektir nerede toogo desteği. Sorunları ve kitaplık kodu özellik istekleri için hello kitaplığı sahibine başvurun. Sorunları ve hello Hizmet tarafı protokol uygulanması özellik istekleri için Microsoft'a başvurun.

Kitaplıkları iki destek kategoride getirir:

* **Microsoft tarafından desteklenen**. Microsoft bu kitaplıklar için düzeltme sağlayan ve SDL yapmıştır Bu kitaplıklar üzerinde durum tespitlerini.
* **Uyumlu**. Microsoft, bu kitaplıklar temel senaryolarda test ve hello v2.0 uç noktası ile çalıştıkları onaylandı. Bu kitaplıklar için düzeltmeler ve bu kitaplıklar gözden yapılmadı Microsoft sağlamaz. Sorunları ve özellik istekleri yönlendirilmiş toohello kitaplığın açık kaynaklı proje olması gerekir.

Merhaba v2.0 uç noktası ile çalışma kitaplıkların bir listesi için bu makaledeki hello sonraki bölümlere bakın.


## <a name="microsoft-supported-client-libraries"></a>Microsoft tarafından desteklenen istemci kitaplıkları

> [!IMPORTANT]
> Merhaba MSAL Önizleme kitaplıkları, bir üretim ortamında kullanım için uygundur. Sağladığımız bizim geçerli üretim kitaplığı (ADAL) yaptığımız hello Bu kitaplıklar için aynı üretim düzeyi desteği. Merhaba Önizleme sırasında değişiklikleri toohello MSAL API, dahili önbellek biçimini vermiyoruz ve hata düzeltmeleri veya özellik geliştirmeleri birlikte tootake diğer mekanizmaları size bildirim olmadan bu kitaplıklar için gerekli. Bu, uygulamanızın etkileyebilir. Örneği için bir değişiklik toohello önbellek biçimini toosign içinde yeniden erişmeleri gibi kullanıcılarınızın etkileyebilir. Bir API değişikliği, tooupdate kodunuzu gerektirebilir. Merhaba tooupdate toohello genel kullanılabilirlik sürümü altı ay içinde isteriz genel kullanılabilirlik sürümü sağladığımız açtığınızda Önizleme kullanılarak yazılmış uygulamalar olarak kitaplığı sürümü artık çalışabilir.

| Platform | Kitaplık | İndir | Kaynak kodu | Örnek | Başvuru
| --- | --- | --- | --- | --- | --- |
| .NET istemci, Windows mağazası, UWP, Xamarin iOS ve Android | MSAL .NET (Önizleme) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Masaüstü uygulaması](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (Önizleme) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Tek sayfa uygulaması](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS, macOS | MSAL (Önizleme) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS uygulaması](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (Önizleme) | [Merhaba merkezi deposu](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android uygulaması](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Microsoft tarafından desteklenen sunucu ara yazılım kitaplıkları

| Platform | Kitaplık | İndir | Kaynak kodu | Örnek | Başvuru
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | OWIN Openıd Connect Ara |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[MVC uygulama](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | OWIN OAuth taşıyıcı ara yazılımı Azuread'i için |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | .NET 4.5 için JWT işleyicisi | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | ASP.NET Openıd Connect Ara |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[ASP.NET güvenliği (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[MVC uygulama](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | ASP.NET OAuth taşıyıcı ara yazılımı |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[ASP.NET güvenliği (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | .NET Core için JWT işleyicisi  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Web uygulaması](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Uyumlu istemci kitaplıkları
| Platform | Kitaplık adı | Test edilen sürüm | Kaynak kod | Örnek |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Yerel uygulaması örneği](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Yerel uygulaması örneği](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Uyumlu bir sunucu ara yazılım kitaplıkları
| Platform | Kitaplık adı | Test edilen sürüm | Kaynak kod | Örnek |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribe Java scribejava](https://github.com/scribejava/scribejava) | [Sürüm 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [Merhaba PHP ligi oauth2-istemci](https://github.com/thephpleague/oauth2-client) | [Sürüm 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2 istemci](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python Flask |[Flask OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask OAuthlib](https://github.com/lepture/flask-oauthlib) |[Web Uygulaması](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>İlgili içerik
Merhaba hello Azure AD v2.0 uç noktası hakkında daha fazla bilgi için bkz: [Azure AD uygulama modeli v2.0 genel bakış][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
