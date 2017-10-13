---
title: "Parola tek oturum açma için Azure AD galeri uygulamanın yapılandırma sorunu | Microsoft Docs"
description: "Azure AD uygulama galerisinde zaten listelenen uygulamalar için parola çoklu oturum açmayı yapılandırırken ortak sorunları kişiler yüz anlama"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 58d29996a922fac6d295e753ba5d66d32e745a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Parola tek oturum açma için Azure AD galeri uygulamanın yapılandırma sorunu

Bu makale ortak sorunları kişiler yüz yapılandırırken öğrenmenize yardımcı **parola çoklu oturum açma** Azure AD galeri uygulamayla.

## <a name="credentials-are-filled-in-but-the-extension-does-not-submit-them"></a>Kimlik bilgileri girilir ancak uzantı bunları göndermez

Bu, genellikle kullanıcı adı ve parola alanlarına algılamak veya nasıl çalışır, uygulama için oturum açma deneyimi değiştirmek için kullandık oturum açma sayfasını yakın zamanda bir alan eklemek için temel alınan tanımlayıcı değiştirmek için uygulama satıcısına değiştirilmesi durumunda gerçekleşir. Neyse ki, çoğu durumda, Microsoft Hızlı bir şekilde bu sorunları gidermek için uygulama satıcıları ile çalışabilirsiniz.

Microsoft bu tümleştirmeler bölün, ancak bazen bu sorunlar hemen bulmak yapamıyoruz veya düzeltmek için belirli bir süre devam otomatik olarak algılamak için teknolojilerini sahipken. Bu tümleştirmeler biri doğru çalışmaz zaman durumda biz bunu mümkün olan en kısa sürede giderebilmemiz bir destek servis talebi açtıysanız veriyoruz.

Bu, ek olarak **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde Gönder** bunları yerel olarak kendi uygulama Azure Active Directory ile tümleştirmek için ile çalışabilmek için. Satıcıya gönderebilirsiniz [Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) başlatılan getirmek için.

## <a name="credentials-are-filled-in-and-submitted-but-the-page-indicates-the-credentials-are-incorrect"></a>Kimlik bilgileri doldurulur ve gönderildi, ancak kimlik bilgileri yanlışsa sayfa gösterir

Bu sorunu çözmek için önce aşağıdakileri denetleyin:

