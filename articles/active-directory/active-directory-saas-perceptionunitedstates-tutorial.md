---
title: "Öğretici: Azure Active Directory Tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile algısına Amerika Birleşik Devletleri (Non-UltiPro) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Öğretici: Azure Active Directory Tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile

Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile algısına Amerika Birleşik Devletleri (Non-UltiPro).

Algısına Amerika Birleşik Devletleri (Non-UltiPro) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooPerception Amerika Birleşik Devletleri (UltiPro olmayan) sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooPerception Amerika Birleşik Devletleri (Non-UltiPro) (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir algısına Amerika Birleşik Devletleri (Non-UltiPro) çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden algısına Amerika Birleşik Devletleri (Non-UltiPro) ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Merhaba Galerisi'nden algısına Amerika Birleşik Devletleri (Non-UltiPro) ekleme
tooconfigure hello tümleştirmesi algısına Amerika Birleşik Devletleri (UltiPro olmayan), Azure AD'ye hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd algısına Amerika Birleşik Devletleri (Non-UltiPro) gerekir.

**tooadd hello galerisinden algısına Amerika Birleşik Devletleri (Non-UltiPro) hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **algısına Amerika Birleşik Devletleri (Non-UltiPro)**seçin **algısına Amerika Birleşik Devletleri (Non-UltiPro)** sonuç panelinden ardından **Ekle** düğmesi tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde algısına Amerika Birleşik Devletleri (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile algısına "Britta Simon" adlı bir test kullanıcı tabanlı ABD (UltiPro olmayan) test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen algısına Amerika Birleşik Devletleri (Non-UltiPro) içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı algısına Amerika Birleşik Devletleri (Non-UltiPro) içinde arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değerini algısına Amerika Birleşik Devletleri (UltiPro olmayan), Ata **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve test algısına Amerika Birleşik Devletleri (Non-UltiPro) ile Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Algısına Amerika Birleşik Devletleri (Non-UltiPro) test kullanıcısı oluşturma](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave Britta Simon içinde algısına bağlantılı toohello Azure AD kullanıcı gösterimi olan ABD (UltiPro olmayan), karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **algısına Amerika Birleşik Devletleri (Non-UltiPro)** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. Merhaba üzerinde **algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://perception.kanjoya.com/sp`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > Merhaba değeri gerçek değil. Merhaba değeri hello öğreticinin ilerleyen bölümlerinde açıklanan hello gerçek yanıt URL ile güncelleştirir.
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **algısına Amerika Birleşik Devletleri (Non-UltiPro) yapılandırma** 'yi tıklatın **yapılandırma algısına Amerika Birleşik Devletleri (Non-UltiPro)** tooopen **yapılandırma oturum açma** penceresini açın. Kopya hello **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**

    a. Merhaba **algısına Amerika Birleşik Devletleri (Non-UltiPro)** uygulama gerektirir hello **SAML varlık kimliği** kopyaladığınız, değer toobe URI kodlanmış. tooget hello kodlanmış URI değeri, kullanım hello aşağıdaki bağlantıda:**http://www.url-encode-decode.com/**.

    b. Merhaba URI edindikten sonra kodlanmış değeri birleştirmek, ile Merhaba **yanıt URL'si** aşağıdaki - belirtildiği gibi

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Merhaba değerinde yukarıda Yapıştır hello **yanıt URL'si** metin kutusuna **algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri** bölümü.

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) yapılandırma](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. Başka bir tarayıcı penceresinde tooyour algısına Amerika Birleşik Devletleri (Non-UltiPro) şirket sitesinde yönetici olarak oturum açın.

8. Merhaba ana araç çubuğunda **hesap ayarlarını**.

    ![Algısına Amerika Birleşik Devletleri (Non-UltiPro) kullanıcı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. Merhaba üzerinde **hesap ayarlarını** sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Algısına Amerika Birleşik Devletleri (Non-UltiPro) kullanıcı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. Merhaba, **şirket adı** metin kutusuna, tür hello hello adını **şirket**.
    
    b. Merhaba, **hesap adı** metin kutusuna, tür hello hello adını **hesap**.

    c. İçinde **varsayılan yanıt-tooEmail** metin kutusu, geçerli tür hello **e-posta**.

    d. Seçin **SSO kimlik sağlayıcısı** olarak **SAML 2.0**.

10. Merhaba üzerinde **SSO yapılandırma** sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Seçin **SAML NameID türü** olarak **e-posta**.

    b. Merhaba, **SSO yapılandırma adı** metin kutusuna, tür hello adını, **yapılandırma**.
    
    c. İçinde **kimlik sağlayıcı adı** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan. 

    d. İçinde **SAML etki alanı metin kutusu**, gibi hello etki alanını girin  **@contoso.com** .

    e. Tıklayın **yeniden karşıya** tooupload hello **meta veri XML** dosya.

    f. Tıklatın **güncelleştirme**.


> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Algısına Amerika Birleşik Devletleri (Non-UltiPro) test kullanıcısı oluşturma

Bu bölümde, Britta Simon algısına Amerika Birleşik Devletleri (Non-UltiPro) adlı bir kullanıcı oluşturun. Çalışmak [algısına Amerika Birleşik Devletleri (Non-UltiPro) destek ekibi](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello kullanıcılar hello algısına Amerika Birleşik Devletleri (Non-UltiPro) Platform.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooPerception Amerika Birleşik Devletleri (Non-UltiPro) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooPerception Amerika Birleşik Devletleri (Non-UltiPro) hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **algısına Amerika Birleşik Devletleri (Non-UltiPro)**.

    ![Merhaba uygulamalar listesinde Hello algısına Amerika Birleşik Devletleri (Non-UltiPro) bağlantısı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba algısına Amerika Birleşik Devletleri (Non-UltiPro) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma algısına Amerika Birleşik Devletleri (UltiPro olmayan) uygulama tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

