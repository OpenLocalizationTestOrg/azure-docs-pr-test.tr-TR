---
title: "Öğretici: Azure Active Directory Tümleştirme ile IBM Kenexa anket Kurumsal | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile IBM Kenexa anket kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Öğretici: Azure Active Directory Tümleştirme ile IBM Kenexa anket Enterprise

Bu öğreticide, bilgi nasıl toointegrate IBM Kenexa anket kuruluş Azure Active Directory'ye (Azure AD).

IBM Kenexa anket kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooIBM Kenexa anket Kurumsal sahip Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına ile çoklu oturum açma (SSO) kullanarak, kullanıcılar tooautomatically oturum açma tooIBM Kenexa anket Kurumsal etkinleştirebilirsiniz.
- Hesaplarınızı tek bir merkezi konumda yönetebilirsiniz: Azure portal hello.

Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak tooknow yazılım hakkında daha fazla bilgi istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

IBM Kenexa anket Kurumsal ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- IBM Kenexa anket Kurumsal SSO etkin abonelik

> [!NOTE]
> Bu öğreticide hello adımları test ettiğinizde, bir üretim ortamında kullanmayın öneririz.

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD SSO bir test ortamında test. Merhaba öğreticide özetlenen hello senaryo iki ana yapı taşlarını oluşur:

* IBM Kenexa anket Kurumsal hello Galerisi'nden ekleme
* Yapılandırma ve Azure AD SSO test etme

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>IBM Kenexa anket Kurumsal hello Galerisi'nden ekleme
Azure AD'ye IBM Kenexa anket Enterprise tooconfigure hello tümleştirme hello galeri tooyour listesinden yönetilen SaaS uygulamaları IBM Kenexa anket Kurumsal ekleyin.

