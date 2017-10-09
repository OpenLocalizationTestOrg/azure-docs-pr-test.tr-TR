---
title: "Öğretici: Azure Active Directory Tümleştirme ile Klue | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Klue arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a>Öğretici: Azure Active Directory Tümleştirme Klue ile

Bu öğreticide, bilgi nasıl toointegrate Klue Azure Active Directory'ye (Azure AD).

Klue Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooKlue sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooKlue (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Klue ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Klue çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Klue ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-klue-from-hello-gallery"></a>Merhaba Galerisi'nden Klue ekleme
Azure AD'ye tooconfigure hello tümleştirme Klue, tooadd Klue hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Klue hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Klue**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. Merhaba Sonuçlar panelinde seçin **Klue**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Klue sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Klue içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Klue hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Klue içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Klue ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Klue test kullanıcısı oluşturma](#creating-a-klue-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Klue içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Klue uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Klue, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Klue** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. Merhaba üzerinde **Klue etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`urn:klue:<Customer ID>`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`

4. Denetleme **Göster Gelişmiş URL ayarları**. Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.klue.com/account/auth/saml/<Customer UUID>/`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek yanıt URL'si, tanımlayıcı ve oturum açma URL'si ile güncelleştirin. Kişi [Klue istemci destek ekibi](mailto:support@klue.com) tooget bu değerleri.

5. Merhaba Klue uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/attribute.png)

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntü önceki hello gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı      | Öznitelik değeri      |
    | ------------------- | -------------------- |
    | ilk_ad          | User.givenName |
    | Soyadı           | User.surname |
    | E-posta               | User.userPrincipalName|
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. **Tamam**’a tıklayın.

7. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. Merhaba üzerinde **Klue yapılandırma** 'yi tıklatın **yapılandırma Klue** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. tooconfigure çoklu oturum açma üzerinde **Klue** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64), SAML çoklu oturum açma hizmet URL'si ve SAML varlık kimliği** çok[Klue destek ekibi](mailto:support@klue.com).

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-klue-test-user"></a>Klue test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde Klue adlı bir kullanıcı ' dir. Klue yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler. Bu bölümde, eylem öğe yok. Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Klue sırasında oluşturulur.

>[!Note]
>El ile bir kullanıcıyla iletişim toocreate gerekiyorsa [Klue destek ekibi](mailto:support@klue.com).

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooKlue vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooKlue hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Klue**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Klue hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Klue uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

