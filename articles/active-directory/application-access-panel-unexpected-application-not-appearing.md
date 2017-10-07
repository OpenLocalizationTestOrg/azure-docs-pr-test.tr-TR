---
title: "Merhaba erişim panelinde atanan aaaAn uygulama görünmesini değil | Microsoft Docs"
description: "Bir uygulama hello erişim paneli görünmeyen neden sorun giderme"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a>Atanmış bir uygulama hello erişim panelinde görünmüyor

Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni. Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır. Merhaba uygulaması düzgün şekilde yapılandırılmalıdır ve atanan toohello kullanıcı veya grup hello kullanıcı toosee hello hello erişim paneli uygulamada üyesidir.

bir kullanıcı için görüyor olabilirsiniz uygulamalarının Hello türü kategorileri aşağıdaki hello ayrılır:

-   Office 365 uygulamaları

-   Federasyon tabanlı SSO ile yapılandırılan Microsoft ve üçüncü taraf uygulamalar

-   Parola tabanlı SSO uygulamaları

-   Varolan SSO çözümleriyle uygulamaları

## <a name="general-issues-toocheck-first"></a>Genel toocheck ilk sorunları

-   Bir uygulamayı yalnızca tooa kullanıcı eklendiyse, hello uygulama eklediyseniz toosign içeri ve dışarı yeniden hello kullanıcının erişim paneline sonra birkaç dakika toosee deneyin.

-   Bir lisans yalnızca bir kullanıcı veya grup hello kullanıcı kaldırıldıysa bu üyesi hello boyutu ve karmaşıklığı yapılan değişiklikleri toobe hello grubunun bağlı olarak uzun bir süre devam edebilir ' dir. Erişim paneli hello oturum açmadan önce ek süresi için izin verin.

## <a name="problems-related-tooapplication-configuration"></a>Sorunları ilgili tooapplication yapılandırma

Düzgün yapılandırılmadığından, bir uygulama kullanıcının erişim panelinde görünüyor değil. Aşağıda ilgili tooapplication yapılandırma sorunlarını gidermek için kullanabileceğiniz bazı yöntemler şunlardır:

