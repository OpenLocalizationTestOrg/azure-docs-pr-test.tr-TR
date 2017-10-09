---
title: "Öğretici: Azure Active Directory Tümleştirme ile Ceridian Dayforce HCM | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Ceridian Dayforce HCM arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a>Öğretici: Azure Active Directory Tümleştirme Ceridian Dayforce HCM ile

Bu öğreticide, bilgi nasıl toointegrate Ceridian Dayforce HCM Azure Active Directory'ye (Azure AD).

Ceridian Dayforce HCM Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooCeridian Dayforce HCM sahip Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooCeridian Dayforce HCM (çoklu oturum açma) etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Ceridian Dayforce HCM ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Ceridian Dayforce HCM çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Ceridian Dayforce HCM ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a>Merhaba Galerisi'nden Ceridian Dayforce HCM ekleme
Azure AD'ye tooconfigure hello tümleştirme Ceridian Dayforce HCM, tooadd Ceridian Dayforce HCM hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Ceridian Dayforce HCM hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Ceridian Dayforce HCM**seçin **Ceridian Dayforce HCM** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Ceridian Dayforce HCM hello sonuçları listesinde](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Ceridian Dayforce "Britta Simon" adlı bir test kullanıcı tabanlı HCM ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Ceridian Dayforce HCM içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Ceridian Dayforce HCM hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Ceridian Dayforce HCM içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Ceridian Dayforce HCM ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Ceridian Dayforce HCM test kullanıcısı oluşturma](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Ceridian Dayforce HCM içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Ceridian Dayforce HCM uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Ceridian Dayforce HCM ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Ceridian Dayforce HCM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. Merhaba üzerinde **Ceridian Dayforce HCM etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü hello URL, kullanıcıların toosign üzerinde tooyour tarafından Ceridian Dayforce HCM uygulama kullanılır.
    
    | Ortam | URL |
    | :-- | :-- |
    | Üretim için | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | Test için | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    
    | Ortam | URL |
    | :-- | :-- |
    | Üretim için | `https://ncpingfederate.dayforcehcm.com/sp` |
    | Test için | `https://fs-test.dayforcehcm.com/sp` |
    
    c. Merhaba, **yanıt URL'si** metin kutusuna, Azure AD toopost hello yanıt tarafından kullanılan türü hello URL.
    
    | Ortam | URL |
    | :-- | :-- |
    | Üretim için | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | Test için | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Kişi [Ceridian Dayforce HCM istemci destek ekibi](https://www.ceridian.com/contact-us/index.html) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. Ceridian Dayforce HCM uygulamanızı belirli bir biçimde hello SAML onaylar bekliyor. Çalışmak [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html) ilk tooidentify hello doğru kullanıcı tanımlayıcısı. Microsoft önerir hello kullanarak **"name"** kullanıcı tanımlayıcısı olarak özniteliği. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı  | Öznitelik değeri |
    | --------------- | -------------------- |    
    | ad  | User.extensionattribute2 |    

    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba, **değeri** listesi, uygulamanız için kullanmak istediğiniz toouse select hello kullanıcı özniteliği.
    Örneğin, toouse hello benzersiz kullanıcı tanımlayıcısı olarak EmployeeID istiyorsanız ve hello ExtensionAttribute2 hello öznitelik değeri depoladığınız seçip **user.extensionattribute2**.
    
    d. **Tamam**’a tıklayın.

7. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. Merhaba üzerinde **Ceridian Dayforce HCM yapılandırma** 'yi tıklatın **yapılandırma Ceridian Dayforce HCM** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Ceridian Dayforce HCM yapılandırma](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. tooconfigure çoklu oturum açma üzerinde **Ceridian Dayforce HCM** yan, indirilen toosend hello ihtiyacınız **meta veri XML** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html).

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a>Ceridian Dayforce HCM test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Ceridian Dayforce HCM Britta Simon adlı bir kullanıcı var. İş ile Merhaba [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html) tooget kullanıcılar hello Ceridian Dayforce HCM uygulama eklendi. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooCeridian Dayforce HCM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Ceridian Dayforce HCM**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooCeridian Dayforce HCM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Ceridian Dayforce HCM**.

    ![Merhaba Ceridian Dayforce HCM bağlantı hello uygulamalar listesinde](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Merhaba Ceridian Dayforce HCM hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Ceridian Dayforce HCM uygulama almanız gerekir. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

