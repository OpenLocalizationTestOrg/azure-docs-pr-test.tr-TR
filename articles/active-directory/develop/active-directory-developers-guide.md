---
title: "Geliştiriciler için Active Directory aaaAzure | Microsoft Docs"
description: "Bu makale, Azure Active Directory kullanarak Microsoft iş ve okul hesaplarında oturum açmaya genel bakış sunmaktadır."
services: active-directory
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4dbbea6c1e0b8a70c0c36ddd1caec5658130a003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-for-developers"></a>Geliştiriciler için Azure Active Directory
Azure Active Directory toosecurely oturum herhangi bir kullanıcı bir iş veya Okul hesabıyla Microsoft tarafından yedeklenen açma geliştiricilerinin sağlayan bir bulut kimlik hizmetidir.  Burada Hello belgeleri nasıl tooadd Azure AD destek endüstri standart kimlik doğrulama protokolleri, OAuth ve Openıd Connect kullanarak tooyour uygulama gösterir.

| | |
| --- | --- |
|[Auth temel bilgileri](active-directory-authentication-scenarios.md) | Azure AD ile bir giriş tooauthentication |
|[Uygulama türleri](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Azure AD tarafından desteklenen hello kimlik doğrulama senaryoları genel bakış |                                
                                                                              
## <a name="get-started"></a>başlarken
Destekli bu ayarlar, Azure Active Directory Kullanıcıları, kimlik doğrulama kitaplıkları toosign kullanılarak üzerinden yol.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Mobil Uygulamalar ve Masaüstü Uygulamaları](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />Mobil Uygulamalar ve Masaüstü Uygulamaları</center> | [Genel Bakış](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET](active-directory-devquickstarts-dotnet.md)<br /><br />[Windows](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md)<br /><br />[OAuth 2.0](active-directory-protocols-oauth-code.md) |
| <center>![Web Apps](./media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [Genel Bakış](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [NodeJS](active-directory-devquickstarts-openidconnect-nodejs.md)<br /><br />[OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) |  |
| <center>![Tek Sayfa Uygulamaları](./media/active-directory-developers-guide/SPA.png)<br />Tek Sayfa Uygulamaları</center> | [Genel Bakış](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![Web API'leri](./media/active-directory-developers-guide/Web_API.png)<br />Web API'leri</center> | [Genel Bakış](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[NodeJS](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![Hizmetten hizmete](./media/active-directory-developers-guide/Service_App.png)<br />Hizmetten hizmete</center> | [Genel Bakış](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#server-or-daemon-application-to-web-api)<br /><br />[OAuth 2.0 İstemci Kimlik Bilgileri](active-directory-protocols-oauth-service-to-service.md) |  |

## <a name="guides"></a>Kılavuzlar
Bu makaleler Azure Active Directory ile nasıl tooperform ortak görevleri bildirir.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[Uygulama kaydı](active-directory-integrating-applications.md)           | Nasıl tooregister Azure AD'de uygulama |
|[Çok kiracılı uygulamalar](active-directory-devhowto-multi-tenant-overview.md)    | Toosign herhangi bir Microsoft hesabı nasıl çalışır |
|[OAuth ve OpenID Connect](active-directory-protocols-openid-connect-code.md)| Bizim modern kimlik doğrulama protokolleri kullanarak API'leri toosign kullanıcıların ve çağrı web nasıl |
|[Diğer kılavuzlar...](active-directory-developers-guide-index.md#guides)        |     |

## <a name="reference"></a>Başvuru
Bu makaleler, Azure Active Directory’de kullanılan API'ler, protokol iletileri ve terimler hakkında ayrıntılı bilgi sağlar.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [Kimlik Doğrulama Kitaplıkları (ADAL)](active-directory-authentication-libraries.md)   | Merhaba kitaplıkları & SDK'ları Azure AD tarafından sağlanan genel bakış |
| [Kod örnekleri](active-directory-code-samples.md)                                  | Tüm Azure AD kod örneklerinin listesi |
| [Sözlük](active-directory-dev-glossary.md)                                      | Bu belgede kullanılan terminoloji ve sözcük tanımları |
| [Diğer başvuru kaynakları...](active-directory-developers-guide-index.md#reference)|     |

## <a name="help--support"></a>Yardım ve Destek
Azure Active Directory üzerinde geliştirme hello en iyi yerler tooget Yardım bunlar.

|  |  
|---|
|[Stack Overflow’da `azure-active-directory` ve `adal` etiketleri](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)      |
|[Azure Active Directory geri bildirimleri](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)|
| [Microsoft Dev Chat'i (sınırlı bir süre için ücretsiz) deneyin](http://aka.ms/devchat) |

<br />

> [!NOTE]
> Microsoft Kişisel hesapları toosign bileşenini gerekiyorsa, hello kullanarak tooconsider isteyebilirsiniz [Azure AD v2.0 uç](active-directory-appmodel-v2-overview.md).  tek bir kimlik doğrulaması sistemine hello Birleştirici Microsoft Kişisel hesapları & Microsoft iş hesaplarından (Azure AD) Hello Azure AD v2.0 uç noktadır.
