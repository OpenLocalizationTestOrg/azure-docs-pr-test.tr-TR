---
title: "Öğretici: Azure Active Directory Tümleştirme ile öğesine | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasında ve öğesine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a>Öğretici: Azure Active Directory Tümleştirme ile özelliği

Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) öğesine sahip.

Yani Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooNamely sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooNamely (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Yani, sizinle tooconfigure Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir öğesine çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Yani hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-namely-from-hello-gallery"></a>Yani hello Galerisi'nden ekleme
tooconfigure hello tümleştirilmesi, yani Azure AD, yani listesinden hello galeri tooyour yönetilen SaaS uygulamaları tooadd gerekir.

**Yani Galerisi'nden hello tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **öğesine**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. Merhaba Sonuçlar panelinde seçin **öğesine**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile "Britta Simon" adlı bir test kullanıcı öğesine göre test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen, yani tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı arasındaki bağlantıyı ilişki öğesine kurulan toobe gerekir.

Yani, hello hello değeri olarak atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açmayı test adlı, sizinle yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Oluşturma bir öğesine test kullanıcısı](#creating-a-namely-test-user)**  -toohave bir Britta Simon karşılık gelen adlı başka bir deyişle bağlantılı toohello Azure AD kullanıcı gösterimini içinde.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirmek ve çoklu oturum açma, yani uygulama yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile öğesine, gerçekleştirme adımları izleyerek hello:**

1. Merhaba hello üzerinde Azure portal'ın **öğesine** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. Merhaba üzerinde **adlı etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.namely.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.namely.com/saml/metadata`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [öğesine istemci destek ekibi](https://www.namely.com/contact/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **öğesine yapılandırma** 'yi tıklatın **öğesine yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. Başka bir tarayıcı penceresinde tooyour üzerinde öğesine şirket site yönetici olarak oturum açın.

8. Merhaba üstte Hello araç çubuğunda **şirket**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. Merhaba tıklatın **ayarları** sekmesi.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. Tıklatın **SAML**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. Merhaba üzerinde **SAML ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    a. Tıklatın **etkinleştirmek SAML**. 

    b. Merhaba, **kimlik sağlayıcısı SSO URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.
    
    c. İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **kimlik sağlayıcısı sertifikası** metin kutusu.
     
    d. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-namely-test-user"></a>Oluşturma bir öğesine test kullanıcısı

Bu bölümde Hello amacı toocreate Britta Simon öğesine adlı bir kullanıcı var.

**toocreate Britta Simon öğesine, adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Oturum açma tooyour yönetici olarak öğesine site şirket.

2. Merhaba üstte Hello araç çubuğunda **kişiler**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. Merhaba tıklatın **Directory** sekmesi.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. Tıklatın **yeni bir kişiye eklemek**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. Merhaba üzerinde **Yeni Kişi Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    a. Merhaba, **ad** metin kutusuna, türü **Britta**.

    b. Merhaba, **Soyadı** metin kutusuna, türü **Simon**.

    c. Merhaba, **e-posta** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    d. **Kaydet** düğmesine tıklayın.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooNamely vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooNamely hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **öğesine**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba tıklattığınızda öğesine hello erişim paneli döşeme, otomatik olarak oturum açma tooyour öğesine uygulama almanız gerekir

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

