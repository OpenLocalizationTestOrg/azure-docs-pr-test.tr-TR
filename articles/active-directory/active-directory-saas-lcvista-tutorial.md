---
title: "Öğretici: Azure Active Directory Tümleştirme ile LCVista | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LCVista arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a>Öğretici: Azure Active Directory Tümleştirme LCVista ile

Bu öğreticide, bilgi nasıl toointegrate LCVista Azure Active Directory'ye (Azure AD).

LCVista Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLCVista sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooLCVista (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure LCVista ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir LCVista çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden LCVista ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-lcvista-from-hello-gallery"></a>Merhaba Galerisi'nden LCVista ekleme
Azure AD'ye tooconfigure hello tümleştirme LCVista, tooadd LCVista hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd LCVista hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **LCVista**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. Merhaba Sonuçlar panelinde seçin **LCVista**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı LCVista ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen LCVista içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LCVista hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LCVista içinde.

tooconfigure ve LCVista ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[LCVista test kullanıcısı oluşturma](#creating-a-lcvista-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LCVista içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LCVista uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile LCVista, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **LCVista** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. Merhaba üzerinde **LCVista etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.lcvista.com/rainier/login`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.lcvista.com` 
     
    > [!NOTE] 
    > Bu değerler hello gerçek değildir. Bu güncelleştirme tanımlayıcısı ve oturum açma URL'si ile Merhaba gerçek değerler. Kişi [LCVista istemci destek ekibi](https://lcvista.com/contact) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. Merhaba üzerinde **LCVista yapılandırma** 'yi tıklatın **yapılandırma LCVista** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  Üzerinde tooyour LCVista uygulama yönetici olarak oturum açın.

8. Merhaba, **SAML Config** bölümünde, hello denetleyin **etkinleştirmek SAML oturum açma** ve görüntü belirtildiği hello ayrıntılarını girin. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    a. Yapıştır hello **veren URL'si** hello Azure AD'den kopyalanan **varlık kimliği** bölümü. 

    b. Yapıştır hello **çoklu oturum açma hizmet URL'si** hello Azure AD'den kopyalanan **URL** bölümü.

    c. Meta veriler (Azure Portalı'ndan indirilen XML'den), hello değerini kopyalayın **X509Certificate** hello yapıştırın **x509 sertifika** bölümü.

    d. Merhaba, **ad özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.

    e. Merhaba, **son name özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.

    f. Merhaba, **e-posta özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    g. Merhaba, **Username özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    e. Tıklatın **kaydetmek** toosave hello ayarları.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-lcvista-test-user"></a>LCVista test kullanıcısı oluşturma

Bu bölümde, LCVista içinde Britta Simon adlı bir kullanıcı oluşturun. Toocontact gerek [LCVista istemci destek ekibi](https://lcvista.com/contact) hello LCVista uygulama tooadd hello kullanıcılar. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooLCVista vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLCVista hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **LCVista**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin. Merhaba LCVista kutucuğa tıklayın hello erişim paneli, siz olacaksınız tooOrganization oturum açma sayfası yeniden yönlendirildi. Başarılı oturum açma işleminden sonra oturum açma LCVista uygulama tooyour olacaktır. Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

