---
title: "Öğretici: Azure Active Directory Tümleştirme ile Cisco Webex | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Cisco Webex nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Öğretici: Cisco Webex Azure Active Directory Tümleştirme
Merhaba amacı Bu öğretici, Azure ve Cisco Webex tooshow hello tümleştirme ' dir.  
Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Cisco Webex Kiracı

Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcılarının atamış Webex olacaktır tooCisco mümkün toosingle oturum hello uygulamasına, Cisco Webex şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) hello veya hello kullanarak [giriş toohello Erişim paneli](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

* Merhaba uygulama tümleştirmesi Cisco Webex için etkinleştirme
* Çoklu oturum açma (SSO) yapılandırma
* Kullanıcı hazırlama işleminin yapılandırılması
* Kullanıcılar atama

![Senaryo](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "senaryosu")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Cisco Webex için Hello uygulama tümleştirmeyi etkinleştir
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Cisco Webex için.

**Cisco Webex için tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
   ![Uygulama ekleme](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
   ![Galeriden bir uygulama eklemek](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **Cisco Webex**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **Cisco Webex**ve ardından **tam** tooadd Merhaba uygulaması.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooCisco Webex temel toooutline ' dir.  

Bu yordam bir parçası, gerekli toocreate base-64 kodlanmış sertifika olur. Bu yordama bilmiyorsanız bkz [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **Cisco Webex** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl kullanıcılar toosign tooCisco Webex üzerinde gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "çoklu oturum açmayı yapılandırın")
3. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**.
   
   ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "uygulama URL'sini yapılandırın")   
   1. Merhaba, **URL SING** metin kutusuna, Cisco Webex Kiracı URL'nizi yazın (örneğin: *http://contoso.webex.com*).
   2. Merhaba, **Cisco Webex yanıt URL'si** metin kutusuna, türü, **Cisco Webex AssertionConsumerService URL** (örn: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. Merhaba üzerinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** sayfası, toodownload, sertifikanızı tıklatın **indirme sertifika**ve hello sertifika dosyayı bilgisayarınıza kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "çoklu oturum açmayı yapılandırın")
5. Farklı web tarayıcısı penceresinde Cisco Webex şirket sitenize yönetici olarak oturum açın.
6. Hello içinde hello üst menüsünde **Site Yönetimi**.
   
   ![Site Yönetimi](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Yönetimi")
7. Merhaba, **sitesi yönetme** 'yi tıklatın **SSO yapılandırma**.
   
   ![SSO yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO yapılandırma")
8. Hello Federe Web SSO yapılandırma bölümü, hello aşağıdaki adımları gerçekleştirin:
   
   ![SSO yapılandırma Federasyon](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federasyon SSO yapılandırma")  
   1. Merhaba gelen **Federasyon Protokolü** listesinde **SAML 2.0**.
   2. Oluşturma bir **Base-64 kodlanmış** indirilen sertifikanızı dosyasından.  
    >[!TIP]
    >Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Base-64 kodlanmış sertifikanızı not defteri sonra bunu içerik kopyalama hello açın.
   4. Tıklatın **SAML meta verileri içeri aktarma**ve ardından, base-64 kodlanmış sertifika yapıştırın.
   5. Hello hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopyalama hello **veren URL'si** değer ve hello yapıştırma **SAML (IDP kimliği)veren** metin kutusu.
   6. Hello hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopyalama hello **uzaktan oturum açma URL'si** değer ve hello yapıştırma **müşteri SSO hizmeti oturum açma URL** metin kutusu.
   7. Merhaba gelen **NameID biçimi** listesinde **e-posta adresi**.
   8. Merhaba, **AuthnContextClassRef** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:ac:classes:Password**.
   9. Hello hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfası, kopyalama hello **uzak oturum kapatma URL'si** değer ve hello yapıştırma **müşteri SSO hizmet oturum kapatma URL** metin kutusu.
   10. Tıklatın **güncelleştirme**.
9. Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Cisco Webex yapılandırma** iletişim sayfa hello tek oturum açma yapılandırması onay seçin ve ardından **tam**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "çoklu oturum açmayı yapılandırın")
   
## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır

Cisco Webex içine sipariş tooenable Azure AD kullanıcıların toolog bunların Cisco Webex sağlanmalıdır.  

* Cisco Webex Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour oturum **Cisco Webex** Kiracı.
2. Çok Git**kullanıcıları yönetme \> Kullanıcı Ekle**.
   
   ![Kullanıcıları ekleme](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "kullanıcı ekleme")
3. Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı Ekle](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Kullanıcı Ekle")   
   1. Olarak **hesap türü**seçin **konak**.
   2. Metin kutuları aşağıdaki hello var olan bir Azure AD kullanıcısının hello bilgilerini yazın: **ad, Soyadı**, **kullanıcı adı**, **e-posta**, **parola**, **Parolayı onaylayın**.
   3. **Ekle**'ye tıklayın.

>[!NOTE]
>API AAD kullanıcı hesapları Cisco Webex tooprovision tarafından sağlanan veya herhangi diğer Cisco Webex kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooCisco Webex, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde **Cisco Webex** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