tooadd IBM Kenexa anket Kurumsal hello galerisinden hello aşağıdaki:

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, hello tıklatın **Azure Active Directory** düğmesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. bir uygulama, tooadd tıklatın hello **yeni uygulama** düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **IBM Kenexa anket Kurumsal**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Hello sonuçlar listesinde seçin **IBM Kenexa anket Kurumsal**ve ardından hello **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![IBM Kenexa anket Kurumsal hello sonuçları listesinde](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD SSO IBM Kenexa anket "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı kuruluş ile test etme

SSO toowork için Azure AD, Azure AD'de tooidentify hello IBM Kenexa anket Kurumsal kullanıcı karşılık gelen gerekir. Diğer bir deyişle, Azure AD IBM Kenexa anket kuruluşta bir Azure AD kullanıcısının ve ilgili kullanıcı arasında bir bağlantı ilişkisi oluşturmanız gerekir.

tooestablish hello bağlantı ilişkisi, Ata hello hello değerini **kullanıcı adı** kuruluştaki IBM Kenexa anket hello hello değeri olarak **kullanıcıadı** Azure AD'de.

tooconfigure ve test IBM Kenexa anket Enterprise, tam ile Azure AD SSO hello sonraki iki bölümde yapı taşları hello.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO yapılandırın

Bu bölümdeki hello Azure portalında Azure AD SSO'yu etkinleştirmek ve SSO hello aşağıdakileri yaparak IBM Kenexa anket Kurumsal uygulamanızda yapılandırın:

1. Merhaba hello üzerinde Azure portal'ın **IBM Kenexa anket Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Oturum açma tek bağlantı IBM Kenexa anket Kurumsal yapılandırma][4]

2. Merhaba, **çoklu oturum açma** iletişim kutusunda hello **modu** kutusunda **SAML tabanlı oturum açma** tooenable SSO.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. Merhaba, **IBM Kenexa anket kuruluş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![IBM Kenexa anket kuruluş etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello bir URL türüyle:`https://surveys.kenexa.com/<companycode>`

    b. Merhaba, **yanıt URL'si** metin kutusuna, desen aşağıdaki hello bir URL türüyle:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Merhaba önceki değerleri gerçek değildir. Merhaba gerçek tanımlayıcısı ile güncelleştirin ve URL yanıt. tooobtain hello gerçek değerler, kişi hello [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw).

4. Altında **SAML imzalama sertifikası**, tıklatın **sertifika (Base64)**ve ardından hello sertifika dosya tooyour bilgisayara kaydedin.

    ![Merhaba sertifika (Base64) indirme bağlantısı](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Merhaba IBM Kenexa anket Kurumsal uygulama, tooadd özel öznitelik eşlemeleri toohello yapılandırması, SAML belirteci özniteliklerin gerektiren belirli bir biçimde, tooreceive hello güvenlik onaylar biçimlendirme dili (SAML) onaylar bekliyor. Merhaba hello yanıt hello kullanıcı tanımlayıcısı talebin değeri hello hello Kenexa sistemde yapılandırılmış SSO kimliği eşleşmelidir. toomap kuruluşunuzdaki SSO Internet Veri Birimi Protokolü (IDP) olarak uygun kullanıcı tanımlayıcısı Merhaba, iş ile Merhaba [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw). 

    Varsayılan olarak, Azure AD hello kullanıcı tanımlayıcısı hello kullanıcı asıl adı (UPN) değeri olarak ayarlar. Merhaba bu değeri değiştirebilirsiniz **özniteliği** sekmesinde, aşağıdaki ekran görüntüsü hello gösterildiği gibi. yalnızca doğru eşleme hello tamamladıktan sonra hello tümleştirme çalışır.
    
    ![Merhaba kullanıcı öznitelikleri iletişim kutusu](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. **Kaydet** düğmesine tıklayın.

    ![Merhaba yapılandırma çoklu oturum açma düğmesi Kaydet](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. tooopen hello **yapılandırma oturum açma** penceresi altında **IBM Kenexa anket Kurumsal yapılandırma**, tıklatın **IBM Kenexa anket Kurumsal yapılandırma**. 
 
    ![Merhaba IBM Kenexa anket Kurumsal yapılandırma bağlantısı](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Kopya hello **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** hello değerlerinden **hızlı başvuru** bölümü.

8. Merhaba, **yapılandırma oturum açma** penceresi altında **hızlı başvuru**, kopya hello **Sign-Out URL**, **SAML varlık kimliği**, ve  **SAML çoklu oturum açma hizmet URL'si** değerleri.

9. tooconfigure SSO hello üzerinde **IBM Kenexa anket Kurumsal** tarafı, indirilen hello Gönder **sertifika (Base64)**, **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** toohello değerleri [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Merhaba Bu yönergelerde kısa sürümü tooa başvurabilir [Azure portal](https://portal.azure.com) hello uygulaması kuruluyor sırada. Hello hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesini tıklatın ve ardından erişim Merhaba katıştırılmış hello aracılığıyla belgelere **yapılandırma** hello sonunda bölüm. toolearn hello embedded belgeler özelliği hakkında daha fazla bilgi görmek [Azure AD embedded belgeler](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde, test kullanıcı Britta Simon hello Azure portal hello aşağıdakileri yaparak oluşturun:

![Bir Azure AD test kullanıcısı oluşturma][100]

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>IBM Kenexa anket Kurumsal test kullanıcısı oluşturma

Bu bölümde, IBM Kenexa anket kuruluşta Britta Simon adlı bir kullanıcı oluşturun. 

toocreate kullanıcılar hello IBM Kenexa anket Enterprise sistemi ve bunlar için harita hello SSO kimliği ile Merhaba çalışabilir [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw). Bu SSO kimlik değeri ayrıca olmalıdır toohello kullanıcı tanımlayıcısı değeri Azure AD'den eşlenmiş. Merhaba bu varsayılan ayarı değiştirebilirsiniz **özniteliği** sekmesi.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, kullanıcı Britta Simon toouse Azure SSO erişimi tooIBM Kenexa anket Kurumsal vererek etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

tooassign kullanıcı Britta Simon tooIBM Kenexa anket Kurumsal hello aşağıdaki:

1. Hello Azure portal, hello açın **uygulamaları** görüntülemek için Git toohello **dizin** görünümü, select **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Merhaba "Kurumsal uygulamalar" ve "Tüm uygulamaları" bağlantılar][201] 

2. Merhaba, **uygulamaları** listesinde **IBM Kenexa anket Kurumsal**.

    ![Merhaba IBM Kenexa anket Kurumsal bağlantı hello uygulamalar listesinde](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. Merhaba sol bölmede **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. Merhaba tıklatın **Ekle** düğmesine ve ardından hello **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.

    ![Merhaba eklemek atama bölmesi][203]

5. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinde **Britta Simon**.

6. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda, hello **seçin** düğmesi.

7. Merhaba, **eklemek atama** iletişim hello kutusunda, **atamak** düğmesi.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.

Merhaba tıkladığınızda **IBM Kenexa anket Kurumsal** parçasında Merhaba erişim paneli, tooyour IBM Kenexa anket Kurumsal uygulama otomatik olarak imzalanmış.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
