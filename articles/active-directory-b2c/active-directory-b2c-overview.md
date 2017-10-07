---
title: "Genel Bakış - Azure AD B2C | Microsoft Docs"
description: "Azure Active Directory B2C ile tüketiciye yönelik uygulamalar geliştirme"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure AD B2C: Siz uygulamanıza odaklanın, kayıt ve oturum açma işlemlerini bize bırakın

Azure AD B2C, web ve mobil uygulamalarınızda kullanabileceğiniz bulut tabanlı kimlik yönetim çözümüdür. Toohundreds kimlikleri milyonlarca ölçeklendirir yüksek oranda kullanılabilir bir küresel hizmet var. Kurumsal düzeyde güvenli bir platform üzerinde oluşturulan Azure AD B2C uygulamalarınızın, işinizin ve müşterilerinizin korunmasını sağlar.

En az yapılandırma ile Azure AD B2C, uygulama tooauthenticate sağlar:

* **Sosyal Hesaplar** (Facebook, Google, LinkedIn vs.)
* **Kurumsal Hesaplar** (açık standart protokollerini, OpenID Connect veya SAML kullanarak)
* **Yerel Hesaplar** (e-posta adresi ve parola veya kullanıcı adı ve parola)

## <a name="get-started"></a>başlarken

İlk olarak, kendi Kiracı özetlenen hello adımları kullanarak alma [bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).

Ardından uygulama geliştirme senaryonuzu seçin:

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Mobil Uygulamalar ve Masaüstü Uygulamaları](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />Mobil Uygulamalar ve Masaüstü Uygulamaları</center> | [Genel Bakış](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Web Apps](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [Genel Bakış](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.js](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![Tek Sayfa Uygulamaları](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />Tek Sayfa Uygulamaları</center> | [Genel Bakış](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![Web API'leri](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />Web API'leri</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [.NET web API'si çağırma](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>Yenilikler

Geri genellikle toolearn gelecekteki değişiklikler toohello Azure Active Directory B2C hakkında burayı tıklatın. @AzureAD kullanarak tüm değişiklikler hakkında tweet de göndereceğiz.

* Ayrıca "Yerleşik ilkeleri" (genel kullanılabilirlik), çok hello ["Özel ilkelerini"](active-directory-b2c-overview-custom.md) özellik artık genel önizlemede kullanılabilir durumdadır.  Özel ilkeler kimlik deneyimlerini hello oluşumunu üzerinde denetime ihtiyaç kimlik uzmanları içindir.
* Merhaba [erişim belirteci](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) özellik artık genel önizlemede kullanılabilir durumdadır.
* [Avrupa tabanlı Azure AD B2C dizinlerinin genel kullanıma açıldığı](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/) duyuruldu.
* Her geçen gün büyüyen [GitHub'daki kod örnekleri](https://github.com/Azure-Samples?q=b2c) kitaplığımıza göz atın!

## <a name="how-tooarticles"></a>Nasıl tooarticles

Bilgi nasıl toouse belirli Azure Active Directory B2C özellikleri:

* [Facebook](active-directory-b2c-setup-fb-app.md), [Google +](active-directory-b2c-setup-goog-app.md), [Microsoft hesabı](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) ve [LinkedIn](active-directory-b2c-setup-li-app.md) gibi hesapları, tüketiciye yönelik uygulamalarınızda kullanım için yapılandırın.
* [Özel öznitelikler toocollect bilgileri tüketicileriniz hakkında](active-directory-b2c-reference-custom-attr.md).
* [Tüketiciye yönelik uygulamalarınızda Azure Multi-Factor Authentication'ı etkinleştirin](active-directory-b2c-reference-mfa.md).
* [Tüketicileriniz için self servis parola sıfırlama ayarlayın](active-directory-b2c-reference-sspr.md).
* [Özelleştirme Hello Görünüm ve yapısını kaydolma, oturum açma ve diğer tüketiciye yönelik sayfaların](active-directory-b2c-reference-ui-customization.md) Azure Active Directory B2C tarafından sunulan.
* [Kullanım hello Azure Active Directory grafik API'si tooprogrammatically oluşturma, okuma, güncelleştirme ve tüketicileri silme](active-directory-b2c-devquickstarts-graph-dotnet.md) Azure Active Directory B2C kiracınızda.

## <a name="next-steps"></a>Sonraki adımlar

Bu bağlantılar hello hizmeti derinlemesine keşfetmek için kullanışlıdır:

* Merhaba bkz [Azure Active Directory B2C fiyatlandırma bilgileri](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Azure Active Directory B2C için [kod örneklerimizi](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) gözden geçirin. 
* Yığın taşması hello kullanarak Yardım [azure ad b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) etiketi.
* Kullanarak Bize düşüncelerinizi iletin [kullanıcı sesi](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), toohear istiyoruz bunları!
* Gözden geçirme hello [Azure AD B2C Protokolü başvurusu](active-directory-b2c-reference-protocols.md).
* Gözden geçirme hello [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md).
* Okuma hello [Azure Active Directory B2C ile ilgili SSS](active-directory-b2c-faqs.md).
* [Azure Active Directory B2C için dosya desteği istekleri](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma

Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.

