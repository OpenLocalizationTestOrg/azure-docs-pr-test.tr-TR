---
title: "Parola tek oturum açma için Azure AD galeri uygulamanın yapılandırma aaaProblem | Microsoft Docs"
description: "Önceden listelenen uygulamalar için parola çoklu oturum açmayı hello Azure AD uygulama galerisinde yapılandırırken Hello ortak sorunları kişiler yüz anlama"
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
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Parola tek oturum açma için Azure AD galeri uygulamanın yapılandırma sorunu

Bu makalede yardımcı toounderstand hello ortak sorunları kişiler yüz yapılandırırken **parola çoklu oturum açma** Azure AD galeri uygulamayla.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>Kimlik bilgileri girilir ancak hello uzantısı bunları göndermez

Bu genellikle hello uygulamanın satıcısına oturum açma değiştiyse tooadd bir alan son sayfasında gerçekleşir, toodetect hello kullanıcı adı ve parola alanlarına kullandık temel alınan tanımlayıcı değiştirmek veya nasıl çalışır, uygulama için hello oturum açma deneyimi değiştirin. Neyse ki, çoğu durumda, Microsoft bu sorunları uygulama satıcıları toorapidly çözümleme ile çalışabilirsiniz.

Microsoft bu tümleştirmeler bölün, ancak bazen biz mümkün toofind değildir algılayabilir teknolojileri tooautomatically varken bu sorunları koyma ya da bunlar bazı alırken sağ toofix zaman. Bu tümleştirmeler biri doğru çalışmaz zaman hello durumda biz bunu mümkün olan en kısa sürede giderebilmemiz bir destek servis talebi açtıysanız veriyoruz.

