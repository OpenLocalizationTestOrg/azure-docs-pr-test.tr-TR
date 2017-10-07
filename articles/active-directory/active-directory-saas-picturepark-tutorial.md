---
title: "Öğretici: Azure Active Directory Tümleştirme ile Picturepark | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Picturepark arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Öğretici: Azure Active Directory Tümleştirme Picturepark ile

Bu öğreticide, bilgi nasıl toointegrate Picturepark Azure Active Directory'ye (Azure AD).

Picturepark Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooPicturepark sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooPicturepark (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Picturepark ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Picturepark çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Picturepark ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-picturepark-from-hello-gallery"></a>Merhaba Galerisi'nden Picturepark ekleme
Azure AD'ye tooconfigure hello tümleştirme Picturepark, tooadd Picturepark hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Picturepark hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Picturepark**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. Merhaba Sonuçlar panelinde seçin **Picturepark**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Picturepark sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Picturepark içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Picturepark hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Picturepark içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Picturepark ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Picturepark test kullanıcısı oluşturma](#creating-a-picturepark-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Picturepark içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Picturepark uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Picturepark, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Picturepark** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. Merhaba üzerinde **Picturepark etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.picturepark.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Picturepark istemci destek ekibi](https://picturepark.com/about/contact/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Picturepark yapılandırma** 'yi tıklatın **yapılandırma Picturepark** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. Farklı web tarayıcısı penceresinde Picturepark şirket sitenize yönetici olarak oturum açın.

8. Merhaba üstte Hello araç çubuğunda **Yönetimsel Araçlar**ve ardından **Yönetim Konsolu**.
   
    ![Yönetim Konsolu](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Yönetim Konsolu")

9. Tıklatın **kimlik doğrulaması**ve ardından **kimlik sağlayıcıları**.
   
    ![Kimlik doğrulama](./media/active-directory-saas-picturepark-tutorial/ic795063.png "kimlik doğrulaması")

10. Merhaba, **kimlik sağlayıcı Yapılandırması** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kimlik sağlayıcısı Yapılandırması](./media/active-directory-saas-picturepark-tutorial/ic795064.png "kimlik sağlayıcı yapılandırması")
   
    a. **Ekle**'ye tıklayın.
  
    b. Yapılandırmanız için bir ad yazın.
   
    c. Seçin **varsayılan olarak ayarla**.
   
    d. İçinde **veren URI** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
   
    e. İçinde **güvenilir verenin parmak iziyle** metin kutusuna, Yapıştır hello değerini **parmak izi** kopyalanan **SAML imzalama sertifikası** bölümü. 

11. Tıklatın **JoinDefaultUsersGroup**.

12. tooset hello **Emailaddress** hello özniteliğinde **talep** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` tıklatıp **kaydetmek**.

      ![Yapılandırma](./media/active-directory-saas-picturepark-tutorial/ic795065.png "yapılandırma")

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-picturepark-test-user"></a>Picturepark test kullanıcısı oluşturma

Picturepark içine sipariş tooenable Azure AD kullanıcıların toolog bunların Picturepark sağlanmalıdır. Picturepark Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Picturepark** Kiracı.

2. Merhaba üstte Hello araç çubuğunda **Yönetimsel Araçlar**ve ardından **kullanıcılar**.
   
    ![Kullanıcıların](./media/active-directory-saas-picturepark-tutorial/ic795067.png "kullanıcılar")

3. Merhaba, **kullanıcılara genel bakış** sekmesini tıklatın, **yeni**.
   
    ![Kullanıcı Yönetimi](./media/active-directory-saas-picturepark-tutorial/ic795068.png "kullanıcı yönetimi")

4. Merhaba üzerinde **kullanıcı oluştur** iletişim kutusunda, hello gerçekleştirmek geçerli bir Azure Active Directory kullanıcı adımları izleyerek tooprovision istiyor:
   
    ![Kullanıcı oluşturma](./media/active-directory-saas-picturepark-tutorial/ic795069.png "kullanıcı oluştur")
   
    a. Merhaba, **e-posta adresi** metin kutusuna, türü hello **e-posta adresi** hello kullanıcının  **BrittaSimon@contoso.com** .  
   
    b. Merhaba, **parola** ve **parolayı onayla** metin kutuları, türü hello **parola** BrittaSimon biri. 
   
    c. Merhaba, **ad** metin kutusuna, türü hello **ad** hello kullanıcının **Britta**. 
   
    d. Merhaba, **Soyadı** metin kutusuna, türü hello **Soyadı** hello kullanıcının **Simon**.
   
    e. Merhaba, **şirket** metin kutusuna, türü hello **şirket adı** hello kullanıcı. 
   
    f. Merhaba, **Ülke** metin kutusuna, select hello **Ülke** hello kullanıcı.
  
    g. Merhaba, **ZIP** metin kutusuna, türü hello **posta kodu** hello şehrin.
   
    h. Merhaba, **Şehir** metin kutusuna, türü hello **şehir adı** hello kullanıcı.

    ı. Seçin bir **dil**.
   
    j. **Oluştur**'a tıklayın.

>[!NOTE]
>API'leri, Azure AD kullanıcı hesapları Picturepark tooprovision tarafından sağlanan veya herhangi diğer Picturepark kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooPicturepark vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooPicturepark hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Picturepark**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Picturepark hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Picturepark uygulama almanız gerekir. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

