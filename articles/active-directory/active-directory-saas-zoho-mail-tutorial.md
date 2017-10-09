---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zoho | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zoho arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a>Öğretici: Azure Active Directory Tümleştirme Zoho ile

Bu öğreticide, bilgi nasıl toointegrate Zoho Azure Active Directory'ye (Azure AD).

Zoho Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooZoho sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooZoho (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Zoho ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Zoho çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Zoho ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-zoho-from-hello-gallery"></a>Merhaba Galerisi'nden Zoho ekleme
Azure AD'ye tooconfigure hello tümleştirme Zoho, tooadd Zoho hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Zoho hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Zoho**seçin **Zoho** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zoho sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Zoho içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zoho hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Zoho içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Zoho ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Zoho test kullanıcısı oluşturma](#create-a-zoho-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zoho içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zoho uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Zoho, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Zoho** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. Merhaba üzerinde **Zoho etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Zoho etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.zohomail.com`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Zoho istemci destek ekibi](https://www.zoho.com/mail/contact.html) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Zoho yapılandırma** 'yi tıklatın **yapılandırma Zoho** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, değişiklik parola URL'si ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Zoho yapılandırma](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. Farklı web tarayıcısı penceresinde Zoho posta şirket sitenize yönetici olarak oturum açın.

8. Toohello Git **Denetim Masası**.
   
    ![Denetim Masası](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Denetim Masası")

9. Merhaba tıklatın **SAML kimlik doğrulaması** sekmesi.
   
    ![SAML kimlik doğrulaması](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML kimlik doğrulaması")

10. Merhaba, **SAML kimlik doğrulama ayrıntıları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML kimlik doğrulama ayrıntıları](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML kimlik doğrulama ayrıntıları")
   
    a. Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
   
    b. Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.
   
    c. Merhaba, **değişiklik parola URL'si** metin kutusuna, Yapıştır **değişiklik parola URL'si** Azure portalından kopyalanan.
       
    d. Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, base-64 kodlanmış sertifikasını açın ve ardından toohello yapıştırın **PublicKey** metin kutusu.
   
    e. Olarak **algoritması**seçin **RSA**.
   
    f. **Tamam** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-zoho-test-user"></a>Zoho test kullanıcısı oluşturma

Zoho posta uygulamasına sipariş tooenable Azure AD kullanıcıların toolog bunlar Zoho postaya sağlanmalıdır. Zoho posta Hello durumda sağlama bir el ile bir görevdir.

> [!NOTE]
> API AAD kullanıcı hesaplarının Zoho posta tooprovision tarafından sağlanan veya herhangi diğer Zoho posta kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:

1. İçinde tooyour oturum **Zoho posta** yönetici olarak şirket site.

2. Çok Git**Denetim Masası \> posta & belgeleri**.

3. Çok Git**kullanıcı ayrıntıları \> Kullanıcı Ekle**.
   
    ![Kullanıcı ekleme](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "kullanıcı ekleme")

4. Merhaba üzerinde **kullanıcıları eklemek** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı ekleme](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "kullanıcı ekleme")
   
    a. Merhaba, **ad** metin kutusuna, tür hello ilk gibi kullanıcı adını **Britta**.

    b. Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını gibi **Simon**.

    c. Merhaba, **e-posta kimliği** metin kutusuna, tür hello e-posta gibi kullanıcı kimliğini  **brittasimon@contoso.com** .

    d. Merhaba, **parola** metin kutusu, kullanıcı parolasını girin.
   
    e. **Tamam** düğmesine tıklayın.  
      
    > [!NOTE]
    > etkin duruma gelmesi hello Azure Active Directory hesap sahibi bağlantı tooconfirm hello hesabı olan bir e-posta alırsınız.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooZoho vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooZoho hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Zoho**.

    ![Merhaba Zoho bağlantı hello uygulamalar listesinde](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Zoho hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zoho uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

