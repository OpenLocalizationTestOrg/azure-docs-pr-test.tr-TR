---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zendesk | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zendesk arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Öğretici: Zendesk Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Zendesk Azure Active Directory'ye (Azure AD).

Zendesk Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooZendesk sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooZendesk (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Zendesk ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Zendesk çoklu oturum açma abonelik etkin


> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Zendesk hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-zendesk-from-hello-gallery"></a>Zendesk hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Zendesk, tooadd Zendesk hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Zendesk hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Zendesk**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. Merhaba Sonuçlar panelinde seçin **Zendesk**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zendesk sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Zendesk içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zendesk hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Zendesk içinde.

tooconfigure ve Zendesk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Zendesk test kullanıcısı oluşturma](#creating-a-zendesk-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zendesk içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zendesk uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Zendesk, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Zendesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. Merhaba üzerinde **Zendesk etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<subdomain>.zendesk.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri tanımlayıcı URL'si ve oturum açma hello gerçek URL ile güncelleştirin. Kişi [Zendesk destek ekibi](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget bu değerleri. 

4. Zendesk hello SAML onaylar belirli bir biçimde bekliyor. Zorunlu SAML özniteliklere vardır ancak özniteliği isteğe bağlı olarak ekleyebileceğiniz **kullanıcı öznitelikleri** bölümü aşağıdaki adımları aşağıdaki hello tarafından: 

     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Merhaba tıklatın **görüntüleme ve düzenleme tüm diğer özniteliklerle hello** onay kutusu.
     
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Merhaba tıklatın **özniteliği eklemek** tooopen **Ekle özniteliği** iletişim.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. Merhaba, **adı** metin kutusuna, türü hello öznitelik adı (örneğin **emailaddress**).
    
    d. Merhaba gelen **değeri** listesinde, select hello öznitelik değeri (olarak **user.mail**).
    
    e. Tıklatın **Tamam**
 
    > [!NOTE] 
    > Varsayılan olarak Azure AD'de olmayan uzantı öznitelikleri tooadd öznitelikleri kullanın. Tıklatın [SAML ayarlanabilir kullanıcı öznitelikleri](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello tam listesi SAML öznitelikleri **Zendesk** kabul eder. 

5. Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. Merhaba üzerinde **Zendesk yapılandırma** 'yi tıklatın **yapılandırma Zendesk** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. Farklı web tarayıcısı penceresinde Zendesk şirket sitenize yönetici olarak oturum açın.

8. Tıklatın **yönetici**.

9. Merhaba sol gezinti bölmesinde **ayarları**ve ardından **güvenlik**.

10. Merhaba üzerinde **güvenlik** sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
     ![Güvenlik](./media/active-directory-saas-zendesk-tutorial/ic773089.png "güvenlik")

    ![Çoklu oturum açma](./media/active-directory-saas-zendesk-tutorial/ic773090.png "çoklu oturum açma")

     a. Merhaba tıklatın **yönetici & aracıları** sekmesi.

     b. Seçin **çoklu oturum açma (SSO) ve SAML**ve ardından **SAML**.

     c. İçinde **SAML SSO URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan. 

     d. İçinde **uzak oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.
        
     e. İçinde **sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.
     
     f. **Kaydet** düğmesine tıklayın.

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. Kullanıcıların toodisplay hello listesini Git çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-a-zendesk-test-user"></a>Zendesk test kullanıcısı oluşturma

içine tooenable Azure AD kullanıcıların toolog **Zendesk**, içine sağlanmalıdır **Zendesk**.  
Merhaba uygulamalarında atanan hello rolüne bağlı olarak, hello beklenen davranıştır:

 1. **Son kullanıcı** hesapları otomatik olarak oturum açarken sağlandı.
 2. **Aracı** ve **yönetici** hesapları gereken el ile derlemenizde toobe **Zendesk** oturum açmadan önce.
 
**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Zendesk** Kiracı.

2. Select hello **müşteri listesi** sekmesi.

3. Select hello **kullanıcı** sekmesine ve tıklayın **Ekle**.
   
    ![Kullanıcı Ekle](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Kullanıcı Ekle")
4. Tooprovision istediğiniz ve ardından var olan bir Azure AD hesabını hello e-posta adresini yazın **kaydetmek**.
   
    ![Yeni kullanıcı](./media/active-directory-saas-zendesk-tutorial/ic773633.png "yeni kullanıcı")

> [!NOTE]
> API AAD kullanıcı hesaplarının Zendesk tooprovision tarafından sağlanan veya herhangi diğer Zendesk kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooZendesk vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooZendesk hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Zendesk**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Zendesk hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zendesk uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
