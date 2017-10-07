---
title: "Sık sorulan sorular (SSS) - Azure AD B2C | Microsoft Docs"
description: "Azure Active Directory B2C hakkında sık sorulan sorular"
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: Sık sorulan sorular (SSS) 
Bu sayfayı hello Azure Active Directory (Azure AD) B2C hakkında sık sorulan sorular yanıtlanmaktadır. Geri Güncelleştirmeler denetleniyor tutun.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>My var olan, çalışan tabanlı Azure AD kiracısı Azure AD B2C özellikleri kullanabilir miyim?
Azure AD ve Azure AD B2C ayrı ürün teklifleri ve hello aynı olamayacağı Kiracı.  Azure AD kiracısı bir kuruluşu temsil eder.  Azure AD B2C kiracısı ile bağlı olan taraf uygulamaları kullanılan kimlikleri toobe koleksiyonunu temsil eder.  Özel ilkelerinde ile (genel Önizleme), Azure AD B2C tooAzure AD izin verme kimlik doğrulama bir kuruluşta çalışan devredebilir.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Office 365'te Azure AD B2C tooprovide sosyal oturum açma (Facebook ve Google +) kullanabilir miyim?
Azure AD B2C, Microsoft Office 365 için kullanılan tooauthenticate kullanıcılar olamaz.  Azure AD çalışan erişim tooSaaS uygulamaları yönetmek için Microsoft çözümü ve lisans ve koşullu erişim gibi bu amaç için tasarlanmış özellikler vardır.  Azure AD B2C, web ve mobil uygulamaları oluşturmak için bir kimlik ve erişim yönetim platformu sağlar.  Azure AD B2C yapılandırılmış toofederate tooan Azure AD kiracısı olduğunda hello Azure AD kiracısı Azure AD B2C kullanan çalışan erişim tooapplications yönetir.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Azure AD B2C yerel hesaplarında nelerdir? Nasıl bunlar Azure AD içinde iş veya Okul hesapları farklı misiniz?
Bir Azure AD kiracısında toohello Kiracı ait olan kullanıcıların oturum açma hello form ile bir e-posta adresi `<xyz>@<tenant domain>`.  Merhaba `<tenant domain>` hello birini hello etki alanlarında Kiracı veya ilk hello doğrulanır `<...>.onmicrosoft.com` etki alanı. Bu hesap türü bir iş veya Okul hesabıdır.

Bir Azure AD B2C kiracısı çoğu uygulamaları hello kullanıcı toosign-herhangi bir rastgele e-posta adresi ile istediğiniz (örneğin, joe@comcast.net, bob@gmail.com, sarah@contoso.com, veya jim@live.com). Bu hesap türü, bir yerel hesaptır.  Ayrıca isteğe bağlı bir kullanıcı adları yerel hesaplar (örneğin, Can, bob, sarah veya jim) destekliyoruz. Azure AD B2C'hello Azure portal yapılandırarak bu iki yerel hesap türünden birini seçebilirsiniz.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>Hangi sosyal kimlik sağlayıcıları, artık destekliyor musunuz? Bunu hangilerinin hello gelecekteki toosupport planlama?
Şu anda Facebook, Google +, LinkedIn, Amazon, Twitter (Önizleme), WeChat (Önizleme), Weibo (Önizleme) ve h destekliyoruz (Önizleme). Müşteri talebe göre diğer popüler sosyal kimlik sağlayıcıları için destek ekleyeceğiz.

