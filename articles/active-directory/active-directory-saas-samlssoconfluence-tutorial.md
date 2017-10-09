---
title: "Öğretici: Azure Active Directory ile tümleştirme Confluence için SAML SSO GmbH çözünürlüğün | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SAML SSO GmbH çözünürlüğün Confluence için arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Öğretici: Çözümleme GmbH Confluence için SAML SSO Azure Active Directory Tümleştirmesi

Bu öğreticide, bilgi nasıl toointegrate SAML SSO Confluence için Azure Active Directory (Azure AD) ile GmbH çözünürlüğün.

Azure AD ile GmbH çözünürlüğün SAML SSO Confluence için tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Çözümleme GmbH tarafından erişim tooSAML SSO Confluence için olan Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSAML Confluence için SSO (çoklu oturum açma) GmbH çözünürlüğün Azure AD hesaplarına etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure GmbH çözünürlüğün Confluence için SAML SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- SAML SSO etkin abonelik GmbH çoklu oturum çözünürlüğün Confluence için

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAML SSO Confluence için çözüm GmbH tarafından hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a>SAML SSO Confluence için çözüm GmbH tarafından hello Galerisi'nden ekleme

tooconfigure hello tümleştirilmesi Confluence için SAML SSO GmbH çözünürlüğün Azure AD'ye, tooadd SAML SSO için Confluence hello galeri tooyour yönetilen SaaS uygulamaları listesinden GmbH çözünürlüğün gerekir.

**tooadd Confluence için SAML SSO hello galerisinden GmbH çözünürlüğün hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SAML SSO GmbH çözünürlüğün Confluence için**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. Merhaba Sonuçlar panelinde seçin **SAML SSO GmbH çözünürlüğün Confluence için**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Confluence için SAML SSO GmbH "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı çözünürlüğün test etme

Tek toowork'ın oturum açma Azure AD hangi hello karşılık gelen kullanıcı SAML SSO Confluence için Azure AD içinde GmbH tooa kullanıcıdır çözünürlüğün tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello çözünürlüğün SAML SSO Confluence için ilgili kullanıcı arasında bir bağlantı ilişkisi GmbH kurulan toobe gerekir.

Merhaba hello değeri GmbH çözünürlüğün Confluence için SAML SSO içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açma ile test SAML SSO Confluence için GmbH çözünürlüğün, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SAML SSO çözümleme GmbH test kullanıcı tarafından Confluence için oluşturma](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave bir Britta Simon SAML SSO Confluence için karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir GmbH çözünürlüğün.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, SAML SSO Confluence için çözüm GmbH uygulama tarafından yapılandırın.

**Azure AD çoklu oturum açma GmbH, çözünürlüğün tooconfigure Confluence için SAML SSO hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **SAML SSO GmbH çözünürlüğün Confluence için** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. Merhaba üzerinde **Confluence GmbH etki alanı çözünürlüğün ve URL'ler için SAML SSO** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`

4. Denetleme **Göster Gelişmiş URL ayarları**. Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Kişi [SAML SSO GmbH istemci çözünürlüğün Confluence için destek ekibi](https://www.resolution.de/go/support) tooget bu değerleri. 

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. Farklı web tarayıcısı penceresinde tooyour içinde oturum **SAML SSO çözümleme GmbH Yönetici portalı tarafından Confluence için** yönetici olarak.

8. Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Yeniden yönlendirilen tooAdministrator erişim sayfası var. Merhaba parola girin ve tıklayın **Onayla** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. Altında **ATLASSIAN Market** sekmesini tıklatın, **Bul yeni eklentileri**. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Arama **SAML çoklu oturum açma (SSO) Confluence için** tıklatıp **yükleme** düğmesini tooinstall hello yeni SAML eklentisini.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. Merhaba eklentisi yükleme başlar. **Kapat**’a tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. **Yönet**'e tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Bu yeni eklenti ayrıca altında bulunabilir **kullanıcılar ve güvenlik** sekmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. Üzerinde **SAML SingleSignOn eklentisi yapılandırma** sayfasında, **ek kimlik sağlayıcısı ekleyin** düğmesini tooconfigure hello ayarlarını kimlik sağlayıcısı.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. Bu sayfada şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    a. Ekleme **adı** hello kimlik sağlayıcısı (örneğin Azure AD).
    
    b. Ekleme **açıklama** hello kimlik sağlayıcısı (örneğin Azure AD).

    c. Tıklatın **XML** ve select hello **meta veri** Azure Portalı'ndan indirilen dosya.

    d. Tıklatın **yük** düğmesi.

    e. Merhaba IDP meta verileri okur ve hello alanlar hello ekran vurgulu olarak doldurur.   
18. Tıklatın **Ayarları Kaydet** düğmesini toosave hello ayarları.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>SAML SSO çözümleme GmbH test kullanıcı tarafından Confluence için oluşturma

tooenable Azure AD kullanıcıların toolog Confluence için SSO GmbH çözünürlüğün tooSAML bunlar Confluence için SAML SSO içine GmbH çözümleme tarafından sağlanmalıdır.  
Confluence GmbH çözünürlüğün için SAML SSO içinde sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour SAML SSO çözümleme GmbH şirket site tarafından Confluence için yönetici olarak oturum açın.

2. Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. Kullanıcılar bölümü altında tıklatın **kullanıcıları eklemek** sekmesi. Merhaba üzerinde **"Bir kullanıcı Ekle"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının Britta Simon gibi türü hello e-posta.

    b. Merhaba, **tam adı** metin kutusuna, türü hello kullanıcının tam adını Britta Simon gibi.

    c. Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.

    d. Merhaba, **parola** metin kutusuna, Britta Simon hello parolayı girin.

    e. Tıklatın **parolayı onayla** hello parolayı yeniden girin.
    
    f. Tıklatın **Ekle** düğmesi.    

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, çözüm GmbH tarafından erişim tooSAML Confluence için SSO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign GmbH, çözünürlüğün Britta Simon tooSAML Confluence için SSO hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SAML SSO GmbH çözünürlüğün Confluence için**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba SAML SSO Confluence için çözüm GmbH hello erişim paneli parçasında tarafından tıkladığınızda, çözümleme GmbH uygulama tarafından Confluence için otomatik olarak oturum açma SAML SSO tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

