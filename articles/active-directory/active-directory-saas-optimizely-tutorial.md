---
title: "Öğretici: Azure Active Directory Tümleştirme ile Optimizely | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Optimizely arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a>Öğretici: Azure Active Directory Tümleştirme Optimizely ile

Bu öğreticide, bilgi nasıl toointegrate Optimizely Azure Active Directory'ye (Azure AD).

Optimizely Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooOptimizely sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooOptimizely (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Optimizely ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Optimizely çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Optimizely ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-optimizely-from-hello-gallery"></a>Merhaba Galerisi'nden Optimizely ekleme
Azure AD'ye tooconfigure hello tümleştirme Optimizely, tooadd Optimizely hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Optimizely hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Optimizely**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. Merhaba Sonuçlar panelinde seçin **Optimizely**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Optimizely ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Optimizely içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Optimizely hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Optimizely içinde.

tooconfigure ve Optimizely ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Optimizely test kullanıcısı oluşturma](#creating-an-optimizely-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Optimizely içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Optimizely uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Optimizely, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Optimizely** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. Merhaba üzerinde **Optimizely etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.optimizely.net/<instance name>`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`urn:auth0:optimizely:contoso`

    > [!NOTE] 
    > Bu değerler hello gerçek değildir. Oturum açma hello gerçek URL'si ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcısı ile Merhaba değeri güncelleştirir. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Optimizely yapılandırma** 'yi tıklatın **yapılandırma Optimizely** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **Optimizely** tarafı, Optimizely hesap yöneticinize başvurun ve sağlamak indirilen hello **sertifika (Base64)**, ve **SAML çoklu oturum açma hizmet URL'si** . 

8. Yanıt tooyour e-posta ile Optimizely, hello oturum üzerinde URL'si (SP tarafından başlatılan SSO'yu) ve hello tanımlayıcı (hizmet sağlayıcısı varlık kimliği) değerlerini sağlar.

    a. Kopya hello **SP tarafından başlatılan SSO'yu URL** Optimizely ve hello içine yapıştırma tarafından sağlanan **oturum üzerinde URL'si** metin kutusuna **Optimizely etki alanı ve URL'leri** Azure Portal'daki bölümü 

    b. Kopya hello **hizmet sağlayıcısı varlık kimliği** Optimizely ve hello içine yapıştırma tarafından sağlanan **tanımlayıcısı** metin kutusuna **Optimizely etki alanı ve URL'leri** Azure Portal'daki bölümü 

9. Farklı bir tarayıcı penceresinde oturum açma Optimizely uygulama tooyour.

10. Hesap adı hello üst, sağ alt köşesinde tıklatın ve ardından **hesap ayarlarını**.
   
    ![Azure AD çoklu oturum açma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. Merhaba hesap sekmesinde hello kutuyu **etkinleştirmek SSO** çoklu oturum açma hello içinde altında **genel bakış** bölüm.
   
    ![Azure AD çoklu oturum açma](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. Tıklatın **Kaydet**

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-optimizely-test-user"></a>Bir Optimizely test kullanıcısı oluşturma

Bu bölümde, Optimizely içinde Britta Simon adlı bir kullanıcı oluşturun.

1. Merhaba giriş sayfasında, seçin **ortak** sekmesi.

2. tooadd yeni bir ortak çalışanı toohello projesi tıklatın **yeni bir ortak çalışanı**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. Merhaba e-posta adresini doldurduğunuzda ve bir rol atayın. Tıklatın **davet**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. Bir e-posta davet alırlar. Merhaba e-posta adresini kullanarak toolog içinde tooOptimizely sahiptirler.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooOptimizely vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooOptimizely hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Optimizely**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Optimizely hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Optimizely uygulama almanız gerekir. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