Azure AD B2C için destek de ekledi [özel ilkeler](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Bunlar [özel ilkeler](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) herhangi bir kimlik sağlayıcısı ile destekleyen kendi İlkesi Geliştirici toocreate izin [Openıd Connect](http://openid.net/specs/openid-connect-core-1_0.html) veya SAML. 

Kullanıma göre özel ilkelerini kullanmaya başlama bizim [özel ilke başlangıç paketi](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>Çeşitli sosyal kimlik sağlayıcılardan gelen tüketicileri hakkında daha fazla bilgi kapsamları toogather yapılandırabilir miyim?
Hayır, ancak bu özellik üzerinde bizim yol haritası. desteklenen bizim sosyal kimlik sağlayıcıları kümesi için kullanılan hello varsayılan kapsamları şunlardır:

* Facebook: e-posta
* Google +: e-posta
* Microsoft hesabı: openıd e-posta profili
* Amazon: profili
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>Uygulamam Azure AD B2C ile çalışmak için Azure üzerinde çalışan toobe var mı?
Hayır, uygulamanızda herhangi bir yerde (Merhaba Bulut veya şirket içi) barındırabilir. Azure AD B2C ile toointeract gereken tek şey özelliği toosend hello ve genel olarak erişilebilir uç noktaları HTTP isteklerini almak.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Birden çok Azure AD B2C Kiracı var. Nasıl bunları Azure portal hello üzerinde yönetebilirim?
'Azure AD B2C' hello Azure portalında, sol tarafındaki menüsünde hello açmadan önce geçiş gerekir hello dizine toomanage istiyor.  Kimliğinizi hello sağ üst tarafındaki hello Azure portal'ın tıklatarak dizinleri geçiş sonra hello açılan dizininde görüntülenen seçin.  Bir adım adım için görüntülerle görün [tooAzure AD B2C ayarlarını gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Nasıl doğrulama e-postaları özelleştirebilirim (Merhaba içerik ve hello "den:" alan) Azure AD B2C tarafından gönderilen?
Merhaba kullanabilirsiniz [şirket markası özelliğini](../active-directory/active-directory-add-company-branding.md) toocustomize hello içerik doğrulama e-postaların. Özellikle, bu iki öğenin hello e-postanın özelleştirilebilir:

* **Kapak sayfası logosu**: hello sağ alt gösterilen.
* **Arka plan rengi**: hello üst kısmında gösterilen.

    ![Özelleştirilmiş doğrulama e-posta ekran görüntüsü](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

Merhaba e-posta imza hello B2C Kiracı ilk oluşturduğunuzda belirttiğiniz hello B2C kiracının adını içerir. Bu yönergeleri kullanarak hello adını değiştirebilirsiniz:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Abonelik Yöneticisi hello gibi.
1. Tooyour B2C Kiracı gidin.
1. Merhaba tıklatın **yapılandırma** sekmesi.
1. Değişiklik hello **adı** hello altında **Directory özellikleri** bölümü.
1. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.

Şu anda hiçbir şekilde toochange hello yok "den:" Merhaba e-posta alan. Oy [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) hello hello doğrulama e-posta gövdesi özelleştirme ilgilendiğiniz.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Nasıl my varolan kullanıcı adları, parolalar ve profilleri my veritabanı tooAzure AD B2C geçişini sağlayabilir miyim?
Geçiş Aracı hello Azure AD Graph API toowrite kullanabilirsiniz. Merhaba bkz [grafik API'si örnek](active-directory-b2c-devquickstarts-graph-dotnet.md) Ayrıntılar için.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Parola ilkeleri, Azure AD B2C'de yerel hesaplar için kullanılır?
Merhaba yerel hesaplar için Azure AD B2C parola ilkesi hello ilkesi için Azure AD temel alır. Azure AD B2C kaydı, kayıt veya oturum açma ve parola ilkeleri kullanan hello "güçlü" parola gücünü sıfırlamak ve parolaları süresi sona ermiyor. Okuma hello [Azure AD parola ilkesi](https://msdn.microsoft.com/library/azure/jj943764.aspx) daha fazla ayrıntı için.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>My şirket içi Active Directory tooAzure AD B2C depolanan Azure AD Connect toomigrate tüketici kimliği kullanabilir miyim?
Hayır, Azure AD Connect Azure AD B2C ile tasarlanmış toowork değil. Merhaba kullanmayı [grafik API'si](active-directory-b2c-devquickstarts-graph-dotnet.md) kullanıcı geçişi için.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>Uygulamam IFRAME içinde Azure AD B2C sayfalar yukarı açabilir miyim?
Hayır, güvenlik nedenleriyle, Azure AD B2C sayfaları IFRAME içinde açılamaz.  Hizmetimiz hello tarayıcı tooprohibit IFRAMES ile iletişim kurar.  güvenlik topluluğu genel hello ve OAUTH2 belirtimi Merhaba, IFRAMES için kimlik deneyimi tıklatın jacking toohello riskini son karşı kullanılması önerilir.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Azure AD B2C gibi Microsoft Dynamics CRM sistemleri ile çalışır mı?
Microsoft Dynamics 365 portalı ile tümleştirme kullanılabilir.  Bkz: [kimlik doğrulaması için yapılandırma Dynamics 365 Portal toouse Azure AD B2C](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Azure AD B2C mu iş SharePoint şirket içi 2016 veya önceki?
Azure AD B2C hello SharePoint dış iş ortağı paylaşımı senaryo için tasarlanmamıştır; bkz: [Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) yerine.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Azure AD B2C veya B2B toomanage dış kimlikler kullanmalıyım?
Bu makaleyi okuyun [dış kimlikler](../active-directory/active-directory-b2b-compare-external-identities.md) hello uygulama hakkında daha fazla uygun toolearn özellikleri tooyour Dış kimlik senaryoları.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Hangi raporlama ve Özellikler Denetim Azure AD B2C sağlar? Aynı Azure AD Premium olduğu gibi hello misiniz?
Hayır, Azure AD B2C aynı Azure AD Premium olarak raporlarını ayarlamak hello desteklemez. Ancak birçok commonalities vardır:

* Merhaba oturum açma raporları her oturum açma azaltılmış ayrıntılarla kaydını sağlar.
* Denetim raporları hello Azure portal, Azure Active Directory altında bulunan > etkinlik denetim günlüklerini > B2C seçin ve istediğiniz gibi filtreler uygulayabilirsiniz. Hem yönetici etkinliği, hem de uygulama etkinlik ele alınmıştır. 
* Kullanıcı sayısı, oturum açma sayısı ve MFA hacmi kapsayan bir kullanım raporu şu adreste bulunabilir [kullanım raporlama API'si](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Hello Azure AD B2C tarafından sunulan sayfaların UI yerelleştirme? Hangi dilleri destekleniyor mu?
Evet!  Hakkında bilgi edinin [dil özelleştirme](active-directory-b2c-reference-language-customization.md), genel önizlemede değil.  36 diller için çeviriler sağladığımız ve gereksinimlerinizi herhangi dize toosuit ayarlarını geçersiz kılabilir.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Azure AD B2C tarafından sunulan my kaydolma ve oturum açma sayfalarında kendi URL'leri kullanabilir miyim? Login.microsoftonline.com toologin.contoso.com hello URL örneği için değiştirebilirim?
Şu anda değil. Bu özellik bizim yol haritası üzerinde kullanılabilir. Merhaba etki alanınızda doğrulama **etki alanları** hello Klasik Azure portalı sekmesinde bu hedef gerçekleştirmek değil.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>My Azure AD B2C kiracısı nasıl silebilirim?
Bu adımları toodelete Azure AD B2C kiracınızın izleyin:

1. Bu adımları çok[tooAzure AD B2C ayarlarını gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
1. Toohello gidin **uygulamaları**, **kimlik sağlayıcıları**, ve **tüm ilkeler** ve bunların her birini tüm hello girişleri silin.
1. Şimdi toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Abonelik Yöneticisi hello gibi. (Aynı iş veya Okul hesabı veya toosign Azure için kullandığınız aynı Microsoft hesabı hello hello kullanın.)
1. Merhaba sol toohello Active Directory uzantısına gidin ve B2C kiracısına tıklayın.
1. Merhaba tıklatın **kullanıcılar** sekmesi.
1. Her kullanıcı Aç (dışlama hello abonelik yönetici kullanıcı, şu anda olarak oturum açtınız) seçin. Tıklatın **silmek** hello sayfasının ve tıklatın hello altındaki **Evet** istendiğinde.
1. Merhaba tıklatın **uygulamaları** sekmesi.
1. Seçin **Şirketimin sahip olduğu uygulamalar** hello içinde **Göster** açılan alan ve tıklatın hello onay işareti.
1. Bir uygulama olarak adlandırılan **b2c uzantıları uygulaması**. Tıklatın **silmek** hello sayfasının ve tıklatın hello altındaki **Evet** istendiğinde.
1. Yeniden toohello Active Directory uzantısına gidin ve B2C kiracınızın seçin.
1. Tıklatın **silmek** hello sayfanın hello sonundaki. toocomplete hello işlemi, Merhaba ekranında hello yönergeleri izleyin.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Azure AD B2C Enterprise Mobility Suite'in parçası olarak alabilir miyim?
Hayır, Azure AD B2C Kullandıkça Öde Azure hizmeti ve Enterprise Mobility Suite'in parçası değil.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Azure AD B2C ile ilgili sorunları nasıl rapor edebilirim?
Bkz: [Azure Active Directory B2C için dosya desteği istekleri](active-directory-b2c-support.md).
