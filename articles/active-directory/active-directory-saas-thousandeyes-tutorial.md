---
title: "Öğretici: Azure Active Directory Tümleştirme ile ThousandEyes | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ThousandEyes arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Öğretici: Azure Active Directory Tümleştirme ThousandEyes ile

Bu öğreticide, bilgi nasıl toointegrate ThousandEyes Azure Active Directory'ye (Azure AD).

ThousandEyes Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooThousandEyes sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooThousandEyes (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure ThousandEyes ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir ThousandEyes çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden ThousandEyes ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-thousandeyes-from-hello-gallery"></a>Merhaba Galerisi'nden ThousandEyes ekleme
Azure AD'ye tooconfigure hello tümleştirme ThousandEyes, tooadd ThousandEyes hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd ThousandEyes hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **ThousandEyes**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. Merhaba Sonuçlar panelinde seçin **ThousandEyes**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ThousandEyes sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen ThousandEyes içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ThousandEyes hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri ThousandEyes içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve ThousandEyes ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[ThousandEyes test kullanıcısı oluşturma](#creating-a-thousandeyes-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ThousandEyes içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ThousandEyes uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile ThousandEyes, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **ThousandEyes** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. Merhaba üzerinde **ThousandEyes etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://app.thousandeyes.com/login/sso`

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **ThousandEyes yapılandırma** 'yi tıklatın **yapılandırma ThousandEyes** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour üzerinde oturum **ThousandEyes** yönetici olarak şirket site.

8. Hello içinde hello üst menüsünde **ayarları**.
   
    ![Ayarları](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "ayarları")

9. Tıklatın **hesabı**
   
    ![Hesap](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "hesabı")

10. Merhaba tıklatın **güvenlik ve kimlik doğrulama** sekmesi.
   
    ![Güvenlik ve kimlik doğrulama](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "güvenlik ve kimlik doğrulama")

11. Merhaba, **Kurulum çoklu oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma Kurulum](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Kurulum çoklu oturum açma")
  
    a. Seçin **çoklu oturum açmayı etkinleştir**.
  
    b. İçinde **oturum açma sayfası URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
  
    c. İçinde **oturum kapatma sayfası URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.
  
    d. **Kimlik sağlayıcısı veren** metin kutusuna, Yapıştır **SAML varlık kimliği** Azure portalından kopyalanan.
  
    e. İçinde **doğrulama sertifikası**, tıklatın **dosya**ve Azure portalından indirdiğiniz hello sertifikasını karşıya yükleyin.
  
    f. **Kaydet** düğmesine tıklayın.
 
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-thousandeyes-test-user"></a>ThousandEyes test kullanıcısı oluşturma

ThousandEyes içine sipariş tooenable Azure AD kullanıcıların toolog bunların ThousandEyes sağlanmalıdır.  
ThousandEyes Hello durumda sağlama bir el ile bir görevdir.

>[!NOTE]
>API, kullanıcı hesaplarını ThousandEyes tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer ThousandEyes kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

**bir kullanıcı hesabı tooThousandEyes tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. ThousandEyes şirket sitenize yönetici olarak oturum açın.

2. Tıklatın **ayarları**.
   
    ![Ayarları](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "ayarları")

3. Tıklatın **hesap**.
   
    ![Hesap](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "hesabı")

4. Merhaba tıklatın **hesapları k & ullanıcıların** sekmesi.
   
    ![K & ullanıcıların hesapları](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "hesapları ve kullanıcılar")

5. Merhaba, **Kullanıcı Ekle & hesapları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı hesapları ekleme](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "kullanıcı hesapları ekleme")   
  
    a. İçinde **adı** metin kutusuna, tür hello gibi kullanıcı adını **Britta Simon**.

    b. İçinde **e-posta** metin kutusuna, kullanıcının türü hello e-posta ister  **brittasimon@contoso.com** .
   
    b. Tıklatın **yeni kullanıcı Ekle tooAccount**.
      
     >[!NOTE]
     >Hello Azure Active Directory hesap sahibi bağlantı tooconfirm dahil olmak üzere bir e-posta almak ve hello hesabını etkinleştirebilir.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooThousandEyes vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooThousandEyes hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ThousandEyes**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Hello erişim paneli ThousandEyes döşeme hello tıkladığınızda, otomatik olarak oturum açma ThousandEyes uygulama tooyour almanız gerekir.

Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

