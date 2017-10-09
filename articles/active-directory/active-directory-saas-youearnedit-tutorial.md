---
title: "Öğretici: Azure Active Directory Tümleştirme ile YouEarnedIt | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile YouEarnedIt arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a>Öğretici: Azure Active Directory Tümleştirme YouEarnedIt ile

Bu öğreticide, bilgi nasıl toointegrate YouEarnedIt Azure Active Directory'ye (Azure AD).

YouEarnedIt Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooYouEarnedIt sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooYouEarnedIt (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure YouEarnedIt ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir YouEarnedIt çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden YouEarnedIt ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-youearnedit-from-hello-gallery"></a>Merhaba Galerisi'nden YouEarnedIt ekleme
Azure AD'ye tooconfigure hello tümleştirme YouEarnedIt, tooadd YouEarnedIt hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd YouEarnedIt hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **YouEarnedt**seçin **YouEarnedt** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı YouEarnedIt sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen YouEarnedIt içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı YouEarnedIt hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri YouEarnedIt içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve YouEarnedIt ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[YouEarnedIt test kullanıcısı oluşturma](#create-a-youearnedit-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir YouEarnedIt içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma YouEarnedIt uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile YouEarnedIt, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **YouEarnedIt** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. Merhaba üzerinde **YouEarnedIt etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![YouEarnedIt etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri: 
    | Ortam  | düzeni  |
    |:--- |:--- |
    | Üretim | `https://<company name>.youearnedit.com/users/sign_in` |
    | Korumalı alan  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    b. Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:
    | Ortam  | düzeni  |
    |:--- |:--- |
    | Üretim | `https://<company name>.youearnedit.com` |
    | Korumalı alan  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [YouEarnedIt istemci destek ekibi](https://youearnedit.freshdesk.com/support/tickets/new) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **YouEarnedIt yapılandırma** 'yi tıklatın **yapılandırma YouEarnedIt** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![YouEarnedIt yapılandırma](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **YouEarnedIt** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)** ve **SAML çoklu oturum açma hizmet URL'si** çok[YouEarnedIt destek ekibi](https://youearnedit.freshdesk.com/support/tickets/new). Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-youearnedit-test-user"></a>YouEarnedIt test kullanıcısı oluşturma

Bu bölümde, YouEarnedIt içinde Britta Simon adlı bir kullanıcı oluşturun. Lütfen YouEarnedIt destek team tooadd hello kullanıcıları hello YouEarnedIt Platform çalışırlar.

>[!NOTE]
>YouEarnedIt hello kimlik sağlayıcısı toosupply EmailAddress ya da kullanıcı adı hello NameID özniteliğinde bekler. Karşılık gelen kullanıcı adı veya EmailAddress hello veritabanı içinde bulunamadı veya tam olarak eşleşmiyor kimlik doğrulaması başarısız olur. Bu hesapları hello SSO tümleştirme (genellikle ya da API veya CSV içeri aktarma yoluyla) önce hello YouEarnedIt sistemin içine aktarılması gerektirir.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooYouEarnedIt vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooYouEarnedIt hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **YouEarnedIt**.

    ![Merhaba YouEarnedIt bağlantı hello uygulamalar listesinde](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba YouEarnedIt hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour YouEarnedIt uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

