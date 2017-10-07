---
title: "Öğretici: Azure Active Directory Tümleştirme Tangoe komutu Premium Mobile ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Tangoe komutu Premium mobil arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>Öğretici: Azure Active Directory Tümleştirme Tangoe komutu Premium Mobile ile

Bu öğreticide, bilgi nasıl toointegrate Tangoe komutu Premium mobil Azure Active Directory'ye (Azure AD).

Tangoe komutu Premium mobil Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooTangoe komutu Premium mobil sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooTangoe komutu Premium mobil (çoklu oturum açma) etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Tangoe komutu Premium Mobile ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Tangoe komutu Premium mobil çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Tangoe komutu Premium mobil ekleme
2. Yapılandırma ve Azure AD çoklu oturum açmayı test etme

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>Merhaba Galerisi'nden Tangoe komutu Premium mobil ekleme
Azure AD'ye tooconfigure hello tümleştirme Tangoe komutu Premium Mobile tooadd Tangoe komutu Premium mobil hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Tangoe komutu Premium mobil hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Tangoe komutu Premium mobil**seçin **Tangoe komutu Premium mobil** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Tangoe komutu Premium mobil Galerisi'nden ekleme ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tangoe komutu Premium "Britta Simon" adlı bir test kullanıcı tabanlı Mobile ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Tangoe komutu Premium Mobile'da tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Tangoe komutu Premium Mobile'da hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Tangoe komutu Premium Mobile'da atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Tangoe komutu Premium Mobile ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Tangoe komutu Premium mobil test kullanıcısı oluşturma](#create-a-tangoe-command-premium-mobile-test-user) ** -toohave Britta Simon Mobile'da Tangoe komutu Premium bağlantılı toohello Azure AD kullanıcı gösterimi olan, karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Tangoe komutu Premium mobil uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Tangoe komutu Premium Mobile ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Tangoe komutu Premium mobil** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. Merhaba üzerinde **Tangoe komutu Premium mobil etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Tangoe komutu Premium mobil etki alanı ve URL'leri](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin. Kişi [Tangoe komutu Premium mobil istemci destek ekibi](https://www.tangoe.com/contact-2/) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Kaydet düğmesi](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. Merhaba üzerinde **Tangoe komutu Premium mobil yapılandırma** 'yi tıklatın **yapılandırma Tangoe komutu Premium mobil** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Tangoe komutu Premium mobil yapılandırma bölümü](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget SSO yapılandırılmış uygulamanızın, kişi, [Tangoe komutu Premium mobil istemci destek ekibi](https://www.tangoe.com/contact-2/) ve hello şunları sağlar:

   - Merhaba indirilen meta veri dosyası
   - Merhaba **SAML varlık kimliği**
   - Merhaba **SAML çoklu oturum açma hizmet URL'si**
   - Merhaba **Sign-Out URL'si**

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Kullanıcıların ve grupların tüm kullanıcılar ->](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Kullanıcı ekle](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>Tangoe komutu Premium mobil test kullanıcısı oluşturma

Bu bölümde, Britta Simon Tangoe komutu Premium Mobile'da adlı bir kullanıcı oluşturun. 

Çoklu oturum açma işleminden önce hello uygulamada sağlanan tüm hello kullanıcılar toobe Tangoe komutu Premium mobil uygulama gerekir. İş, bu nedenle Lütfen hello ile [Tangoe komutu Premium mobil istemci destek ekibi](https://www.tangoe.com/contact-2/) tooprovision bu kullanıcılar hello uygulamaya. 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooTangoe komutu Premium mobil vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooTangoe komutu Premium mobil hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Tangoe komutu Premium mobil**.

    ![Tangoe komutu Premium mobil uygulama listesinde](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.

Merhaba Tangoe komutu Premium mobil hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma Tangoe komutu Premium mobil uygulama tooyour almanız gerekir. Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