Toplama toothis içinde **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde göndermek** toonatively biz ile çalışabilmek için Azure Active Directory ile kendi uygulama tümleştirin. Merhaba satıcı toohello gönderebilirsiniz [hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget bunları başlatıldı.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>Kimlik bilgileri doldurulur ve gönderildi, ancak hello kimlik bilgileri yanlışsa hello sayfa gösterir

Bu sorun, ilk onay hello aşağıdaki tooresolve:

-   İlk çok deneyin hello kullanıcınız**toohello uygulama Web sitesinin doğrudan oturum** kendileri için depolanan hello kimlik bilgilerine sahip.

  * Çalışırsa, hello tıklatın hello kullanıcı sahip **güncelleştirme kimlik bilgileri** hello düğmesinde **uygulama döşeme** hello içinde **uygulamaları** hello bölümünü [uygulama Erişim paneli](https://myapps.microsoft.com/) tooupdate bunları en son bilinen toohello kullanıcı adı ve parola çalışma.

   * Siz veya başka bir yönetici atanmış hello bu kullanıcının kimlik bilgilerinin, hello kullanıcı veya grubun uygulama atama toohello giderek bulursanız **kullanıcıları ve grupları** hello atama seçerek hello uygulamasının sekmesi ve Merhaba tıklatarak **güncelleştirme kimlik bilgileri** düğmesi.

-   Merhaba kullanıcı kendi kimlik bilgilerini atanmışsa hello kullanıcınız **toobe parolalarını hello uygulamada dolduğunu değil emin denetleyin** ve bu durumda, **süresi dolmuş parolasını güncelleştirmesi** toohello içinde açarak doğrudan uygulama.

   * Merhaba parola hello uygulamada güncelleştirildikten sonra hello kullanıcı tooclick hello isteği **güncelleştirme kimlik bilgileri** hello düğmesinde **uygulama döşeme** hello içinde **uygulamaları** Merhaba bölümünü [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) tooupdate bunları en son bilinen toohello kullanıcı adı ve parola çalışma.

   * Siz veya başka bir yönetici atanmış hello bu kullanıcının kimlik bilgilerinin, hello kullanıcı veya grubun uygulama atama toohello giderek bulursanız **kullanıcıları ve grupları** hello atama seçerek hello uygulamasının sekmesi ve Merhaba tıklatarak **güncelleştirme kimlik bilgileri** düğmesi.

-   Merhaba aşağıda hello açıklanan adımları izleyerek Hello kullanıcı güncelleştirme hello erişim paneli tarayıcı uzantısına sahip [nasıl tooinstall hello erişim paneli tarayıcı uzantısı](#how-to-install-the-access-panel-browser-extension) bölümü.

-   Merhaba erişim paneli tarayıcı uzantısı çalışır ve kullanıcı tarayıcıda etkin olduğundan emin olun.

-   Kullanıcılarınızın panelinden hello erişim sırasında toohello uygulamada toosign ayarlamadığınızdan emin olun **incognito, InPrivate ya da özel mod**. Merhaba erişim paneli uzantısı bu modda desteklenmiyor.

Bu işe yaramazsa durumunda, geçici olarak Azure AD ile Merhaba uygulamanın tümleştirme bozuk hello uygulama tarafında gerçekleşen bir değişikliği hello durumda olabilir. Merhaba uygulamanın satıcısına tanıtır Örneğin, bu giriş, hangi nedenler tümleştirmesi, kendi, toobreak gibi otomatik bir komut dosyası için el ile vs farklı şekilde davranan kendi sayfasında otomatik oluşabilir. Neyse ki, çoğu durumda, Microsoft bu sorunları uygulama satıcıları toorapidly çözümleme ile çalışabilirsiniz.

Microsoft bu tümleştirmeler bölün, ancak bazen biz mümkün toofind değildir algılayabilir teknolojileri tooautomatically varken bu sorunları koyma ya da bunlar bazı alırken sağ toofix zaman. Bu tümleştirmeler biri doğru çalışmaz zaman hello durumda biz bunu mümkün olan en kısa sürede giderebilmemiz bir destek servis talebi açtıysanız veriyoruz.

Toplama toothis içinde **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde göndermek** toonatively biz ile çalışabilmek için Azure Active Directory ile kendi uygulama tümleştirin. Merhaba satıcı toohello gönderebilirsiniz [hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget bunları başlatıldı.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>Chrome ve Firefox ancak Internet Explorer'da Hello uzantısı çalışır

Toothis sorunu iki ana nedeni vardır:

-   Yoksa hello Web sitesi Internet Explorer'da etkin hello güvenlik ayarlarına bağlı olarak parçası bir **Güvenilen Bölge**, bazen bizim betik engellenmesi hello uygulama için yürütme.

  *  tooresolve bunu hello kullanıcıdan çok isteyin**hello uygulamanın Web sitesi ekleme** toohello **Güvenilen siteler** içinde listesinde kendi **Internet Explorer güvenlik ayarlarını**. Kullanıcıların toohello gönderebilirsiniz [nasıl tooadd site toomy Güvenilen siteler listesini](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) makale ayrıntılı yönergeler için.

-   Nadir durumlarda, Internet Explorer'ın güvenlik doğrulaması bazen hello sayfa tooload hello betik yürütme işlemi bizim daha yavaş neden olabilir.

   * Ne yazık ki, bu durum hello tarayıcı sürümü, bilgisayarın hızı veya ziyaret siteye bağlı olarak değişebilir. Bu durumda, biz bu belirli uygulama hello tümleştirme giderebilmemiz desteğe başvurun öneririz.

Toplama toothis içinde **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde göndermek** toonatively biz ile çalışabilmek için Azure Active Directory ile kendi uygulama tümleştirin. Merhaba satıcı toohello gönderebilirsiniz [hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget bunları başlatıldı.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Hello uygulamanın oturum açma sayfasına kısa süre önce değiştirildi veya ek bir alan gerektirir, denetleyin

Merhaba uygulamanın oturum açma sayfasına büyük ölçüde değiştiyse, bazen bu bizim tümleştirmeler toobreak neden olur. Bu uygulamanın satıcısına işareti alan, bir güvenlik kodu ekler veya çok faktörlü kimlik doğrulaması tootheir karşılaştığında örneğidir. Neyse ki, çoğu durumda, Microsoft bu sorunları uygulama satıcıları toorapidly çözümleme ile çalışabilirsiniz.

Microsoft bu tümleştirmeler bölün, ancak bazen biz mümkün toofind değildir algılayabilir teknolojileri tooautomatically varken bu birlikte sorunları hemen. Aksi halde bazı zaman toofix gerçekleştirin. Bu tümleştirmeler biri doğru çalışmaz zaman hello durumda biz bunu mümkün olan en kısa sürede giderebilmemiz bir destek talebi açarak veriyoruz.

Toplama toothis içinde **bu uygulamanın satıcısına iletişim kurmayan varsa** **bizim şekilde göndermek** toonatively biz ile çalışabilmek için Azure Active Directory ile kendi uygulama tümleştirin. Merhaba satıcı toohello gönderebilirsiniz [hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget bunları başlatıldı.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Nasıl tooinstall hello erişim paneli tarayıcı uzantısı

tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:

1.  Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.

2.  Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.

3.  Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.

4.  Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir. **Ekleme** hello uzantısı tooyour tarayıcı.

5.  Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.

6.  Bir kez yüklenir, **yeniden** tarayıcı oturumunda.

7.  Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları

Ayrıca hello uzantısı Chrome ve Firefox için hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:

-   [Chrome erişim paneli uzantısı](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox erişim paneli uzantısı](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)

