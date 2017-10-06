---
title: "Öğretici: Azure Active Directory Tümleştirme ile ScreenSteps | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ScreenSteps arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Öğretici: Azure Active Directory Tümleştirme ScreenSteps ile

Bu öğreticide, bilgi nasıl toointegrate ScreenSteps Azure Active Directory'ye (Azure AD).

ScreenSteps Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooScreenSteps sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooScreenSteps (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure ScreenSteps ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir ScreenSteps çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden ScreenSteps ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-screensteps-from-hello-gallery"></a>Merhaba Galerisi'nden ScreenSteps ekleme
Azure AD'ye tooconfigure hello tümleştirme ScreenSteps, tooadd ScreenSteps hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd ScreenSteps hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **ScreenSteps**seçin **ScreenSteps** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ScreenSteps sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen ScreenSteps içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ScreenSteps hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri ScreenSteps içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve ScreenSteps ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[ScreenSteps test kullanıcısı oluşturma](#create-a-screensteps-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ScreenSteps içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ScreenSteps uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile ScreenSteps, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **ScreenSteps** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. Merhaba üzerinde **ScreenSteps etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![ScreenSteps etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma, bu öğreticinin ilerleyen bölümlerinde açıklanan URL. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **ScreenSteps yapılandırma** 'yi tıklatın **yapılandırma ScreenSteps** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![ScreenSteps yapılandırma](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. Farklı web tarayıcısı penceresinde ScreenSteps şirket sitenize yönetici olarak oturum açın.

8. Tıklatın **hesap ayarları**.

    ![Hesap Yönetimi](./media/active-directory-saas-screensteps-tutorial/ic778523.png "hesap yönetimi")

9. Tıklatın **çoklu oturum açma**.

    ![Uzaktan kimlik doğrulama](./media/active-directory-saas-screensteps-tutorial/ic778524.png "uzaktan kimlik doğrulama")

10. Tıklatın **tek oturum açma uç noktası oluşturma**.

    ![Uzaktan kimlik doğrulama](./media/active-directory-saas-screensteps-tutorial/ic778525.png "uzaktan kimlik doğrulama")

11. Merhaba, **oluşturmak tek oturum açma uç noktası** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Bir kimlik doğrulama uç noktası oluşturma](./media/active-directory-saas-screensteps-tutorial/ic778526.png "bir kimlik doğrulama uç noktası oluşturma")
    
    a. Merhaba, **başlık** metin kutusuna, bir başlık yazın.
    
    b. Merhaba gelen **modu** listesinde **SAML**.
    
    c. **Oluştur**'a tıklayın.

12. **Düzen** yeni uç nokta hello.

    ![Uç noktayı Düzenle](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Düzenle uç noktası")

13. Merhaba, **Düzenle tek oturum açma uç noktası** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Uzaktan kimlik doğrulama uç noktası](./media/active-directory-saas-screensteps-tutorial/ic778527.png "uzaktan kimlik doğrulama uç noktası")

    a. Tıklatın **yeni SAML sertifika dosyası karşıya yükleme**ve Azure portalından indirdikten sonra karşıya yükleme hello sertifika.
    
    b. Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **uzaktan oturum açma URL'si** metin kutusu.
    
    c. Yapıştır **Sign-Out URL** hello hello Azure portal ' kopyaladığınız değeri **oturum kapatma URL'si** metin kutusu.
    
    d. Seçin bir **grup** tooassign kullanıcılar toowhen sağlandı.
    
    e. Tıklatın **güncelleştirme**.

    f. Kopya hello **SAML tüketici URL** toohello Pano toohello içinde Yapıştır **oturum açma URL'si** metin kutusuna **ScreenSteps etki alanı ve URL'leri** bölümü.
    
    g. Toohello iade **Düzenle tek oturum açma uç noktası**.
    
    h. Hello'ı tıklatın **olun hesabı için varsayılan** toouse ScreenSteps oturum tüm kullanıcılar için bu uç nokta düğmesine tıklayın. Alternatif olarak, hello tıklatabilirsiniz **tooSite ekleme** toouse belirli sitelerin Bu uç nokta düğmesini **ScreenSteps**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-screensteps-test-user"></a>ScreenSteps test kullanıcısı oluşturma

Bu bölümde, ScreenSteps içinde Britta Simon adlı bir kullanıcı oluşturun. Çalışmak [ScreenSteps istemci destek ekibi](https://www.screensteps.com/contact) hello ScreenSteps platform hello kullanıcıları eklemek için. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir. 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooScreenSteps vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooScreenSteps hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ScreenSteps**.

    ![Merhaba ScreenSteps bağlantı hello uygulamalar listesinde](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Hello erişim paneli ScreenSteps döşeme hello tıkladığınızda, otomatik olarak oturum açma ScreenSteps uygulama tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

