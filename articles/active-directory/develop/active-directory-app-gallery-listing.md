---
title: "aaaListing hello Azure Active Directory Uygulama galerisinde uygulamanızı"
description: "Nasıl toolist çoklu oturum açma içinde destekleyen bir uygulama hello Azure Active Directory galeri | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme
Çoklu oturum açma Azure Active Directory ile hello destekleyen bir uygulama toolist [Azure AD galeri](https://azure.microsoft.com/marketplace/active-directory/all/), hello uygulamanın ilk tümleştirme modları aşağıdaki Merhaba, tooimplement gerekir:

* **Openıd Connect** - Openıd Connect kimlik doğrulamasını kullanan Azure AD ile tümleştirme doğrudan ve yapılandırması için Azure AD onay API hello. Uygulamanızı SAML desteklemez ve yalnızca bir tümleştirme başlıyorsanız, ardından hello öneri modu budur.
* **SAML** – hello özelliği tooconfigure üçüncü taraf kimlik sağlayıcıları hello SAML protokolü kullanarak uygulamanızı zaten sahiptir.

Her iki modda listeleme gereksinimleri aşağıda verilmiştir.

## <a name="openid-connect-integration"></a>Openıd Connect tümleştirme
toointegrate aşağıdaki hello Azure AD ile uygulamanızı [Geliştirici yönergeleri](active-directory-authentication-scenarios.md). Daha sonra tamamlamak aşağıdaki hello sorular ve göndermek toowaadpartners@microsoft.com.

* Uygulamanızla Azure AD team tootest hello tümleştirmesi hello tarafından kullanılan bir test Kiracı ya da hesabı için kimlik bilgilerini sağlayın.  
* Nasıl hello Azure AD team oturum açabilir ve Azure AD tooyour uygulaması hello kullanarak bir örneğine bağlanmak üzerinde yönergelerinizi [Azure AD onay framework](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Azure AD Hello için gerekli tüm ek yönergeler tootest çoklu oturum açma uygulamanız ile ekip sağlar. 
* Merhaba aşağıdaki bilgileri sağlayın:

> Şirket adı:
> 
> Şirket Web sitesi:
> 
> Uygulama adı:
> 
> Uygulama açıklaması (200 karakter sınırı):
> 
> Uygulama Web sitesi (bilgilendirme):
> 
> Uygulamanın teknik destek Web sitesi veya kişi bilgileri:
> 
> Https://portal.azure.com hello uygulama ayrıntıları gösterildiği gibi hello uygulamanın uygulama Kimliğini:
> 
> Ya da uygulama kayıt müşteriler için toosign nereye URL hello uygulama satın alın:
> 
> (Hello Azure Active Directory Marketi kullanılabilir kategorilerini görmek için) altında listelenen, uygulama toobe toothree kategorileri seçin:
> 
> Uygulama küçük simgesi (PNG dosyası, 45px, düz bir arka plan rengi tarafından 45px) ekleyin:
> 
> Uygulama büyük simge (PNG dosyası, 215px, düz bir arka plan rengi tarafından 215px) ekleyin:
> 
> Uygulama Logo (PNG dosyası, 122px, saydam arka plan rengi tarafından 150px) ekleyin:
> 
> 

## <a name="saml-integration"></a>SAML tümleştirme
SAML 2.0 destekleyen herhangi bir uygulama kullanarak doğrudan bir Azure AD kiracısı ile tümleştirilebilir [bu yönergeleri tooadd özel bir uygulama](../active-directory-saas-custom-apps.md). Uygulama tümleştirmesi Azure AD ile çalışıp çalışmadığını test ettikten sonra aşağıdaki bilgilerle çok hello Gönder<mailto:waadpartners@microsoft.com>.

* Uygulamanızla Azure AD team tootest hello tümleştirmesi hello tarafından kullanılan bir test Kiracı ya da hesabı için kimlik bilgilerini sağlayın.  
* SAML oturum açma URL'si, veren URL'si (varlık kimliği) hello ve yanıt URL'si (onaylama tüketici hizmeti), uygulamanız için değerleri açıklandığı gibi sağlamak [burada](../active-directory-saas-custom-apps.md). SAML meta veri dosyasının bir parçası olarak bu değer genellikle sağlarsanız, sonra Lütfen, de gönderebilirsiniz.
* Nasıl kısa bir açıklama sağlayın tooconfigure Azure AD kimlik sağlayıcısı SAML 2.0 kullanarak uygulamanızdaki. Uygulamanızı yapılandırma Azure AD kimlik sağlayıcısı Self Servis Yönetim Portalı üzerinden destekliyorsa, sonra lütfen yukarıda verilen hello kimlik hello özelliği tooset buna yukarı dahil emin olun.
* Merhaba aşağıdaki bilgileri sağlayın:

> Şirket adı:
> 
> Şirket Web sitesi:
> 
> Uygulama adı:
> 
> Uygulama açıklaması (200 karakter sınırı):
> 
> Uygulama Web sitesi (bilgilendirme):
> 
> Uygulamanın teknik destek Web sitesi veya kişi bilgileri:
> 
> Ya da uygulama kayıt müşteriler için toosign nereye URL hello uygulama satın alın:
> 
> Altında listelenen, uygulama toobe toothree kategorileri seçin (Merhaba kullanılabilir kategorilerini görmek için [Azure Active Directory Marketi](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Uygulama küçük simgesi (PNG dosyası, 45px, düz bir arka plan rengi tarafından 45px) ekleyin:
> 
> Uygulama büyük simge (PNG dosyası, 215px, düz bir arka plan rengi tarafından 215px) ekleyin:
> 
> Uygulama Logo (PNG dosyası, 122px, saydam arka plan rengi tarafından 150px) ekleyin:
> 
> 

