---
title: "Öğretici: Azure Active Directory Tümleştirme ile Moxtra | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Moxtra arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Öğretici: Azure Active Directory Tümleştirme Moxtra ile

Bu öğreticide, bilgi nasıl toointegrate Moxtra Azure Active Directory'ye (Azure AD).

Moxtra Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooMoxtra sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooMoxtra (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Moxtra ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Moxtra çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Moxtra ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-moxtra-from-hello-gallery"></a>Merhaba Galerisi'nden Moxtra ekleme
Azure AD'ye tooconfigure hello tümleştirme Moxtra, tooadd Moxtra hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Moxtra hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Moxtra**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. Merhaba Sonuçlar panelinde seçin **Moxtra**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Moxtra sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Moxtra içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Moxtra hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Moxtra içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Moxtra ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Moxtra test kullanıcısı oluşturma](#creating-a-moxtra-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Moxtra içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Moxtra uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Moxtra, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Moxtra** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. Merhaba üzerinde **Moxtra etki alanı ve URL'leri** bölümünde, adım aşağıdaki hello gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://www.moxtra.com/service/#login`

4. Moxtra uygulama hello SAML onaylar belirli bir biçimde bekler. Bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello Bu yapılandırmanın bir örneği gösterir. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ------------------- | -------------------- |    
    | FirstName | User.givenName |
    | Soyadı | User.surname |
    | idpid    | < SAML varlık kimliği > 

    > [!Note]
    > Merhaba değerini **idpid** özniteliği gerçek değil. Merhaba gerçek değerinden alabilirsiniz **hızlı başvuru** altında bölümünde **Moxtra yapılandırma**.
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.

    d. **Tamam**’a tıklayın.
    
5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **Moxtra yapılandırma** 'yi tıklatın **yapılandırma Moxtra** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. Başka bir tarayıcı penceresinde tooyour Moxtra şirket sitesinde yönetici olarak oturum açın.

9. Merhaba soldaki Hello araç çubuğunda **Yönetici Konsolu > SAML çoklu oturum açma**ve ardından **yeni**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. Merhaba üzerinde **SAML** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: *SAML*). 
  
    b. Merhaba, **IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan. 
 
    c. İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan. 
 
    d. Merhaba, **AuthnContextClassRef** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:ac:classes:Password**. 
 
    e. Merhaba, **NameID biçimi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**. 
 
    f. Not Defteri'nde, Azure Portalı'ndan indirilen açık sertifika hello içeriği Kopyala ve hello yapıştırma **sertifika** metin kutusu.    
 
    g. SAML e-posta etki alanınızın Hello SAML e-posta etki alanı metin kutusuna yazın.    
  
    >[!NOTE]
    >toosee hello adımları tooverify hello etki alanı, hello tıklayın "**ı**" altında.

    h. Tıklatın **güncelleştirme**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-moxtra-test-user"></a>Moxtra test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde Moxtra adlı bir kullanıcı ' dir.

**toocreate Moxtra içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Üzerinde tooyour Moxtra şirket site yönetici olarak oturum açın.

2. Merhaba soldaki Hello araç çubuğunda **Yönetici Konsolu > Kullanıcı Yönetimi**ve ardından **Kullanıcı Ekle**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
  
    a. Merhaba, **ad** metin kutusuna, türü **Britta**.
  
    b. Merhaba, **Soyadı** metin kutusuna, türü **Simon**.
  
    c. Merhaba, **e-posta** metin kutusuna, Britta'nın e-posta adresi ile aynı Azure Portal'da türü.
  
    d. Merhaba, **bölme** metin kutusuna, türü **geliştirme**.
  
    e. Merhaba, **departmanı** metin kutusuna, türü **BT**.
  
    f. Seçin **yönetici**.
  
    g. **Ekle**'ye tıklayın.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooMoxtra vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooMoxtra hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Moxtra**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Moxtra hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Moxtra uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

