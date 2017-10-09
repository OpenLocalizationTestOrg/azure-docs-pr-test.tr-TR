---
title: "Öğretici: Azure Active Directory Tümleştirme ile UserEcho | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile UserEcho arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a>Öğretici: Azure Active Directory Tümleştirme UserEcho ile

Bu öğreticide, bilgi nasıl toointegrate UserEcho Azure Active Directory'ye (Azure AD).

UserEcho Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooUserEcho sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooUserEcho (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure UserEcho ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir UserEcho çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden UserEcho ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-userecho-from-hello-gallery"></a>Merhaba Galerisi'nden UserEcho ekleme
Azure AD'ye tooconfigure hello tümleştirme UserEcho, tooadd UserEcho hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd UserEcho hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **UserEcho**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. Merhaba Sonuçlar panelinde seçin **UserEcho**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UserEcho sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen UserEcho içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı UserEcho hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri UserEcho içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve UserEcho ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[UserEcho test kullanıcısı oluşturma](#creating-a-userecho-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir UserEcho içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma UserEcho uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile UserEcho, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **UserEcho** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. Merhaba üzerinde **UserEcho etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.userecho.com/`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.userecho.com/saml/metadata/`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [UserEcho istemci destek ekibi](https://feedback.userecho.com/) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **UserEcho yapılandırma** 'yi tıklatın **yapılandırma UserEcho** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. Başka bir tarayıcı penceresinde tooyour UserEcho şirket sitesinde yönetici olarak oturum açın.

8. Merhaba araç hello üstte, kullanıcı adı tooexpand hello menüsünü tıklatın ve ardından **Kurulum**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. Tıklatın **tümleştirmeler**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. Tıklatın **Web sitesi**ve ardından **çoklu oturum açma (SAML2)**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. Merhaba üzerinde **çoklu oturum açma (SAML)** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    a. Olarak **SAML etkin**seçin **Evet**.
    
    b. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **SAML SSO URL** metin kutusu.
    
    c. Yapıştır **Sign-Out URL**, hello hello Azure portal ' Kopyalanan **uzak logoout URL** metin kutusu.
    
    d. İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **X.509 sertifikası** metin kutusu.
    
    e. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-userecho-test-user"></a>UserEcho test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde UserEcho adlı bir kullanıcı ' dir.

**toocreate UserEcho içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Yönetici olarak oturum açma tooyour UserEcho şirket sitesi.

2. Merhaba araç hello üstte, kullanıcı adı tooexpand hello menüsünü tıklatın ve ardından **Kurulum**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. Tıklatın **kullanıcılar**, tooexpand hello **kullanıcılar** bölümü.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. **Kullanıcılar**’a tıklayın.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. Tıklatın **yeni bir kullanıcı davet**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. Merhaba üzerinde **yeni bir kullanıcı davet** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    a. Merhaba, **adı** metin kutusuna, hello kullanıcı Britta Simon gibi türünün adı.
    
    b.  Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.
    
    c. Tıklatın **davet**.

Davetiye UserEcho kullanarak kendi toostart sağlayan tooBritta gönderilir. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooUserEcho vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooUserEcho hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **UserEcho**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.  

Merhaba UserEcho hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour UserEcho uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

