---
title: "Öğretici: Azure Active Directory Tümleştirme ile Asana | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Asana arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>Öğretici: Azure Active Directory Tümleştirme Asana ile

Bu öğreticide, bilgi nasıl toointegrate Asana Azure Active Directory'ye (Azure AD).

Asana Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAsana sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooAsana (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Asana ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Asana çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Asana ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-asana-from-hello-gallery"></a>Merhaba Galerisi'nden Asana ekleme
Azure AD'ye tooconfigure hello tümleştirme Asana, tooadd Asana hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Asana hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Asana**seçin **Asana** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Asana ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Asana içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Asana hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Asana içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Asana ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Asana test kullanıcısı oluşturma](#create-an-asana-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Asana içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Asana uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Asana, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Asana** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. Merhaba üzerinde **Asana etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Asana etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü URL'si:`https://app.asana.com/`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, tür değeri:`https://app.asana.com/`
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Asana yapılandırma** 'yi tıklatın **yapılandırma Asana** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Asana yapılandırma](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. Farklı bir tarayıcı penceresinde oturum açma Asana uygulama tooyour. tooconfigure Asana, erişim hello çalışma alanı ayarları'hello çalışma hello sağ üst köşesinde hello ekran adına tıklayarak SSO. Ardından, tıklatın  **\<çalışma alanı adınız\> ayarları**. 
   
    ![Asana sso ayarları](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. Merhaba üzerinde **kuruluş ayarları** penceresinde tıklatın **Yönetim**. Ardından **üyeleri gerekir oturum SAML** tooenable hello SSO yapılandırma. Merhaba hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma kuruluş ayarlarını yapılandırma](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. Merhaba, **oturum açma sayfası URL'si** metin kutusuna, Yapıştır hello **SAML çoklu oturum açma hizmet URL'si**.

     b. Azure portalından indirdiğiniz hello sertifikayı sağ tıklatın, sonra hello sertifika dosyasını Not Defteri'nde veya tercih edilen metin düzenleyiciyi kullanarak açın. Merhaba arasında kopyalama hello içerik başlamak ve hello son sertifika başlık ve hello yapıştırın **X.509 sertifikası** metin kutusu.

9. **Kaydet** düğmesine tıklayın. Çok Git[SSO'yu ayarlamak için Asana Kılavuzu](https://asana.com/guide/help/premium/authentication#gl-saml) daha fazla yardıma ihtiyacınız varsa.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-an-asana-test-user"></a>Bir Asana test kullanıcısı oluşturma

Bu bölümde, Asana içinde Britta Simon adlı bir kullanıcı oluşturun.

1. Üzerinde **Asana**, Git toohello **takımlar** hello Sol paneldeki bölümü. Yanı sıra düğmesi oturum Hello'ı tıklatın. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Tür hello e-posta britta.simon@contoso.com hello metin kutusuna ve ardından **davet**.

3. Tıklatın **Gönder davet**. Merhaba yeni kullanıcı bir e-posta kendi e-posta dikkate alır. Kendisinin toocreate gerekir ve hello hesabı doğrulanamıyor.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooAsana vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200]

**tooassign Britta Simon tooAsana hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Asana**.

    ![Merhaba Asana bağlantı hello uygulamalar listesinde](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde Hello amacı, Azure AD çoklu oturum açma tootest değil.

TooAsana oturum açma sayfasına gidin. Merhaba e-posta adresi metin kutusuna hello e-posta adresi eklemek britta.simon@contoso.com. Merhaba parola metin kutusunu boş bırakın ve ardından **oturum**. Yeniden yönlendirilen tooAzure AD oturum açma sayfasına olacaktır. Azure AD kimlik bilgilerinizi tamamlayın. Şimdi, Asana üzerinde oturum açtınız.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
