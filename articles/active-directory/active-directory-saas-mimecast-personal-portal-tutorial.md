---
title: "Öğretici: Azure Active Directory Tümleştirme Mimecast kişisel portalıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mimecast kişisel Portal arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>Öğretici: Azure Active Directory Tümleştirme Mimecast kişisel portalı ile

Bu öğreticide, bilgi nasıl toointegrate Mimecast kişisel Portal ile Azure Active Directory (Azure AD).

Mimecast kişisel Portal Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooMimecast kişisel Portal olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooMimecast (çoklu oturum açma) kişisel Portal etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Mimecast kişisel Portal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Mimecast kişisel Portal çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Mimecast kişisel Portal ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>Merhaba Galerisi'nden Mimecast kişisel Portal ekleme
Azure AD'ye tooconfigure hello tümleştirme Mimecast kişisel portalı tooadd Mimecast kişisel Portal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Mimecast kişisel Portal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Mimecast kişisel Portal**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. Merhaba Sonuçlar panelinde seçin **Mimecast kişisel Portal**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Mimecast kişisel "Britta Simon" adlı bir test kullanıcı tabanlı Portal ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Mimecast kişisel portalında tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Mimecast kişisel portalında hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Mimecast kişisel portalında atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Mimecast kişisel Portal ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Mimecast kişisel Portal test kullanıcısı oluşturma](#creating-a-mimecast-personal-portal-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Mimecast kişisel Portalı'nda, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mimecast kişisel portalı uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Mimecast kişisel portalıyla hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Mimecast kişisel Portal** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. Merhaba üzerinde **Mimecast kişisel Portal etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Mimecast kişisel Portal istemci destek ekibi](https://www.mimecast.com/customer-success/technical-support/) tooget bu değerleri. 
 


4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Mimecast kişisel Portal Yapılandırması** 'yi tıklatın **Mimecast kişisel Portal Yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. Farklı web tarayıcısı penceresinde Mimecast kişisel portalınızı bir yönetici olarak oturum.

8. Çok Git**Hizmetleri \> uygulamaları**.
   
    ![Uygulamaları](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "uygulamalar")

9. Tıklatın **kimlik doğrulaması profilleri**.
   
    ![Kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "kimlik doğrulaması profilleri")

10. Tıklatın **yeni kimlik doğrulama profili**.
   
    ![Yeni kimlik doğrulama profili](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "yeni kimlik doğrulama profili")

11. Merhaba, **kimlik doğrulama profili** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kimlik doğrulama profili](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "kimlik doğrulama profili")
   
    a. Merhaba, **açıklama** metin kutusuna, yapılandırmanız için bir ad yazın.
   
    b. Seçin **Mimecast kişisel portalı SAML kimlik doğrulaması zorunlu**.
   
    c. Olarak **sağlayıcı**seçin **Azure Active Directory**.
   
    d. İçinde **veren URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.
   
    e. İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
   
    f. İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.

    g. Açık, **base-64** kodlanmış sertifika Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde ve toohello yapıştırın **kimlik sağlayıcısı sertifikası (meta verileri)** metin kutusu.

    h. Seçin **çoklu oturum açmaya izin verme**.
   
    ı. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>Mimecast kişisel Portal test kullanıcısı oluşturma

Mimecast kişisel Portal içine sipariş tooenable Azure AD kullanıcıların toolog bunlar Mimecast kişisel portalına sağlanmalıdır. Mimecast kişisel Portal Hello durumda sağlama bir el ile bir görevdir.

Kullanıcıların oluşturabilmeniz için önce tooregister bir etki alanı gerekir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. Tooyour üzerinde oturum **Mimecast kişisel Portal** yönetici olarak.

2. Çok Git**dizinleri \> dahili**.
   
    ![Dizinleri](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "dizinleri")

3. Tıklatın **kayıt yeni bir etki alanı**.
   
    ![Yeni etki alanı kayıt](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "kayıt yeni bir etki alanı")

4. Yeni etki alanınızın oluşturulduktan sonra tıklatın **yeni adresi**.
   
    ![Yeni bir adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "yeni adresi")

5. Merhaba yeni adresi iletişim kutusunda, aşağıdaki adımları geçerli Azure hello gerçekleştirmek tooprovision istediğiniz AD hesabı:
   
    ![Kaydet](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Kaydet")
   
    a. Merhaba, **e-posta adresi** metin kutusuna, türü **e-posta adresi** hello kullanıcı  **BrittaSimon@contoso.com** .
    
    b. Merhaba, **genel adı** metin kutusuna, türü hello **kullanıcıadı** olarak **BrittaSimon**.

    c. Merhaba, **parola**, ve **parolayı onayla** metin kutuları, türü hello **parola** hello kullanıcı.
   
    b. **Kaydet** düğmesine tıklayın.

>[!NOTE]
>Herhangi bir Mimecast kişisel Portal kullanıcı hesabı oluşturma araçlarını veya Mimecast kişisel Portal tooprovision Azure AD kullanıcı hesapları tarafından sağlanan API'leri kullanabilirsiniz. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooMimecast kişisel Portal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooMimecast kişisel Portal hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Mimecast kişisel Portal**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme
Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Mimecast kişisel Portal hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Mimecast kişisel Portal uygulama almanız gerekir. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

