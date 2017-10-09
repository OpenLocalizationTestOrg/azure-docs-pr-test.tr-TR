---
title: "Öğretici: Azure Active Directory Tümleştirme ile PagerDuty | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PagerDuty arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Öğretici: Azure Active Directory Tümleştirme PagerDuty ile

Bu öğreticide, bilgi nasıl toointegrate PagerDuty Azure Active Directory'ye (Azure AD).

PagerDuty Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooPagerDuty sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooPagerDuty (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure PagerDuty ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir PagerDuty çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden PagerDuty ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-pagerduty-from-hello-gallery"></a>Merhaba Galerisi'nden PagerDuty ekleme
Azure AD'ye tooconfigure hello tümleştirme PagerDuty, tooadd PagerDuty hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd PagerDuty hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **PagerDuty**seçin **PagerDuty** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PagerDuty sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen PagerDuty içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PagerDuty hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri PagerDuty içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve PagerDuty ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[PagerDuty test kullanıcısı oluşturma](#create-a-pagerduty-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir PagerDuty içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma PagerDuty uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile PagerDuty, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **PagerDuty** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. Merhaba üzerinde **PagerDuty etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![PagerDuty etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.pagerduty.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [PagerDuty istemci destek ekibi](https://www.pagerduty.com/support/) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **PagerDuty yapılandırma** 'yi tıklatın **yapılandırma PagerDuty** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![PagerDuty yapılandırma](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. Farklı web tarayıcısı penceresinde Pagerduty şirket sitenize yönetici olarak oturum açın.

8. Hello içinde hello üst menüsünde **hesap ayarlarını**.
   
    ![Hesap ayarları](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "hesap ayarları")

9. Tıklatın **çoklu oturum açma**.
   
    ![Çoklu oturum açma](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "çoklu oturum açma")

10. Merhaba üzerinde **etkinleştirmek çoklu oturum açma (SSO)** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı etkinleştir](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "çoklu oturum açmayı etkinleştir")
   
    a. Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, base-64 kodlanmış sertifikasını açın ve ardından toohello yapıştırın **X.509 sertifikası** metin kutusu
  
    b. Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
  
    c. Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.
 
    d. Seçin **tek oturum açma kapatma**.
 
    e. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-pagerduty-test-user"></a>PagerDuty test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooPagerDuty bunların PagerDuty sağlanması gerekir.  
PagerDuty Hello durumda sağlama bir el ile bir görevdir.

>[!NOTE]
>API, kullanıcı hesaplarını Pagerduty tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer Pagerduty kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Pagerduty** Kiracı.

2. Hello içinde hello üst menüsünde **kullanıcılar**.

3. Tıklatın **kullanıcıları eklemek**.
   
    ![Kullanıcıları ekleme](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "kullanıcı ekleme")

4.  Merhaba üzerinde **ekibinizin davet** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Davet Et ekibinizin](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "ekibinizin davet et")

    a. Türü hello **ilk ve son adı** gibi kullanıcının **Britta Simon**. 
   
    b. Girin **e-posta** kullanıcının adresi ister  **brittasimon@contoso.com** .
   
    c. Tıklatın **Ekle**ve ardından **Gönder başvurulmasını**.
   
    >[!NOTE]
    >Tüm eklenen kullanıcıların davet toocreate PagerDuty hesabı alır.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooPagerDuty vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200]

**tooassign Britta Simon tooPagerDuty hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **PagerDuty**.

    ![Merhaba PagerDuty bağlantı hello uygulamalar listesinde](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Tıkladığınızda hello PagerDuty hello erişim Panelyou parçasında otomatik olarak oturum açma tooyour PagerDuty uygulama almanız gerekir.

Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

