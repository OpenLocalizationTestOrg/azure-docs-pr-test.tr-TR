---
title: "tooan içinde Federasyon için yapılandırılan Azure AD galerisinde uygulamanızı imzalama aaaProblems çoklu oturum açma | Microsoft Docs"
description: "Parola çoklu oturum açma için yapılandırılmış bir Azure AD galeri uygulama tootroubleshoot nasıl sorunlar"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a>Tooan Federasyon çoklu oturum açma için yapılandırılmış bir Azure AD galeri uygulama imzalama sorunları

Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir. Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz. Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.

toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Merhaba erişim paneli toplantı tarayıcı gereksinimleri

JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi. toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:

-   Internet Explorer 8, 9, 10, 11 - Windows 7 veya üzeri

-   Chrome - Windows 7 ve daha sonra ve MacOS x veya sonrası

-   Firefox 26,0 veya daha sonra - Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri

>[!NOTE]
>tarayıcı uzantıları köşesi desteklendiğinde hale kenar Windows 10 için kullanılabilir hale hello parola tabanlı SSO uzantısı.
>
>

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

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Internet Explorer için Grup İlkesi ayarı

Kullanıcılarınızın makinelerde Internet Explorer için tooremotely yükleme hello erişim paneli uzantısına izin ver Grup İlkesi ayarlayabilirsiniz.

Merhaba Önkoşullar şunlardır:

-   Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.

-   Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir. Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Merhaba öğreticisini izleyin [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) ilişkin adım adım yönergeler nasıl tooconfigure hello Grup İlkesi ve toousers dağıtın.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Merhaba erişim paneli Internet Explorer'da sorun giderme

Merhaba izleyin [sorun giderme hello Internet Explorer için erişim paneli uzantısı](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) hello uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Hello Azure AD Galeriden bir uygulama ekleme](#_Add_an_application)

-   [Merhaba uygulaması parola çoklu oturum açma için yapılandırma](#configure-the-application-for-password-single-sign-on)

-   [Kullanıcıların toohello uygulama atama](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama ekleme

tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:

1.  Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.

6.  Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.

7.  Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.

8.  Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.

9.  Tıklatın **Ekle** button, tooadd Merhaba uygulaması.

Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Merhaba uygulaması parola çoklu oturum açma için yapılandırma

tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Select hello modu **parola tabanlı oturum açma.**

9.  [Kullanıcıların toohello uygulama atama](#_How_to_assign).

10. Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme. Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.

### <a name="assign-users-toohello-application"></a>Kullanıcıların toohello uygulama atama

tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.

9.  Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.

10. Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.

11. Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**. Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.

12. **İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.

13. Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.

14. **İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.

15. Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.

Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a>Bu sorun giderme, adımları hello sorunu çözümlemek yok 
bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:

-   Bağıntı hata kimliği

-   UPN (kullanıcı e-posta adresi)

-   Tenantıd

-   Tarayıcı türü

-   Saat dilimi ve saat/zaman çerçevesine hata oluşuyor

-   Fiddler izlemeleri

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)
