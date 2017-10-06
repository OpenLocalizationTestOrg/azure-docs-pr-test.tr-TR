---
title: "Öğretici: Azure Active Directory Tümleştirme ile LockPath Keylight | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LockPath Keylight arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Öğretici: Azure Active Directory Tümleştirme LockPath Keylight ile

Bu öğreticide, bilgi nasıl toointegrate LockPath Keylight Azure Active Directory'ye (Azure AD).

LockPath Keylight Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLockPath Keylight sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooLockPath Keylight (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure LockPath Keylight ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir LockPath Keylight çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden LockPath Keylight ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Merhaba Galerisi'nden LockPath Keylight ekleme
Azure AD'ye tooconfigure hello tümleştirme LockPath Keylight, tooadd LockPath Keylight hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd LockPath Keylight hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **LockPath Keylight**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. Merhaba Sonuçlar panelinde seçin **LockPath Keylight**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve LockPath Keylight ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı

Tek toowork'ın oturum açma hangi hello karşılık gelen LockPath Keylight içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LockPath Keylight hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri LockPath Keylight içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve LockPath Keylight ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[LockPath Keylight test kullanıcısı oluşturma](#creating-a-lockpath-keylight-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LockPath Keylight içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LockPath Keylight uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma LockPath Keylight ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **LockPath Keylight** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. Merhaba üzerinde **LockPath Keylight etki alanı ve URL'leri** bölümünde, aşağıdaki adımları hello gerçekleştirmek::

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.keylightgrc.com/`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.keylightgrc.com`

    c. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Kişi [LockPath Keylight istemci destek ekibi](https://www.lockpath.com/contact/) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. Merhaba üzerinde **LockPath Keylight yapılandırma** 'yi tıklatın **yapılandırma LockPath Keylight** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable LockPath Keylight SSO hello aşağıdaki adımları gerçekleştirin:
   
    a. Oturum açma LockPath Keylight hesabı yönetici olarak tooyour.
    
    b. Hello içinde hello üst menüsünde **kişi**seçip **Keylight Kurulum**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. Merhaba soldaki Hello treeview içinde tıklatın **SAML**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. Merhaba üzerinde **SAML ayarları** iletişim kutusunda, tıklatın **Düzenle**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/404.png) 

8. Merhaba üzerinde **SAML ayarlarını Düzenle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Ayarlama **SAML kimlik doğrulaması** çok**etkin**.

    b. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.

    c. Yapıştır hello **tek Sign-Out hizmeti URL'si** hello hello Azure portal ' kopyaladığınız değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.

    d. Tıklatın **Dosya Seç** tooselect indirilen LockPath Keylight sertifika ve ardından **açık** tooupload hello sertifika.

    e. Ayarlama **SAML kullanıcı kimliği konumu** çok**NameIdentifier öğesi hello konu deyiminin**.
    
    f. Merhaba sağlamak **Keylight hizmet sağlayıcısı** desen aşağıdaki hello kullanarak: **https://&lt;ŞirketAdı&gt;. keylightgrc.com**.
    
    g. Ayarlama **otomatik sağlama kullanıcılar** çok**etkin**.

    h. Ayarlama **otomatik sağlama hesap türü** çok**tam kullanıcı**.

    ı. Ayarlama **otomatik sağlama güvenlik rolü**seçin **SAML sahip standart kullanıcı**.
    
    j. Ayarlama **otomatik sağlama güvenlik config**seçin **standart kullanıcı yapılandırması**.
     
    k. Merhaba, **e-posta özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. Merhaba, **ad özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. Merhaba, **son name özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>LockPath Keylight test kullanıcısı oluşturma

Bu bölümde, Britta Simon LockPath Keylight adlı bir kullanıcı oluşturun. LockPath Keylight tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümde, eylem öğe yok. Yeni bir kullanıcı hello kullanıcı henüz yoksa LockPath Keylight erişirken oluşturulur. 

>[!NOTE]
>Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [LockPath Keylight istemci destek ekibi](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooLockPath Keylight vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLockPath Keylight, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **LockPath Keylight**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

LockPath Keylight döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma LockPath Keylight uygulama tooyour almanız gerekir. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

