---
title: "Öğretici: Azure Active Directory Tümleştirme Tableau Online ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Tableau çevrimiçi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Öğretici: Azure Active Directory Tümleştirme Tableau Online ile

Bu öğreticide, bilgi nasıl toointegrate Tableau çevrimiçi Azure Active Directory'ye (Azure AD).

Tableau çevrimiçi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooTableau çevrimiçi olan Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooTableau çevrimiçi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Tableau Online ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Tableau çevrimiçi çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Tableau çevrimiçi hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-tableau-online-from-hello-gallery"></a>Tableau çevrimiçi hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Tableau Online hello galeri tooyour yönetilen SaaS uygulamaları listesinden Tableau çevrimiçi tooadd gerekir.

**tooadd Tableau çevrimiçi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Tableau çevrimiçi**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. Merhaba Sonuçlar panelinde seçin **Tableau çevrimiçi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tableau "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Tableau çevrimiçi tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Tableau çevrimiçi hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Çevrimiçi Tableau'nde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Tableau Online ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Tableau çevrimiçi bir test kullanıcısı oluşturma](#creating-a-tableau-online-test-user)**  -toohave Britta Simon Tableau, kullanıcı bağlantılı toohello Azure AD gösterimidir Online'da, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Tableau çevrimiçi uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Tableau Online ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Tableau çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. Merhaba üzerinde **Tableau çevrimiçi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://sso.online.tableau.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://sso.online.tableau.com/public/sp/<instancename>`

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. Farklı bir tarayıcı penceresinde oturum açma Tableau çevrimiçi uygulama tooyour. Çok Git**ayarları** ve ardından **kimlik doğrulama**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML altında **kimlik doğrulama türleri** bölümü. Merhaba denetleyin **çoklu oturum açma SAML ile** onay kutusu.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Kadar aşağıya kaydırın **alma meta veri dosyasına Tableau çevrimiçi** bölümü.  Gözat'ı tıklatın ve Azure AD'den indirmiş hello meta veri dosyası içeri aktarın. Ardından **Uygula**.
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. Merhaba, **eşleşen onaylar** bölümünde, hello karşılık gelen kimlik sağlayıcısı onaylama adı için INSERT **e-posta adresi**, **ad**, ve **Soyadı** . tooget Azure AD'den bu bilgileri: 
  
    a. İçinde Azure portal Merhaba, üzerinde hello Git **Tableau çevrimiçi** uygulama tümleştirme sayfası.
    
    b. Merhaba öznitelikleri hello bölümünde **"görüntülemek ve diğer tüm kullanıcı öznitelikleri Düzenle"** onay kutusu. 
    
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Merhaba ad alanı değeri bu öznitelikler için kopyalayın: givenname, e-posta ve kullanarak Soyadı hello adımları izleyin:

   ![Azure AD çoklu oturum açma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. Tıklatın **user.givenname** değeri 
    
    e. Hello Hello değerini kopyalayın **ad alanı** metin kutusu.

   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. Merhaba e-posta ve Soyadı toocopy hello namesapce değerleri hello önceki adımları izleyin.

    g. Geçiş toohello Tableau çevrimiçi uygulama sonra ayarlamak hello **çevrimiçi öznitelikleri Tableau** gibi bölümünde:
     * E-posta: **posta** veya **userprincipalname**
     * Ad: **givenname**
     * Soyadı: **Soyadı**
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-tableau-online-test-user"></a>Tableau çevrimiçi bir test kullanıcısı oluşturma

Bu bölümde, Britta Simon Tableau çevrimiçi olarak adlandırılan bir kullanıcı oluşturun.

1. Üzerinde **Tableau çevrimiçi**, tıklatın **ayarları** ve ardından **kimlik doğrulaması** bölümü. Çok ilerleyin**Kullanıcıları Seç** bölümü. Tıklatın **kullanıcıları eklemek** ve ardından **e-posta adreslerini girin**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Seçin **çoklu oturum açma (SSO) kimlik doğrulaması için kullanıcı ekleme**. Merhaba, **e-posta adreslerini girin** textbox ekleyinbritta.simon@contoso.com
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. **Oluştur**'a tıklayın.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, çevrimiçi erişim tooTableau vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign çevrimiçi Britta Simon tooTableau hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Tableau çevrimiçi**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba Tableau çevrimiçi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Tableau çevrimiçi uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

