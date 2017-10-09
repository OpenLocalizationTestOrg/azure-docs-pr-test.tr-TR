---
title: "Öğretici: Azure Active Directory Tümleştirme Predictix Sınıflama planlama | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki Sınıflama Predictix planlama."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1294b712caf12fdafaf65d70a02ee9fbdc3e84a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a>Öğretici: Azure Active Directory Tümleştirme Sınıflama Predictix planlama

Bu öğreticide, bilgi nasıl toointegrate Predictix Sınıflama planlama Azure Active Directory'ye (Azure AD).

Azure AD ile tümleştirme Predictix Sınıflama planlama ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooPredictix Sınıflama planlama sahip Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooPredictix Sınıflama planlama (çoklu oturum açma) etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Predictix Sınıflama planlama ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Predictix Sınıflama planlama çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Sınıflama Predictix planlama hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-predictix-assortment-planning-from-hello-gallery"></a>Sınıflama Predictix planlama hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Predictix Sınıflama planlama tooadd Predictix Sınıflama planlama hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Predictix Sınıflama planlama hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Predictix Sınıflama planlama**seçin **Predictix Sınıflama planlama** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Sınıflama Predictix planlama hello sonuçları listesinde](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Sınıflama Predictix planlama ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Predictix Sınıflama planlama tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Predictix Sınıflama planlama hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Sınıflama Predictix planlamada hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Predictix Sınıflama planlama ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Sınıflama Predictix planlama test kullanıcısı oluşturma](#create-a-predictix-assortment-planning-test-user)**  -toohave Britta Simon Predictix Sınıflama bağlantılı toohello Azure AD kullanıcı gösterimi olan planlama, karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Predictix Sınıflama planlama uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Predictix Sınıflama planlarken, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Predictix Sınıflama planlama** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. Merhaba üzerinde **Predictix Sınıflama planlama etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Predictix Sınıflama planlama etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Predictix Sınıflama planlama istemci destek ekibi](http://www.infor.com/support) tooget bu değerleri. 
 


4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Predictix Sınıflama yapılandırmasını planlama** 'yi tıklatın **yapılandırma Predictix Sınıflama planlama** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Predictix Sınıflama yapılandırmasını planlama](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **Predictix Sınıflama planlama** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)**, **SAML varlık kimliği**,  **SAML çoklu oturum açma hizmet URL'si**, ve **Sign-Out URL** çok[Predictix Sınıflama planlama destek ekibi](http://www.infor.com/support). Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-predictix-assortment-planning-test-user"></a>Sınıflama Predictix planlama test kullanıcısı oluşturma

Bu bölümde, Sınıflama Predictix planlamada Britta Simon adlı bir kullanıcı oluşturun. Lütfen çalışmak [Predictix Sınıflama planlama destek ekibi](http://www.infor.com/contact/) tooadd hello kullanıcılar hello Sınıflama Predictix planlama Platform.
 > [!NOTE]
 > Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooPredictix Sınıflama planlama vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooPredictix Sınıflama planlama, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Predictix Sınıflama planlama**.

    ![Merhaba Predictix Sınıflama planlama bağlantıyı hello uygulamalar listesi](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Predictix Sınıflama planlama parçasında hello erişim paneli tıkladığınızda, otomatik olarak oturum açma Predictix Sınıflama planlama uygulama tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