-   [Azure AD galeri uygulaması için çoklu oturum açmayı tooconfigure nasıl Federasyon](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [Nasıl tooconfigure parola tek oturum açma uygulaması için Azure AD galeri uygulaması](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [Nasıl tooconfigure parola tek oturum açma uygulaması Galerisi olmayan uygulama](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD galeri uygulaması için çoklu oturum açmayı tooconfigure nasıl Federasyon

Kurumsal çoklu oturum açma özelliğine sahip etkin hello Azure AD galerisinde tüm uygulamaları kullanılabilir adım adım öğretici sahiptir. Merhaba erişebilirsiniz [nasıl öğreticiler listesi toointegrate SaaS uygulamaları Azure Active Directory ile](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) ayrıntılı adım adım yönergeler için.

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Hello Azure AD Galeriden bir uygulama ekleme](#add-an-application-from-the-azure-ad-gallery)

-   [Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD meta verileri ve sertifika alma](#download-the-azure-ad-metadata-or-certificate)

-   [Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama ekleme

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

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama için çoklu oturum açmayı yapılandırın

tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

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

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin

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

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki görürsünüz.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD meta verileri veya sertifika yükleme

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

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon

Galeri olmayan uygulama tooconfigure toohave Azure AD premium gerekir ve Merhaba uygulaması SAML 2.0 destekler. Azure AD sürümleri hakkında daha fazla bilgi için ziyaret [Azure AD fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın](#configuring-single-sign-on)

-   [Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD meta verileri ve sertifika alma](#download-the-azure-ad-metadata-or-certificate)

-   [Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın

tooconfigure çoklu oturum açma hello Azure AD Galerisi'nde olmayan bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.

6.  tıklatın **olmayan galeri uygulama** hello içinde **kendi uygulama Ekle** bölümü.

7.  Merhaba Merhaba uygulaması hello adını **adı** metin kutusu.

8.  Tıklatın **Ekle** button, tooadd Merhaba uygulaması.

9.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

10. Seçin **SAML tabanlı oturum açma** hello içinde **modu** açılır.

11. Merhaba gerekli değerleri girin **etki alanı ve URL'ler.** Bu değerleri hello uygulama satıcısından almanız gerekir.

   1. IDP tarafından başlatılan SSO'yu olarak tooconfigure hello uygulama hello yanıt URL'si ve hello tanımlayıcısı girin.

   2.  **İsteğe bağlı:** tooconfigure hello uygulama SP tarafından başlatılan SSO'yu olarak hello oturum URL'yi, gerekli bir değerdir.

12. Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.

13. **İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

14. tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada. Ayrıca, Azure AD URL'leri ve hello uygulama için gerekli sertifika sahiptir.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin

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

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD meta verileri veya sertifika yükleme

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

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Hello Azure AD Galeriden bir uygulama ekleme](#add-an-application-from-the-azure-ad-gallery)

-   [Merhaba uygulaması parola çoklu oturum açma için yapılandırma](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD Galeriden bir uygulama ekleme

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

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Merhaba uygulaması parola çoklu oturum açma için yapılandırma

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

9.  [Kullanıcıların toohello uygulama atama](#how-to-assign-a-user-to-an-application-directly).

10. Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme. Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Bir galeri olmayan uygulama ekleme](#add-a-non-gallery-application)

-   [Merhaba uygulaması parola çoklu oturum açma için yapılandırma](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a>Bir galeri olmayan uygulama ekleme

tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:

1.  Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**.

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.

6.  tıklatın **olmayan galeri uygulaması.**

7.  Merhaba, uygulamanızın hello adını **adı** metin kutusu. Seçin **ekleyin.**

Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Merhaba uygulaması parola çoklu oturum açma için yapılandırma

tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

    1.  Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Select hello modu **parola tabanlı oturum açma.**

9.  Merhaba girin **oturum açma URL'si**. Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir. Merhaba oturum alanları hello URL'de göründüğünden emin olun.

10. [Kullanıcıların toohello uygulama atama](#how-to-assign-a-user-to-an-application-directly).

11. Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme. Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.

## <a name="problems-related-tooassigning-applications-toousers"></a>Sorunları ilgili tooassigning uygulamaları toousers

Toohello uygulama atanmadıkları bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz değil. Bazı yolları toocheck aşağıda verilmiştir:

-   [Bir kullanıcı toohello uygulama atandığından emin olun](#check-if-a-user-is-assigned-to-the-application)

-   [Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan](#how-to-assign-a-user-to-an-application-directly)

-   [Bir kullanıcı tooa lisans atanmışsa onay toohello uygulama ilgili](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [Nasıl tooassign lisans tooa kullanıcı](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a>Bir kullanıcı toohello uygulama atandığından emin olun

toocheck toohello uygulama atanmış bir kullanıcı yoksa, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

6.  **Arama** için söz konusu hello uygulamasının hello adı.

7.  tıklatın **kullanıcılar ve gruplar**.

8.  Kullanıcı toohello uygulama atanmışsa toosee denetleyin.

   * Aksi halde hello adımları "nasıl tooassign bir kullanıcı tooan uygulaması doğrudan" toodo şekilde.

### <a name="how-tooassign-a-user-tooan-application-directly"></a>Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan

tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici**.

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

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Bir kullanıcının bir lisansı altında olup olmadığını denetleyin ilgili toohello uygulama

toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.

  * Merhaba kullanıcı atanan tooan Office lisansı ise bu etkinleştirin birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde.

### <a name="how-tooassign-a-user-a-license"></a>Nasıl tooassign bir kullanıcı bir lisans 

tooassign lisans tooa kullanıcı hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.

8.  Merhaba tıklatın **atamak** düğmesi.

9.  Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.

10. **İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın. Tıklatın **Tamam** ne zaman bu tamamlandı.

11. Merhaba tıklatın **atamak** tooassign bu lisansları toothis kullanıcı düğmesi.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Sorunları ilgili tooassigning uygulamaları toogroups

Merhaba uygulaması atanmış bir grubun parçası olmadığından bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz. Bazı yolları toocheck aşağıda verilmiştir:

-   [Bir kullanıcı grup üyeliklerini denetleyin](#check-a-users-group-memberships)

-   [Tooassign bir uygulama tooa Grup nasıl doğrudan](#how-to-assign-an-application-to-a-group-directly)

-   [Bir kullanıcı grubu tooa lisans atanmış bir parçası olup olmadığını denetleyin](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [Nasıl tooassign lisans tooa grubu](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a>Bir kullanıcı grup üyeliklerini denetleyin

toocheck bir grubun üyeliğini, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **grupları**.

8.  Kullanıcı grubunun bir parçası ise onay toosee toohello uygulama atanır.

  * Merhaba grubundan tooremove hello kullanıcının istiyorsanız **hello satıra tıklayın** hello grubu ve select silin.

### <a name="how-tooassign-an-application-tooa-group-directly"></a>Tooassign bir uygulama tooa Grup nasıl doğrudan

bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici**.

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.

9.  Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.

10. Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.

11. Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**. Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.

12. **İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.

13. Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.

14. **İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.

15. Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.

Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a>Bir kullanıcı grubu tooa lisans atanmış bir parçası olup olmadığını denetleyin

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **grupları**.

8.  belirli bir grup Hello satırının'ı tıklatın.

9.  tıklatın **lisansları** toosee hangi lisansları hello Grup tooit atanan.

   * Merhaba grubu atanan tooan Office lisansı ise bu belirli birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde sağlayabilir.

### <a name="how-tooassign-a-license-tooa-group"></a>Nasıl tooassign lisans tooa grubu

tooassign bir lisans tooa grubu hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm grupları**.

6.  **Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.

8.  Merhaba tıklatın **atamak** düğmesi.

9.  Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.

10. **İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın. Tıklatın **Tamam** ne zaman bu tamamlandı.

11. Merhaba tıklatın **atamak** bu lisansları toothis Grup tooassign düğmesi. Bu, başlangıç boyutu ve karmaşıklığı hello grubunun bağlı olarak uzun bir süre devam edebilir.

>[!NOTE]
>toodo bu daha hızlı ve göz önünde bulundurun geçici olarak bir lisans toohello kullanıcı doğrudan atama. 
>
>

## <a name="next-steps"></a>Sonraki adımlar
[Yeni kullanıcılar tooAzure Active Directory ekleme](active-directory-users-create-azure-portal.md)

