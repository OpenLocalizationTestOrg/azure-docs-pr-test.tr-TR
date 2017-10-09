---
title: "Öğretici: Azure Active Directory Tümleştirme ile Merces tarafından HR2day | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile HR2day Merces tarafından arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Öğretici: Azure Active Directory Tümleştirme Merces tarafından HR2day ile

Bu öğreticide, bilgi nasıl toointegrate HR2day tarafından Azure Active Directory (Azure AD) ile Merces.

HR2day Merces tarafından Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Merces tarafından erişim tooHR2day sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcılarınızın tooautomatically imzalı tooHR2day içinde Merces tarafından kendi Azure AD hesapları ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda--hello Azure portalında yönetebilir.

Azure AD SaaS uygulama tümleştirmesi hakkında daha fazla bilgi için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure HR2day Merces tarafından ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD abonelik.
- Bir HR2day Merces çoklu oturum açma tarafından abonelik etkin.

> [!NOTE]
> Bir üretim ortamında tootest hello kullanarak bu öğreticideki adımlar öneririz yok.

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Alma bir [bir aylık ücretsiz deneme Azure ad](https://azure.microsoft.com/pricing/free-trial/) , zaten yoksa.  

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Burada özetlenen hello senaryo iki ana yapı taşlarını oluşur:

1. HR2day Merces tarafından hello Galerisi'nden ekleniyor.
2. Yapılandırma ve Azure AD sınama çoklu oturum açmayı.

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Merhaba Galerisi'nden Merces tarafından HR2day ekleme
Azure AD'ye HR2day Merces tarafından tooconfigure hello tümleştirilmesi hello galeri tooyour listesinden yönetilen SaaS uygulamaları Merces tarafından HR2day ekleyin.

**tooadd HR2day Merces hello galerisinden tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, seçin hello **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok Git**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni bir uygulama seçin hello **yeni uygulama** hello hello iletişim kutusunun üstündeki düğmesinde.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **HR2day Merces tarafından**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. Merhaba Sonuçlar panelinde seçin **HR2day Merces tarafından**ve ardından hello **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Merces tarafından HR2day ile test etme

Tek toowork'ın oturum açma Azure AD hello karşılık gelen Merces tarafından HR2day içinde tooa kullanıcı Azure AD içinde olduğu tooknow gerekir. Diğer bir deyişle, tooestablish bir Azure AD kullanıcı ve ilgili kullanıcı HR2day Merces tarafından hello arasında bir bağlantı gerekir.

Merhaba Merces tarafından HR2day içinde atamak **kullanıcı adı** Azure AD'de çok **kullanıcıadı** tooestablish hello ilişki.

tooconfigure ve HR2day Merces tarafından ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. [Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on): Bu özellik, kullanıcıların toouse etkinleştirin.
2. [Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user): Test Azure AD çoklu oturum açma Britta Simon ile.
3. [Merces test kullanıcı tarafından bir HR2day oluşturma](#creating-an-hr2day-by-merces-test-user): Britta Simon, karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir Merces tarafından HR2day oluşturun.
4. [Hello Azure AD test kullanıcısı atayın](#assigning-the-azure-ad-test-user): Azure AD çoklu oturum açmayı etkinleştir Britta Simon toouse.
5. [Test çoklu oturum açma](#testing-single-sign-on): hello yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, HR2day Merces uygulama tarafından yapılandırın.

**tooconfigure Azure AD çoklu oturum açma HR2day Merces tarafından ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Merces tarafından HR2day** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. tooenable çoklu oturum açma, hello içinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma**.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. Merhaba, **HR2day Merces etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. Merhaba, **oturum açma URL'si** kutusuna bir URL deseni takip hello kullanarak yazın: `https://<tenantname>.force.com/<instancename>`.

    b. Merhaba, **tanımlayıcısı** kutusuna bir URL deseni takip hello kullanarak yazın: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerler, oturum açma hello gerçek URL ve tanımlayıcıdır ile güncelleştirin. Kişi hello [Merces istemci destek ekibi tarafından HR2day](mailto:servicedesk@merces.nl) tooget bu değerleri. 
 


4. Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **Certificate(Base64)**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. Bu bölümde açıklanmıştır nasıl Itanium tabanlı sistemler için tooenable kullanıcılar tooauthenticate tooHR2day Merces tarafından Azure AD'de hesabıyla. SAML Protokolü hello üzerinde temel Federasyon kullanarak bunu.

    Merces uygulama tarafından HR2day hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour SAML belirteci gerektiren belirli bir biçimde, bekliyor. Aşağıdaki ekran görüntüsü hello bunun bir örneğini gösterir. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Merhaba SAML onayı yapılandırmadan önce hello başvurmalıdır [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl) ve kiracınız için hello benzersiz tanımlayıcı özniteliği hello değerini isteyin. Bu değer toocomplete hello adımları hello sonraki bölümde gerekir. 

6. Merhaba, **çoklu oturum açma** iletişim kutusunda hello **kullanıcı öznitelikleri** bölümünde, hello SAML belirteci özniteliği hello görüntü aşağıdaki gösterildiği gibi yapılandırın. Ardından hello aşağıdaki adımları uygulayın.
    
      | Öznitelik adı    |   Öznitelik değeri |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | Birleştirme ([posta] "102938475Z", "@" |
    
      a. tooopen hello **özniteliği eklemek** iletişim kutusunda **Ekle özniteliği**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. Merhaba, **adı** kutusuna **ATTR_LOGINCLAIM**.

    c. Merhaba gelen **değeri** listesinde **Join()**.

    d. Merhaba gelen **Dize1** listesinde **user.mail**.

    e. İçin **dize2**, HR2day ekibiniz tarafından sunulan benzersiz bir tanımlayıcı hello yazın.

    f. Merhaba, **ayırıcı** kutusuna  **@** .
    
    g. Seçin **Tamam**.

7. Select hello **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. Merhaba, **HR2day Merces yapılandırma tarafından** bölümünde, select **yapılandırma HR2day Merces tarafından** tooopen hello **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru** bölümü.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. Uygulama, kişi hello için SSO tooconfigure [HR2day Merces istemci destek ekibi tarafından](mailTo:servicedesk@merces.nl). İndirilen hello attach **Certificate(Base64)** dosya tooyour e-posta. Ayrıca hello sağlamak **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** böylece SSO tümleştirmesi için yapılandırılmış.

    > [!NOTE]
    >Bu tümleştirme hello desenle ayarlamak varlık kimliği toobe hello gereken toohello Merces takım Bahsediyor **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümü, select hello **çoklu oturum açma** sekmesi. Ardından hello aracılığıyla belgelere erişimi hello katıştırılmış **yapılandırma** hello alt kısmına. Daha fazla bilgiyi hello hello embedded belgeler özelliği hakkında [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, seçin hello **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda **Ekle** hello iletişim kutusunun hello üstte.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin hello:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusu, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola**ve ardından hello parolayı not alın.

    d. **Oluştur**’u seçin.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Bir HR2day tarafından Merces test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde HR2day tarafından Merces adlı bir kullanıcı var. Merhaba HR2day hesabındaki tooadd hello kullanıcıların çalışması ile Merhaba [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Bir kullanıcı toocreate el ile gerekiyorsa hello başvurun [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, kendi erişim tooHR2day Merces tarafından vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooHR2day Merces tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, açık hello uygulamaları görüntülemek, toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar**. Ardından, **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **HR2day Merces tarafından**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. Merhaba soldaki Hello menüde seçin **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Select hello **Ekle** düğmesi. Ardından hello **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][203]

5. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinde **Britta Simon**.

6. Merhaba tıklatın **seçin** düğmesi.

7. Merhaba, **eklemek atama** iletişim kutusunda **atamak**.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Merhaba, bu bölümün amacı olan tootest kullanarak Azure AD çoklu oturum açma yapılandırmanızı hello erişim paneli.  

Merhaba erişim paneli Merces parçasında tarafından hello HR2day seçtiğinizde otomatik olarak tooyour HR2day Merces uygulama tarafından oturumunuz.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

