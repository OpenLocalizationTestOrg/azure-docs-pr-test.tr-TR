---
title: "Öğretici: Azure Active Directory Tümleştirme Symantec Web güvenlik hizmetini (WSS) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Symantec Web güvenlik hizmetini (WSS) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Öğretici: Azure Active Directory Tümleştirme Symantec Web güvenlik hizmetini (WSS)

Bu öğreticide, WSS hello Azure AD sağlanan bir son kullanıcı doğrulanabilmesi toointegrate Azure Active Directory (Azure AD) hesabınızla, Symantec Web güvenlik hizmetini (WSS) nasıl hesap öğreneceksiniz SAML kimlik doğrulaması kullanarak ve kullanıcı zorunlu veya grubu düzeyi ilkesi kuralları.

Symantec Web güvenlik hizmetini (WSS) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Tüm hello son kullanıcılar ve gruplar WSS hesabınızdan, Azure AD portalı tarafından kullanılan yönetin. 

- Merhaba son kullanıcıların tooauthenticate kendilerini Azure AD kimlik bilgilerini kullanarak WSS içindeki izin verir.

- Kullanıcının Hello zorlama etkinleştirmek ve WSS hesabınızda tanımlanan düzeyi ilke kuralları gruplayın.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Symantec Web güvenlik hizmetini (WSS) tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Symantec Web güvenlik hizmetini (WSS) hesabı

> [!NOTE]
> tootest hello bu öğreticideki adımlar, üretim amaç için kullanılmakta olan bir WSS hesabı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, şu anda bu test için üretim amaçla kullanılan WSS hesabınızı kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD hesabınızda tanımlanan hello son kullanıcı kimlik bilgilerini kullanarak, Azure AD tooenable tek oturum açma tooWSS yapılandırır.
Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Hello Symantec Web güvenlik hizmetini (WSS) uygulama ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Merhaba Galerisi'nden Symantec Web güvenlik hizmetini (WSS) ekleme
tooconfigure hello tümleştirmeye Symantec Web güvenlik hizmetini (WSS) Azure AD, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Symantec Web güvenlik hizmetini (WSS) gerekir.

**tooadd hello galerisinden Symantec Web güvenlik hizmetini (WSS) hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Symantec Web güvenlik hizmetini (WSS)**seçin **Symantec Web güvenlik hizmetini (WSS)** sonuç panelinden ardından **Ekle** düğmesini tooadd hello uygulama.

    ![Merhaba sonuçları listesinde Symantec Web güvenlik hizmetini (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Symantec Web güvenlik hizmeti ("Britta Simon" adlı bir test kullanıcı tabanlı WSS) test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Symantec Web güvenlik hizmetini (WSS) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Symantec Web güvenlik hizmetini (WSS) arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Symantec Web güvenlik hizmetini (WSS) içindeki hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve test Symantec Web güvenlik hizmetini (WSS) Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Symantec Web güvenlik hizmetini (WSS) test kullanıcısı oluşturma](#create-a-symantec-web-security-service-wss-test-user)**  -toohave karşılık gelen, Britta Simon Symantec Web güvenlik hizmetini (WSS), kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Symantec Web güvenlik hizmetini (WSS) uygulamanızda yapılandırın.

**tooconfigure Symantec Web güvenlik hizmetini (WSS) ile Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Symantec Web güvenlik hizmetini (WSS)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. Merhaba üzerinde **Symantec Web güvenlik hizmetini (WSS) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Symantec Web güvenlik hizmetini (WSS) etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL'si:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Merhaba temasa [Symantec Web güvenlik hizmetini (WSS) istemci destek ekibi](https://www.symantec.com/contact-us) için hello başlangıç değerleri, **tanımlayıcısı** ve **yanıt URL'si** herhangi bir nedenden dolayı çalışmıyor.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure çoklu oturum açma hello Symantec Web güvenlik hizmetini (WSS) yan üzerinde toohello WSS çevrimiçi belgelerine başvurun. indirilen hello **meta veri XML** dosya hello WSS Portalı'na içeri toobe gerekir. Kişi hello [Symantec Web güvenlik hizmetini (WSS) destek ekibi](https://www.symantec.com/contact-us) hello WSS portal hello yapılandırmasına yardıma ihtiyacınız varsa.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Symantec Web güvenlik hizmetini (WSS) test kullanıcısı oluşturma

Bu bölümde, Britta Simon Symantec Web güvenlik hizmetini (WSS) adlı bir kullanıcı oluşturun. Merhaba karşılık gelen son kullanıcı adı hello WSS Portalı'nda el ile oluşturulabilir veya hello kullanıcıları/grupları (~ 15 dakika) birkaç dakika sonra hello Azure AD'ye eşitlenen toobe toohello WSS Portalı'nda sağlanan bekleyebilirsiniz. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir. kullanılan toobrowse Web siteleri olacaktır hello son kullanıcı makinenin Hello ortak IP adresini de hello Symantec Web güvenlik hizmetini (WSS) Portalı'nda sağlanan toobe gerekir.

> [!NOTE]
> Lütfen [burayı](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget makinenizi ortak IP adresi.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooSymantec Web güvenlik hizmetini (WSS) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooSymantec Web güvenlik hizmetini (WSS) hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Symantec Web güvenlik hizmetini (WSS)**.

    ![Merhaba uygulamalar listesinde Hello Symantec Web güvenlik hizmetini (WSS) bağlantısı](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, WSS hesap toouse yapılandırdığınız göre hello çoklu oturum açma işlevselliğini test edeceksiniz SAML kimlik doğrulaması için Azure AD.

Web tarayıcınızı açın ve sonra da yeniden yönlendirilen toohello Azure oturum açma sayfası olacak toobrowse tooa site çalışırsanız, web tarayıcısı tooproxy trafiği tooWSS yapılandırdıktan sonra. Hello Azure AD (diğer bir deyişle, BrittaSimon) sağlanmış hello test son kullanıcı Hello kimlik bilgilerini girin ve ilişkili parola. Kimlik doğrulaması yapıldıktan sonra seçtiğiniz mümkün toobrowse toohello Web sitesi olması. Kullanıcı olarak BrittaSimon toobrowse toothat site çalıştığınızda hello WSS blok sayfasını görmelisiniz sonra tooa belirli bir siteye gözatma hello WSS yan tooblock BrittaSimon ilke kuralı oluşturmanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

