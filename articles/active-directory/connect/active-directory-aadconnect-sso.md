---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma | Microsoft Docs"
description: "Bu konuda, Azure Active Directory (Azure AD) sorunsuz çoklu oturum açma ve nasıl, tooprovide true çoklu oturum açma Kurumsal ağınızdaki Kurumsal Masaüstü Kullanıcıları için verir açıklanmaktadır."
services: active-directory
keywords: "Azure AD, SSO, gerekli bileşenleri yükleme Active Directory, Azure AD Connect nedir çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory sorunsuz çoklu oturum açma

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory sorunsuz çoklu oturum açma nedir?

Azure Active Directory sorunsuz çoklu oturum açma (Azure AD sorunsuz SSO) otomatik olarak oturum açtığında şirket cihazları bağlı tooyour Kurumsal ağlarında olduklarında kullanıcıların. Etkin olduğunda, kullanıcılar yok tooAzure AD içinde kendi parolalarını toosign tootype gerekir ve genellikle, hatta kendi usernames öğesinde yazın. Bu özellik, herhangi bir şirket içinde ek bileşenini gerek kalmadan, tooyour bulut tabanlı uygulamalar, kullanıcıların kolay erişim sağlar.

Sorunsuz SSO ya da hello ile birleştirilebilir [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) veya [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md) oturum açma yöntemleri.

![Sorunsuz çoklu oturum açma](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>Sorunsuz SSO şu anda önizlemede değil. Bu özellik _değil_ geçerli tooActive Directory Federasyon Hizmetleri (ADFS).

## <a name="key-benefits"></a>Önemli avantajlar

- *Mükemmel bir kullanıcı deneyimi*
  - Kullanıcılar, şirket içi ve bulut tabanlı uygulamalar otomatik olarak imzalanmıştır.
  - Kullanıcılar, tooenter için sürekli olarak parolalarını sahip değilsiniz.
- *Kolay toodeploy & yönetme*
  - Herhangi bir ek bileşeni, bu iş şirket içi toomake gerekli.
  - Bulut kimlik doğrulaması - herhangi bir yöntemle çalışır [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) veya [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md).
  - Toosome veya tüm kullanıcılar Grup İlkesi kullanılarak alınabilir.
  - Herhangi bir AD FS altyapı hello gerek kalmadan Azure AD ile Windows 10 cihazları kaydedin. Bu özellik, toouse sürüm 2.1 veya hello sonraki gereken [çalışma alanına katılma istemcisi](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Özellik vurgular

- Oturum açma kullanıcı adı ya da hello şirket içi varsayılan kullanıcı adı olabilir (`userPrincipalName`) veya Azure AD Connect içinde yapılandırılmış başka bir öznitelik (`Alternate ID`). Sorunsuz SSO hello kullandığından her ikisi de durumlarda iş kullanmak `securityIdentifier` hello Kerberos bileti toolook hello karşılık gelen kullanıcı nesnesi oluşturan talep Azure AD'de.
- Sorunsuz SSO fırsatçılıktan bir özelliktir. Herhangi bir nedenle başarısız olursa, kullanıcı oturum açma deneyimini hello geri tooits normal davranış - yani, hello gider kullanıcı parolalarını hello oturum açma sayfasında tooenter gerekiyor.
- Bir uygulama iletirse bir `domain_hint` (Openıd Connect) veya `whr` (SAML) parametre - kiracınız, tanımlama veya `login_hint` hello kullanıcı tanımlama parametre - kendi Azure AD oturum açma isteğine, kullanıcıların otomatik olarak onlar olmadan oturum açtınız kullanıcı adlarını ve parolalarını girerek.
- Azure AD Connect üzerinden etkinleştirilebilir.
- Boş bir özelliktir ve Azure AD toouse Ücretli tüm sürümleri olması gerekmez.
- Web tarayıcısı tabanlı istemciler ve Destek Office istemcilerinde desteklenen [modern kimlik doğrulaması](https://aka.ms/modernauthga) platformlarında ve Kerberos kimlik doğrulaması özellikli tarayıcılar:

| OS\Browser |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Evet|Hayır|Evet|Evet\*|Yok
|Windows 8.1|Evet|Yok|Evet|Evet\*|Yok
|Windows 8|Evet|Yok|Evet|Evet\*|Yok
|Windows 7|Evet|Yok|Evet|Evet\*|Yok
|Mac OS X|Yok|Yok|Evet\*|Evet\*|Evet\*

\*Gerektirir [ek yapılandırma](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>Biz son kenar tooinvestigate desteği müşteri bildirilen sorunlar geri.

>[!NOTE]
>Toouse Windows 10 için hello önerilir [Azure AD katılım](../active-directory-azureadjoin-overview.md) hello en iyi tek oturum açma deneyimi için Azure AD ile.

## <a name="next-steps"></a>Sonraki adımlar

- [**Hızlı Başlangıç** ](active-directory-aadconnect-sso-quick-start.md) - hale getirmek ve Azure AD sorunsuz SSO çalışıyor.
- [**Teknik derinlemesine** ](active-directory-aadconnect-sso-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sık sorulan sorular** ](active-directory-aadconnect-sso-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
