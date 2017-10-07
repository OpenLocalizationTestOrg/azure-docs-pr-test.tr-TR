---
title: "aaaWhat hello erişim paneli Azure Active Directory'de mi? | Microsoft Belgeleri"
description: "Merhaba toouse varyasyonları paneli (web tarayıcısı, Android uygulaması, iPhone ve iPad uygulama) tooaccess SaaS uygulamaları nasıl erişim hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Merhaba erişim paneli nedir?

Merhaba erişim paneli web tabanlı bir portalıdır. Bir kullanıcı bir iş etkinleştirir veya Okul hesabında Azure AD yönetici izni Azure Active Directory tooview ve başlangıç bulut tabanlı uygulamalara erişim. Ayrıca, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.

Merhaba erişim paneli hello Azure portal ' ayrıdır ve siz toohave bir Azure aboneliği yapar.

![Erişim Paneli][1]

Merhaba erişim paneli dahil olmak üzere profil ayarlarınızı bazıları yeteneği hello tooedit sağlar:

- Bir iş veya Okul hesabıyla ilişkilendirilmiş hello Parolayı Değiştir

- Parola sıfırlama ayarlarını Düzenle

- Kişi ve tercih ayarlarını ilgili toomulti faktörlü kimlik doğrulamasını Düzenle (gerekli toouse silinmiş hesapları için bir yönetici tarafından)

- Kullanıcı kimliği gibi ayrıntıları e-posta ve mobil ve office telefon numaraları ve aygıtların alternatif hesabı görüntüleyin

- Azure AD Yöneticisi hello görünümü ve başlangıç bulut tabanlı uygulamalar verdi bunları erişimi. Merhaba erişim paneli hello kullanıcı açısından hakkında daha fazla bilgi için bkz: hello erişim paneli kullanma. 