-   Önce dener kullanıcınız **oturum uygulama Web sitesine doğrudan** kendileri için depolanan kimlik bilgileri.

  * Çalışan sonra tıklatın kullanıcı varsa **güncelleştirme kimlik bilgileri** düğmesini **uygulama döşeme** içinde **uygulamaları** bölümünü [uygulama erişim paneli ](https://myapps.microsoft.com/) en son bilinen çalışma kullanıcı adı ve parola güncelleştirmek için.

   * Siz veya başka bir yöneticinin bu kullanıcı için kimlik bilgilerini atanmışsa, kullanıcı veya grubun uygulama atama giderek bulmak **kullanıcıları ve grupları** atama seçerek ve tıklatarakuygulamasınınsekmesi **Kimlik bilgilerini güncelleştirmeniz** düğmesi.

-   Kullanıcı kendi kimlik bilgilerini atanan kullanıcı varsa **parolalarını uygulamada dolduğunu değil emin olmak için onay** ve bu durumda, **süresi dolmuş parolasını güncelleştirmesi** oturum açarak uygulamayı doğrudan.

   * Parola uygulamada güncelleştirildikten sonra kullanıcının'ı isteği **güncelleştirme kimlik bilgileri** düğmesini **uygulama döşeme** içinde **uygulamaları** bölümü [Uygulama erişim Paneli'ne](https://myapps.microsoft.com/) en son bilinen çalışma kullanıcı adı ve parola güncelleştirmek için.

   * Siz veya başka bir yöneticinin bu kullanıcı için kimlik bilgilerini atanmışsa, kullanıcı veya grubun uygulama atama giderek bulmak **kullanıcıları ve grupları** atama seçerek ve tıklatarakuygulamasınınsekmesi **Kimlik bilgilerini güncelleştirmeniz** düğmesi.

-   Aşağıda açıklanan adımları izleyerek erişim paneli tarayıcı uzantısı güncelleştirmek için kullanıcının sahip [erişim paneli tarayıcı uzantısı yükleme](#how-to-install-the-access-panel-browser-extension) bölümü.

-   Erişim paneli tarayıcı uzantısı çalışır ve kullanıcı tarayıcıda etkin olduğundan emin olun.

-   Kullanıcılarınız uygulamaya erişim panelinde oturum açmak ayarlamadığınızdan emin olun **incognito, InPrivate ya da özel mod**. Erişim paneli uzantısı bu modda desteklenmiyor.

Bu işe yaramazsa durumunda, geçici olarak Azure AD ile tümleştirme uygulamanın bozuk uygulama tarafında gerçekleşen bir değişikliği durumda olabilir. Uygulamanın satıcısına tanıtır Örneğin, bu giriş, hangi nedenler ayırmak için tümleştirme, gibi kendi, otomatik bir komut dosyası için el ile vs farklı şekilde davranan kendi sayfasında otomatik ortaya çıkabilir. Neyse ki, çoğu durumda, Microsoft Hızlı bir şekilde bu sorunları gidermek için uygulama satıcıları ile çalışabilirsiniz.

Microsoft bu tümleştirmeler bölün, ancak bazen bu sorunlar hemen bulmak yapamıyoruz veya düzeltmek için belirli bir süre devam otomatik olarak algılamak için teknolojilerini sahipken. Bu tümleştirmeler biri doğru çalışmaz zaman durumda biz bunu mümkün olan en kısa sürede giderebilmemiz bir destek servis talebi açtıysanız veriyoruz.

Bu, ek olarak **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde Gönder** bunları yerel olarak kendi uygulama Azure Active Directory ile tümleştirmek için ile çalışabilmek için. Satıcıya gönderebilirsiniz [Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) başlatılan getirmek için.

## <a name="the-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>Chrome ve Firefox, ancak Internet Explorer uzantısı çalışır

Bu sorun için iki ana nedeni vardır:

-   Web sitesi değilse, Internet Explorer'da etkin güvenlik ayarlarına bağlı olarak parçası bir **Güvenilen Bölge**, bazen bizim betik engellenmesi için uygulama yürütme.

  *  Bu sorunu çözmek için kullanıcıya isteyin **uygulamanın Web sitesi ekleme** için **Güvenilen siteler** içinde listesinde kendi **Internet Explorer güvenlik ayarlarını**. Kullanıcılarınıza gönderebilirsiniz [bir siteyi my Güvenilen siteler listesine eklemek nasıl](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) makale ayrıntılı yönergeler için.

-   Nadir durumlarda, Internet Explorer'ın güvenlik doğrulaması bazen bizim betik yürütme işlemi daha yavaş yüklemek sayfanın neden olabilir.

   * Ne yazık ki, bu durum tarayıcı sürümü, bilgisayarın hızı veya site ziyaret bağlı olarak değişebilir. Bu durumda, biz bu belirli uygulama tümleştirmesi giderebilmemiz desteğe başvurun öneririz.

Bu, ek olarak **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde Gönder** bunları yerel olarak kendi uygulama Azure Active Directory ile tümleştirmek için ile çalışabilmek için. Satıcıya gönderebilirsiniz [Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) başlatılan getirmek için.

## <a name="check-if-the-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Uygulamanın oturum açma sayfasına kısa süre önce değiştirildi veya ek bir alan gerektirir, denetleyin

Uygulamanın oturum açma sayfasına büyük ölçüde değiştiyse, bazen bu ayırmak bizim tümleştirmeler neden olur. Bir uygulamanın satıcısına alanında, captcha veya çok faktörlü kimlik doğrulaması deneyimlerini için bir oturum eklediğinde, bu örneğidir. Neyse ki, çoğu durumda, Microsoft Hızlı bir şekilde bu sorunları gidermek için uygulama satıcıları ile çalışabilirsiniz.

Microsoft teknolojileri otomatik olarak algıla sahipken kullandığınızda bu tümleştirmeler bölün ancak bazen bu sorunlar hemen bulmak yapamıyoruz. Aksi halde bunlar düzeltmek için biraz zaman ayırın. Bu tümleştirmeler biri doğru çalışmaz zaman durumda biz bunu mümkün olan en kısa sürede giderebilmemiz bir destek talebi açarak veriyoruz.

Bu, ek olarak **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde Gönder** bunları yerel olarak kendi uygulama Azure Active Directory ile tümleştirmek için ile çalışabilmek için. Satıcıya gönderebilirsiniz [Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) başlatılan getirmek için.

## <a name="how-to-install-the-access-panel-browser-extension"></a>Erişim paneli tarayıcı uzantısı yükleme

Erişim paneli tarayıcı uzantısı yüklemek için aşağıdaki adımları izleyin:

1.  Açık [erişim paneli](https://myapps.microsoft.com) olarak oturum açın ve desteklenen tarayıcılar birinde bir **kullanıcı** Azure ad.

2.  tıklatın bir **parola SSO uygulaması** erişim panelinde.

3.  Yazılımı yüklemek soran istem içinde seçin **Şimdi Yükle**.

4.  Tarayıcınıza bağlı için karşıdan yükleme bağlantısı yönlendirilmiş. **Ekleme** tarayıcınız uzantısı.

5.  Tarayıcınız isterse, ya da seçin **etkinleştirmek** veya **izin** uzantısı.

6.  Bir kez yüklenir, **yeniden** tarayıcı oturumunda.

7.  Erişim paneline oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları

Ayrıca uzantısı Chrome ve Firefox için aşağıya doğrudan bağlantılarından yükleyebilirsiniz:

-   [Chrome erişim paneli uzantısı](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox erişim paneli uzantısı](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Sonraki adımlar
[Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.](active-directory-application-proxy-sso-using-kcd.md)

