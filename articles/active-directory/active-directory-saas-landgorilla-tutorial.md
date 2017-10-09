---
title: "Öğretici: Azure Active Directory Tümleştirme kara Gorilla istemcisi ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve kara Gorilla arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a>Öğretici: Azure Active Directory Tümleştirme kara Gorilla istemcisi ile

Bu öğreticide, bilgi nasıl toointegrate kara Gorilla istemci Azure Active Directory'ye (Azure AD).

Kara Gorilla istemci Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLand Gorilla istemci sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooLand Gorilla istemci (çoklu oturum açma) etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Ön koşullar

tooconfigure kara Gorilla istemci ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir kara Gorilla istemci çoklu oturum açma etkin abonelik


> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Kara Gorilla istemci hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-land-gorilla-client-from-hello-gallery"></a>Kara Gorilla istemci hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme kara Gorilla istemcisinin tooadd kara Gorilla istemci hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd kara Gorilla istemci hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **kara Gorilla istemci**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. Merhaba Sonuçlar panelinde seçin **kara Gorilla istemci**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma kara Gorilla "Britta Simon" adlı bir test kullanıcı tabanlı istemci ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen kara Gorilla istemcisinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve kara Gorilla İstemcisi'nde hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** kara Gorilla istemcisinde.

tooconfigure ve kara Gorilla istemcisi ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma sınırlı grubu.
3. **[Bir kara Gorilla test kullanıcısı oluşturma](#creating-a-land-gorilla-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma kara Gorilla istemci uygulamanızı yapılandırın.

**Azure AD çoklu oturum açma tooconfigure kara Gorilla istemcisiyle hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **kara Gorilla istemci** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. Merhaba üzerinde **kara Gorilla istemci etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello birini kullanarak türü başlangıç değeri: 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    b. Merhaba, **yanıt URL'si** metin kutusuna, URL deseni takip hello birini kullanarak bir yazın:

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip. Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz. Kişi [kara Gorilla istemci ekibi](https://www.landgorilla.com/support/) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. tooget SSO yapılandırması tamamlandı kara Gorilla uçtaki kişi, uygulamanız için [kara Gorilla istemci destek ekibi](https://www.landgorilla.com/support/) ve indirilen hello ile verin **"meta veri XML** dosya.


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-a-land-gorilla-test-user"></a>Bir kara Gorilla test kullanıcısı oluşturma

Lütfen çalışmak [kara Gorilla destek ekibi](https://www.landgorilla.com/support/) tooadd hello kullanıcılar hello kara Gorilla Platform.
    
### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooLand Gorilla istemci vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLand Gorilla istemci hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **kara Gorilla istemci**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba kara Gorilla istemci hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma kara Gorilla istemci uygulaması tooyour almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