- Kendi kendine gruplarını yönetin. Daha açık belirtmek gerekirse Merhaba yönetici oluşturun ve güvenlik grupları ve istek güvenlik grup üyeliklerini Azure AD içinde yönetin. Daha fazla bilgi için bkz: [Azure AD'de kullanıcıları için Self Servis Grup Yönetimi](active-directory-accessmanagement-self-service-group-management.md) ve [gruplarınızı yönetmesine](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Merhaba erişim paneli erişme

URL bir web tarayıcısında aşağıdaki hello ziyaret ederek hello erişim paneli erişebilirsiniz:`http://myapps.microsoft.com`

Oturum açma sayfanız için yapılandırılan özel marka varsa, bu, kuruluşunuzun etki alanı toohello hello URL'nin sonuna ekleyerek markalama yükleyebilirsiniz:`http://myapps.microsoft.com/<your domain>.com`

Bu durumda, Azure portalında yapılandırılmış herhangi bir etkin ya da doğrulanmış etki alanı adını kullanabilirsiniz.

![Wingtip Toys etki alanı adı][2]  

Azure AD ile tümleşik tooapplications imzalayacak toodistribute hello URL tooall kullanıcıların gerekir.

## <a name="authentication"></a>Kimlik Doğrulaması

tooreach hello erişim paneli, bir iş veya Okul hesabı ile Azure AD içinde kimliğinin doğrulanması gerekir. Kimliği doğrulanmış tooAzure AD doğrudan olabilir. Alternatif olarak, bir kuruluş, Active Directory Federasyon Hizmetleri (AD FS) veya diğer teknolojileri kullanarak Federasyon yapılandırdıysa, Windows Server Active Directory tarafından doğrulanabilir.

Azure veya Office 365 için bir abonelik varsa ve hello Azure portal veya bir Office 365 uygulama kullanmakta olduğunuz imzalama yeniden bileşenini olmadan hello uygulamaların listesini görebilirsiniz. Kullanıyorsanız doğrulanmaz hello kullanıcı adı ve parola hesabınız için Azure AD'de kullanıldığı istendiğinde toosign içinde değildir. Kuruluşunuzun Federasyon yapılandırdıysa, hello kullanıcı adı yazmaya yeterli olur.

Doğrulandığında, yöneticiniz hello directory ile tümleşik olan hello uygulamaları ile etkileşim kurabilir. Azure AD ile toointegrate uygulamaları nasıl görürüm toolearn [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Web tarayıcısı gereksinimleri

En azından, JavaScript destekleyen bir tarayıcı hello erişim paneli gerektirir ve CSS etkinleştirdi. Parola tabanlı çoklu oturum açma (SSO) aracılığıyla tooapplications imzalı hello kullanıcı toobe için tarayıcınızda hello erişim paneli uzantısı yüklü olması gerekir. parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinizde hello uzantısı otomatik olarak yüklenir.

Merhaba erişim paneli uzantısı Internet Explorer 8 ve üzeri, kenar, Chrome ve Firefox tarayıcılar için şu anda kullanılabilir değil.

## <a name="mobile-app-support"></a>Mobil uygulama desteği

Hello Azure Active Directory ekibi yayımlar hello uygulamaları mobil uygulamamı. Merhaba uygulamasını yüklediğinizde, iOS ve Android cihazlarda toopassword tabanlı SSO uygulamalarda imzalayabilirsiniz.

> [!NOTE]
> (Salesforce, Google Apps, Dropbox, kutusunda, Concur, iş günü, Office 365 ve diğerleri 70'den fazla dahil) Azure AD ile Federasyon desteği tooapplications içinde herhangi bir cihazda herhangi bir web tarayıcısında bir eklenti veya mobil uygulama gerek kalmadan imzalayabilirsiniz. Diğer tüm [erişim paneli deneyimleri](https://myapps.microsoft.com/) de benim uygulamaları mobil uygulama toobe kullanılan bir mobil cihazda hello gerektirmez.
>
>

### <a name="my-apps-for-android"></a>Uygulamalarım Android için

Uygulamalarım Android için desteklenen herhangi bir cihazda Android sürümü 4.1 çalıştıran Android ve daha sonra.  
Hello kullanılabilir [Google Play mağazasına](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![Uygulamalarım Android için][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>Uygulamalarım iPhone ve iPad için

Uygulamalarım iOS için herhangi bir iPhone veya iOS sürüm 7 ve üzeri çalıştıran iPad için desteklenir.  
Hello kullanılabilir [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![Uygulamalarım iOS için][4]    



## <a name="managed-browser-for-my-apps"></a>Uygulamalarım için yönetilen tarayıcı

Uygulamalarım hello Intune Managed Browser de tümleşiktir. iOS ve Android cihazlar için Intune Managed Browser Hello mobil cihazlarda veri güvenli kalmasını sağlamaya önemli bir rol oynar. Güvenli bir şekilde görüntülemenize ve şirket bilgileri içerebilen ve güvenli bir web tarama deneyimi sağlayan bir web sayfalarında gezinmek izin verir.  
Hızlı erişim toomy uygulamaları Managed Browser giriş sayfanız ve daha az vermiş işaretlerinizi tıklar tooreach tooaccess istediğiniz uygulamayı bulun.

Hello kullanılabilir [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) ve [Google Play mağazası](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Uygulamalarım Mananged tarayıcısı][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Sınama hello kullanıcı deneyimi için ipuçları

Azure Yöneticiyseniz ve hello dizininde bir hesap kullanarak toohello Azure portal imzalanmış, geçerli hesabınıza toohello erişim panelinde otomatik olarak imzalanmış. Bu durumda, tooyou atanmış olan tüm uygulamaları görebilirsiniz.

**tootest olarak bir *farklı* kullanıcı hesabı:**

1. Merhaba sağ üst köşesindeki hello Azure portal veya hello erişim paneli Hello kullanıcı menüsünü tıklatın ve ardından **oturum kapatma**. 
2. Toohello Git [erişim paneli](http://myapps.microsoft.com).
3. Hello oturum açma sayfası, türü hello kullanıcı adı ve parolasını hello dizininizde tootest istiyor.


## <a name="starting-applications"></a>Uygulamaları başlatma

Çeşitli uygulamaları hello erişim paneli üzerinde yer alabilir.

### <a name="office-365-applications"></a>Office 365 uygulamaları

Kuruluşunuz Office 365 uygulamaları kullanıyorsanız ve bunlar için lisanslanır hello Office 365 uygulamaları, erişim panelinde görüntülenir.

Bir Office 365 uygulama için bir uygulama kutucuğu'ı tıklattığınızda yeniden yönlendirilen toohello uygulama ve otomatik olarak oturum açmış olan yapılır.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Federasyon tabanlı SSO ile yapılandırılan Microsoft ve üçüncü taraf uygulamalar

Yöneticiniz uygulamaları hello SSO modu çok ayarlandığında hello hello Azure portalında Active Directory bölümünü ekleyebilirsiniz**Azure AD çoklu oturum açma**. Yöneticiniz açıkça toohello uygulamaları erişim izni varsa, yalnızca bu uygulamaları görebilirsiniz.

Bu uygulamalardan birini için bir kutucuğa tıkladığınızda, yeniden yönlendirilen ve toohello uygulamada oturumunuz otomatik olarak.

### <a name="password-based-sso-without-identity-provisioning"></a>Kimlik sağlama olmadan SSO parola tabanlı

Yöneticiniz uygulamaları hello SSO modu çok ayarlandığında hello hello Azure portalında Active Directory bölümünü ekleyebilirsiniz**parola tabanlı çoklu oturum açma**. Merhaba dizinindeki tüm kullanıcılar bu modda yapılandırılmış tüm uygulamaları görebilirsiniz.

Merhaba ilk kez, bu uygulamalardan birini için bir kutucuğa tıklayın, istendiğinde tooinstall hello parola SSO Internet Explorer veya Chrome için eklenti olur. Merhaba yükleme web tarayıcınız, toorestart gerektirebilir. Ne zaman toohello erişim paneli dönün ve bir kullanıcı adı ve parola Merhaba uygulaması için istenir hello uygulama döşeme tekrar tıklatın. Kullanıcı adınızı ve parolanızı girdikten sonra bu kimlik bilgileri güvenli bir şekilde depolanır ve Azure AD'de tooyour hesabına bağlanır.

Merhaba başlattığınızda toohello uygulamada oturumunuz otomatik olarak hello uygulama kutucuğuna tıklayın.  
Yok tooenter kimlik bilgilerinizi yeniden varsa ve veya hello parola SSO eklentisini yükleyin.

Kimlik bilgilerinizi hello hedef üçüncü taraf uygulama değiştirdiyseniz, Azure AD'de depolanan kimlik bilgilerinizi güncelleştirmeniz gerekir. 

**tooupdate kimlik bilgileri:**

1. Merhaba uygulama kutucuğuna Hello simgesini seçin.
2. Seçin **güncelleştirme kimlik bilgileri** tooreenter hello kullanıcı adı ve parolası hello uygulama.


### <a name="password-based-sso-with-identity-provisioning"></a>Kimlik sağlama ile parola tabanlı SSO

Yöneticiniz uygulamaları hello ekleyebilirsiniz **Active Directory** hello hello SSO modu Azure portalıyla bölümünü ayarlamak çok**parola tabanlı çoklu oturum açma**, kimlik sağlama yanı sıra.

Merhaba ilk kez, bir uygulama bölme için bu uygulamalardan birini tıklatın, istendiğinde tooinstall hello olduğunuz **parola SSO Internet Explorer veya Chrome için eklenti**. Merhaba yükleme web tarayıcınız, toorestart gerektirebilir.  
Ne zaman toohello erişim paneli dönün ve toohello uygulamada oturumunuz otomatik olarak yeniden hello uygulama kutucuğuna tıklayın.

Bazı uygulamalar, toochange hello ilk oturum açma parolanızı gerektirebilir. Kimlik bilgilerinizi hello hedef üçüncü taraf uygulama değiştirdiyseniz, Azure AD'de depolanan hello kimlik bilgilerini güncelleştirmeniz gerekir. 

**tooupdate kimlik bilgileri:**

1. Merhaba uygulama kutucuğuna Hello simgesini seçin.
2. Seçin **güncelleştirme kimlik bilgileri** tooreenter hello kullanıcı adı ve parolası hello uygulama.


### <a name="application-with-existing-sso-solutions"></a>Varolan SSO çözümleriyle uygulama

SSO tooconfigure bir uygulama için hello Azure portalı adı verilen üçüncü bir seçenek sağlar **varolan çoklu oturum açma**. Bu seçenek, yönetici toocreate bağlantı tooan uygulaması etkinleştirir ve Seçili kullanıcılar için hello erişim paneli yerleştirin.

Örneğin, bir uygulama, AD FS 2.0 kullanarak yapılandırılmış tooauthenticate kullanıcılar ise, yöneticiniz hello kullanabilirsiniz **varolan çoklu oturum açma** seçeneği toocreate hello erişim panelinde bağlantı tooit. Hello bağlantı eriştiğinizde, AD FS 2.0 veya ne olursa olsun varolan SSO çözüm hello uygulamanın sağladığı kimlik doğrulaması yapılır.


## <a name="next-steps"></a>Sonraki adımlar

- toosee ilgili tooapplication yönetimi, tüm konuların listesi görmek hello [Azure Active Directory'de uygulama yönetimi için makale dizini](active-directory-apps-index.md).
 
- toolearn nasıl toointegrate Azure AD SaaS bir uygulamaya bkz hello [nasıl öğreticiler listesi toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md).
 
- Azure AD ile uygulamaları yönetme hakkında daha fazla toolearn bkz hello [giriş toosingle oturum açma ve Azure Active Directory ile uygulama erişimini yönetme](active-directory-appssoaccess-whatis.md).
 
- Kullanıcı sağlama hakkında daha fazla toolearn bkz [kullanıcı sağlama ve tooSaaS uygulamaları etkinleştirmektir otomatikleştirmek](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
