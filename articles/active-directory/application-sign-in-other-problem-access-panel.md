---
title: "Merhaba erişim paneli tooan uygulamadan imzalama aaaProblems | Microsoft Docs"
description: "Bir uygulama erişiminde tootroubleshoot sorun myapps.microsoft.com adresindeki Microsoft Azure AD erişim paneli nasıl hello"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Merhaba erişim panelinden tooan uygulamada oturum sorunları

Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni. 

Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır. Merhaba uygulaması düzgün şekilde yapılandırılmalıdır ve atanan toohello kullanıcı veya grup hello kullanıcı toosee hello hello erişim paneli uygulamada üyesidir.

bir kullanıcı için görüyor olabilirsiniz uygulamalarının Hello türü kategorileri aşağıdaki hello ayrılır:

-   Office 365 uygulamaları

-   Federasyon tabanlı SSO ile yapılandırılan Microsoft ve üçüncü taraf uygulamalar

-   Parola tabanlı SSO uygulamaları

-   Varolan SSO çözümleriyle uygulamaları

## <a name="general-issues-toocheck-first"></a>Genel toocheck ilk sorunları

-   Kullanarak emin bir **tarayıcı** hello hello erişim paneli için minimum gereksinimleri karşılayan.

-   Merhaba kullanıcının tarayıcısının hello uygulama tooits hello URL'sini ekledi emin olun **Güvenilen siteler**.

-   Toocheck Merhaba uygulaması olduğundan emin olun **yapılandırılmış** doğru.

-   Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.

-   Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**

-   Emin hello kullanıcının olun **parola süresi değil veya unutulursa.**

-   Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.

-   Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.

-   Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu.

-   Tarayıcınızın tanımlama bilgilerini temizleyip ve toosign olarak yeniden deneniyor yapma emin tooalso deneyin.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Merhaba erişim paneli toplantı tarayıcı gereksinimleri

JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi. toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:

-   Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri

-   Edge Windows 10 Anniversary Edition veya daha yenisi

-   Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde

-   Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Nasıl tooinstall hello erişim paneli tarayıcı uzantısı

tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:

1.  Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.

2.  Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.

3.  Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.

4.  Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir. **Ekleme** hello uzantısı tooyour tarayıcı.

5.  Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.

6.  Bir kez yüklenir, **yeniden** tarayıcı oturumunda.

7.  Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları

Ayrıca hello uzantısı Chrome ve kenar hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:

