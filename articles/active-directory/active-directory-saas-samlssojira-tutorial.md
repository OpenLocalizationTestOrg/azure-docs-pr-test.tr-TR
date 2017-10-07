---
title: "Öğretici: Azure Active Directory ile tümleştirme Jira için SAML SSO GmbH çözünürlüğün | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SAML SSO GmbH çözünürlüğün Jira için arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Öğretici: Çözümleme GmbH Jira için SAML SSO Azure Active Directory Tümleştirmesi

Bu öğreticide, bilgi nasıl toointegrate SAML SSO Jira için Azure Active Directory (Azure AD) ile GmbH çözünürlüğün.

Azure AD ile GmbH çözünürlüğün SAML SSO Jira için tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSAML SSO için Jira tarafından çözüldü GmbH sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına sahip (çoklu oturum açma) GmbH çözünürlüğün Jira için kullanıcılar tooautomatically get açan tooSAML SSO etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure GmbH çözünürlüğün Jira için SAML SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- SAML SSO etkin abonelik GmbH çoklu oturum çözünürlüğün Jira için

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAML SSO Jira için çözüm GmbH tarafından hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a>SAML SSO Jira için çözüm GmbH tarafından hello Galerisi'nden ekleme
tooconfigure hello tümleştirilmesi Jira için SAML SSO GmbH çözünürlüğün Azure AD'ye, tooadd SAML SSO için Jira hello galeri tooyour yönetilen SaaS uygulamaları listesinden GmbH çözünürlüğün gerekir.

**tooadd Jira için SAML SSO hello galerisinden GmbH çözünürlüğün hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SAML SSO GmbH çözünürlüğün Jira için**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. Merhaba Sonuçlar panelinde seçin **SAML SSO GmbH çözünürlüğün Jira için**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Jira için SAML SSO GmbH "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı çözünürlüğün test etme

Tek toowork'ın oturum açma Azure AD hangi hello karşılık gelen kullanıcı SAML SSO Jira için Azure AD içinde GmbH tooa kullanıcıdır çözünürlüğün tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello çözünürlüğün SAML SSO Jira için ilgili kullanıcı arasında bir bağlantı ilişkisi GmbH kurulan toobe gerekir.

Merhaba hello değeri GmbH çözünürlüğün Jira için SAML SSO içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açma ile test SAML SSO Jira için GmbH çözünürlüğün, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SAML SSO çözümleme GmbH test kullanıcı tarafından Jira için oluşturma](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave bir Britta Simon SAML SSO Jira için karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir GmbH çözünürlüğün.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, SAML SSO Jira için çözüm GmbH uygulama tarafından yapılandırın.

**Azure AD çoklu oturum açma GmbH, çözünürlüğün tooconfigure Jira için SAML SSO hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **SAML SSO GmbH çözünürlüğün Jira için** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. Merhaba üzerinde **Jira GmbH etki alanı çözünürlüğün ve URL'ler için SAML SSO** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`

4. Denetleme **Göster Gelişmiş URL ayarları**. Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Kişi [SAML SSO GmbH istemci çözünürlüğün Jira için destek ekibi](https://www.resolution.de/go/support) tooget bu değerleri. 

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. Farklı web tarayıcısı penceresinde tooyour içinde oturum **SAML SSO çözümleme GmbH Yönetici portalı tarafından Jira için** yönetici olarak.

8. Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. Yeniden yönlendirilen tooAdministrator erişim sayfası var. Merhaba girin **parola** tıklatıp **Onayla** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. Eklentiler sekmesi bölümü altında tıklatın **Bul yeni eklentileri**. Arama **SAML çoklu oturum açma (SSO) JIRA için** tıklatıp **yükleme** düğmesini tooinstall hello yeni SAML eklentisini.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. Merhaba eklentisi yükleme başlar. **Kapat**’a tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. **Yönet**'e tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. Üzerinde **SAML SingleSignOn eklentisi yapılandırma** sayfasında, **ek kimlik sağlayıcısı ekleyin** düğmesini tooconfigure hello ayarlarını kimlik sağlayıcısı.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. Bu sayfada şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. Ekleme **adı** hello kimlik sağlayıcısı (örneğin Azure AD).
    
    b. Ekleme **açıklama** hello kimlik sağlayıcısı (örneğin Azure AD).

    c. Tıklatın **XML** ve select hello **meta veri** Azure Portalı'ndan indirilen dosya.

    d. Tıklatın **yük** düğmesi.

    e. Merhaba IDP meta verileri okur ve hello alanlar hello ekran vurgulu olarak doldurur.   

16. Tıklatın **Ayarları Kaydet** düğmesini toosave hello ayarları.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>SAML SSO çözümleme GmbH test kullanıcı tarafından Jira için oluşturma

tooenable Azure AD kullanıcıların toolog Jira için SSO GmbH çözünürlüğün tooSAML bunlar Jira için SAML SSO içine GmbH çözümleme tarafından sağlanmalıdır.  
Jira GmbH çözünürlüğün için SAML SSO içinde sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour SAML SSO çözümleme GmbH şirket site tarafından Jira için yönetici olarak oturum açın.

2. Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. Yeniden yönlendirilen tooAdministrator erişim sayfası tooenter olduğunuz **parola** tıklatıp **Onayla** düğmesi.

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. Altında **kullanıcı yönetimi** bölüm sekmesini tıklatın, **kullanıcı oluşturma**.

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. Merhaba üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. Merhaba, **e-posta adresi** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.

    b. Merhaba, **tam adı** metin kutusuna, Britta Simon gibi hello kullanıcının tam adını yazın.

    c. Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.

    d. Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.

    e. Tıklatın **kullanıcı oluşturma**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSAML SSO için Jira tarafından çözüldü GmbH vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign GmbH, çözünürlüğün Britta Simon tooSAML Jira için SSO hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SAML SSO GmbH çözünürlüğün Jira için**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba SAML SSO Jira için çözüm GmbH hello erişim paneli parçasında tarafından tıkladığınızda, çözümleme GmbH uygulama tarafından Jira için otomatik olarak oturum açma SAML SSO tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

