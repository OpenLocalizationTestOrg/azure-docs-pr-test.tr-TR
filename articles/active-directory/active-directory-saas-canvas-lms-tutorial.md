---
title: "Öğretici: Azure Active Directory Tümleştirme tuvale Lms ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve tuvale LMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a>Öğretici: Tuvale LMS Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate tuvale Azure Active Directory (Azure AD) ile.

Tuvale Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooCanvas sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooCanvas (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure tuvali ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir tuval çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Tuvale hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-canvas-from-hello-gallery"></a>Tuvale hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme tuvalin tooadd tuvale hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd hello galeri tuvalden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **tuvale**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. Merhaba Sonuçlar panelinde seçin **tuvale**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı tuvali ile test etme

Tek toowork'ın oturum açma, Azure AD'de tuvalin hangi hello karşılık gelen kullanıcı tooa kullanıcıdır tooknow Azure AD gerekiyor. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı tuvale hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Tuvalde, hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve tuvali ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Tuvale test kullanıcısı oluşturma](#creating-a-canvas-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir tuvale içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma tuvale uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma tuvali hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **tuvale** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. Merhaba üzerinde **tuvale etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.instructure.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<tenant-name>.instructure.com/saml2`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [tuvale istemci destek ekibi](https://community.canvaslms.com/community/help) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **tuvale yapılandırma** 'yi tıklatın **yapılandırma tuvale** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **değişiklik parola URL'si, Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. Farklı web tarayıcısı penceresinde tooyour tuvale şirket sitede yönetici olarak oturum açın.

8. Çok Git**kurslar \> yönetilen hesapları \> Microsoft**.
   
    ![Tuvale](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "tuvali")

9. Merhaba soldaki Hello Gezinti Bölmesi'nde seçin **kimlik doğrulaması**ve ardından **ekleme yeni SAML Config**.
   
    ![Kimlik doğrulama](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "kimlik doğrulaması")

10. Merhaba geçerli tümleştirme sayfasında hello aşağıdaki adımları gerçekleştirin:
   
    ![Geçerli tümleştirme](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "geçerli tümleştirme")

    a. İçinde **IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.

    b. İçinde **günlük üzerinde URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    c. İçinde **oturum kapatma URL'sini** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.

    d. İçinde **değişiklik parola bağlantısı** metin kutusuna, Yapıştır hello değerini **değişiklik parola URL'si** Azure portalından kopyalanan. 

    e. İçinde **sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.      
        
    f. Merhaba gelen **oturum açma özniteliği** listesinde **NameID**.

    g. Merhaba gelen **tanımlayıcı biçimi** listesinde **emailAddress**.

    h. Tıklatın **kimlik doğrulama ayarlarını Kaydet**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-canvas-test-user"></a>Tuvale test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooCanvas bunlar tuvale sağlanması gerekir.

Tuvale durumunda, kullanıcı sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **tuvale** Kiracı.

2. Çok Git**kurslar \> yönetilen hesapları \> Microsoft**.
   
   ![Tuvale](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "tuvali")

3. **Kullanıcılar**’a tıklayın.
   
   ![Kullanıcıların](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "kullanıcılar")

4. Tıklatın **yeni kullanıcı Ekle**.
   
   ![Kullanıcıların](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "kullanıcılar")

5. Yeni kullanıcı iletişim Sayfa Ekle Hello üzerinde hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı ekleme](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "kullanıcı ekleme")
   
   a. Merhaba, **tam adı** metin kutusuna, bir kullanıcı gibi hello adını girin **BrittaSimon**.

   b. Merhaba, **e-posta** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .

   c. Merhaba, **oturum açma** metin kutusuna, hello kullanıcının Azure AD e-posta adresi gibi girin  **brittasimon@contoso.com** .

   d. Seçin **bu hesap oluşturma hakkında e-posta hello kullanıcı**.

   e. Tıklatın **kullanıcı ekleme**.

>[!NOTE]
>API AAD kullanıcı hesapları tuvale tooprovision tarafından sağlanan veya herhangi diğer tuvale kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooCanvas vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooCanvas hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **tuvale**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Hello tuvale hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour tuvale uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