-   [Chrome erişim paneli uzantısı](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Edge erişim paneli uzantısı](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD galeri uygulaması için çoklu oturum açmayı tooconfigure nasıl Federasyon

Kurumsal çoklu oturum açma özelliğine sahip etkin hello Azure AD galerisinde tüm uygulama kullanılabilir bir adım adım öğretici sahiptir. Merhaba erişebilirsiniz [nasıl öğreticiler listesi toointegrate SaaS uygulamaları Azure Active Directory ile](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) ayrıntılı adım adım yönergeler için.

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Hello Azure AD Galeriden bir uygulama ekleme](#add-an-application)

-   [Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD meta verileri ve sertifika alma](#download-the-azure-ad-metadata-or-certificate)

-   [Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Kullanıcıların toohello uygulama atama](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama ekleme

tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:

1.  Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey

6.  Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.

7.  Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.

8.  Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.

9.  Tıklatın **Ekle** button, tooadd Merhaba uygulaması.

Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama için çoklu oturum açmayı yapılandırın

tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Seçin **SAML tabanlı oturum açma** hello gelen **modu** açılır.

9.  Merhaba gerekli değerleri girin **etki alanı ve URL'ler.** Bu değerleri hello uygulama satıcısından almanız gerekir.

   1. SP tarafından başlatılan SSO'yu olarak tooconfigure Merhaba uygulaması hello oturum URL'yi, gerekli bir değerdir. Bazı uygulamalar için hello tanımlayıcısı da gerekli bir değerdir.

   2. IDP tarafından başlatılan SSO'yu olarak tooconfigure Merhaba uygulaması hello yanıt URL'si gerekli bir değerdir. Bazı uygulamalar için hello tanımlayıcısı da gerekli bir değerdir.

10. **İsteğe bağlı:** tıklatın **Göster Gelişmiş URL ayarları** toosee hello gerekli olmayan değer istiyorsanız.

11. Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.

12. **İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

13. tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada. Ayrıca, hello meta verileri URL'leri ve gerekli sertifika toosetup SSO hello uygulamayla sahiptir.

14. tıklatın **kaydetmek** toosave hello yapılandırma.

15. Kullanıcıların toohello uygulama atayın.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin

tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Merhaba uygulaması tooshow burada yedeklemek istediğiniz görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır. Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.

    >[!NOTE]
    >Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello. Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.
    >
    >

9.  tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD meta verileri veya sertifika yükleme

toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri. Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.

    Azure AD, URL tooget hello meta verilerinin sağlamaz. Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon

Galeri olmayan uygulama tooconfigure toohave Azure AD premium gerekir ve Merhaba uygulaması SAML 2.0 destekler. Azure AD sürümleri hakkında daha fazla bilgi için ziyaret [Azure AD fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın](#configuring-single-sign-on)

-   [Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD meta verileri ve sertifika alma](#download-the-azure-ad-metadata-or-certificate)

-   [Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın

tooconfigure çoklu oturum açma hello Azure AD Galerisi'nde olmayan bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey

6.  tıklatın **olmayan galeri uygulama** hello içinde **kendi uygulama Ekle** bölümü

7.  Merhaba Merhaba uygulaması hello adını **adı** metin kutusu.

8.  Tıklatın **Ekle** button, tooadd Merhaba uygulaması.

9.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

10. Seçin **SAML tabanlı oturum açma** hello içinde **modu** açılır

11. Merhaba gerekli değerleri girin **etki alanı ve URL'ler.** Bu değerleri hello uygulama satıcısından almanız gerekir.

  1. IDP tarafından başlatılan SSO'yu olarak tooconfigure hello uygulama hello yanıt URL'si ve hello tanımlayıcısı girin.

  2. **İsteğe bağlı:** tooconfigure hello uygulama SP tarafından başlatılan SSO'yu olarak hello oturum URL'yi, gerekli bir değerdir.

12. Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.

13. **İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

14. tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada. Ayrıca, Azure AD URL'leri ve hello uygulama için gerekli sertifika sahiptir.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin

tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır. Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.

   >[!NOTE]
   >Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello. Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.
   >
   >

9.  tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1'ı **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2 tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD meta verileri veya sertifika yükleme

toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri. Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.

    Azure AD, URL tooget hello meta verilerinin sağlamaz. Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Hello Azure AD Galeriden bir uygulama ekleme](#add-an-application)

-   [Merhaba uygulaması parola çoklu oturum açma için yapılandırma](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama ekleme

tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:

1.  Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey

6.  Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı

7.  Tooconfigure için çoklu oturum açmayı hello uygulamasını seçin

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

9.  Kullanıcıların toohello uygulama atayın.

10. Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme. Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Bir galeri olmayan uygulama ekleme](#add-a-non-gallery-application)

-   [Merhaba uygulaması parola çoklu oturum açma için yapılandırma](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Bir galeri olmayan uygulama ekleme

tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:

1.  Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey

6.  tıklatın **olmayan galeri uygulaması.**

7.  Merhaba, uygulamanızın hello adını **adı** metin kutusu. Seçin **ekleyin.**

Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Merhaba uygulaması parola çoklu oturum açma için yapılandırma

tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

 * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Select hello modu **parola tabanlı oturum açma.**

9.  Merhaba girin **oturum açma URL'si**. Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir. Merhaba oturum alanları hello URL'de göründüğünden emin olun.

10. Kullanıcıların toohello uygulama atayın.

11. Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme. Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan

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

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Sorun giderme adımları değil hello varsa hello sorunu çözün

bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:

-   Bağıntı hata kimliği

-   UPN (kullanıcı e-posta adresi)

-   Tenantıd

-   Tarayıcı türü

-   Saat dilimi ve saat/zaman çerçevesine hata oluşuyor

-   Fiddler izlemeleri

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)

