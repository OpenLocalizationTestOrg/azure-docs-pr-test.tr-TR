---
title: "Öğretici: Azure Active Directory Tümleştirme ile OpsGenie | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile OpsGenie arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a>Öğretici: Azure Active Directory Tümleştirme OpsGenie ile

Bu öğreticide, bilgi nasıl toointegrate OpsGenie Azure Active Directory'ye (Azure AD).

OpsGenie Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooOpsGenie sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooOpsGenie (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure OpsGenie ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir OpsGenie çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden OpsGenie ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-opsgenie-from-hello-gallery"></a>Merhaba Galerisi'nden OpsGenie ekleme
Azure AD'ye tooconfigure hello tümleştirme OpsGenie, tooadd OpsGenie hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd OpsGenie hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **OpsGenie**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. Merhaba Sonuçlar panelinde seçin **OpsGenie**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı OpsGenie sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen OpsGenie içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı OpsGenie hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri OpsGenie içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve OpsGenie ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[OpsGenie test kullanıcısı oluşturma](#creating-a-opsgenie-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir OpsGenie içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma OpsGenie uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile OpsGenie, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **OpsGenie** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. Merhaba üzerinde **OpsGenie etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://app.opsgenie.com/auth/login`

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **OpsGenie yapılandırma** 'yi tıklatın **yapılandırma OpsGenie** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. Başka bir tarayıcı örneği açın ve sonra oturum açma tooOpsGenie yönetici olarak.

8. ' I tıklatın **ayarları**ve ardından hello **çoklu oturum açma** sekmesi.
   
    ![OpsGenie çoklu oturum açma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. SSO, tooenable seçin **etkin**.
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. Merhaba, **sağlayıcı** bölümünde, hello tıklatın **Azure Active Directory** sekmesi.
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. Hello Azure Active Directory iletişim sayfasında hello aşağıdaki adımları gerçekleştirin:
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    a. Yapıştır **tek oturum üzerinde hizmet URL'si**, hello hello Azure portal ' Kopyalanan **SAML 2.0 Endpoint** metin kutusu.
    
    b. İndirilen base-64 kodlanmış sertifika kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve hello yapıştırma **X.500 sertifika** metin kutusu.
    
    c. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-opsgenie-test-user"></a>OpsGenie test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde OpsGenie adlı bir kullanıcı ' dir. 

1. Bir web tarayıcısı penceresinde OpsGenie Kiracı yönetici olarak oturum açın.

2. Tıklayarak tooUsers listesi gidin **kullanıcı** sol panelinde.
   
   ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. Tıklatın **kullanıcı ekleme**.

4. Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
   ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   a. Merhaba, **e-posta** metin kutusuna, Azure Active Directory'de ele BrittaSimon, hello e-posta adresini yazın.
   
   b. Merhaba, **tam adı** metin kutusuna, türü **Britta Simon**.
   
   c. **Kaydet** düğmesine tıklayın. 

>[!NOTE]
>Britta kendi profili ayarlama yönergeleri içeren bir e-posta alır.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooOpsGenie vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooOpsGenie hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **OpsGenie**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba OpsGenie hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour OpsGenie uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

