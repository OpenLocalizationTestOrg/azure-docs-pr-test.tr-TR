---
title: "Öğretici: Azure Active Directory Tümleştirme Bitbucket için Kantega SSO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kantega SSO Bitbucket için arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: e86a9a9a42f2f80fe83191f113f6bab46cc8a37d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a>Öğretici: Azure Active Directory Tümleştirme Kantega SSO Bitbucket için

Bu öğreticide, bilgi nasıl toointegrate Kantega SSO Azure Active Directory (Azure AD) ile Bitbucket için.

Kantega SSO Bitbucket için Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Bitbucket için erişim tooKantega SSO olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooKantega SSO (çoklu oturum açma) için Bitbucket'tan etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Bitbucket Kantega SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Abonelik Kantega SSO Bitbucket çoklu oturum açma için etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Bitbucket için Kantega SSO hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-kantega-sso-for-bitbucket-from-hello-gallery"></a>Bitbucket için Kantega SSO hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Bitbucket Kantega sso'nun tooadd Kantega SSO hello galeri tooyour listesinden yönetilen SaaS uygulamaları için Bitbucket'tan gerekir.

**tooadd Kantega SSO hello galerisinden Bitbucket için hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Kantega SSO Bitbucket için**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. Merhaba Sonuçlar panelinde seçin **Kantega SSO Bitbucket için**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Kantega SSO "Britta Simon" adlı bir test kullanıcı tabanlı Bitbucket için test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Kantega SSO Bitbucket için tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Bitbucket için Kantega SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bitbucket için Kantega SSO içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açma Bitbucket için test Kantega SSO, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bitbucket test kullanıcısı için Kantega SSO oluşturma](#creating-a-kantega-sso-for-bitbucket-test-user)**  -toohave Britta Simon Kantega SSO kullanıcı bağlantılı toohello Azure AD gösterimidir Bitbucket için karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve, Kantega SSO Bitbucket uygulama için çoklu oturum açmayı yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Bitbucket, Kantega SSO hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Kantega SSO Bitbucket için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. İçinde **IDP** hello modunda başlatılan **Kantega SSO Bitbucket etki alanı ve URL'ler için** bölümünde adım aşağıdaki hello gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. İçinde **SP** başlatılan modu, onay **Göster Gelişmiş URL ayarları** ve adım aşağıdaki hello gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Bu değerleri hello öğreticinin ilerleyen bölümlerinde açıklanan Bitbucket eklentisi hello yapılandırması sırasında alınır.

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. Farklı web tarayıcısı penceresinde tooyour Bitbucket Yönetim Portalı'nda yönetici olarak oturum açın.

8. Dişlisine tıklayın ve hello tıklatın **Bul yeni eklentileri**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. Arama **Kantega SSO Bitbucket SAML & Kerberos için** tıklatıp **yükleme** düğmesini tooinstall hello yeni SAML eklentisini.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. Merhaba Eklentisi yüklemeyi başlatır.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. Merhaba yüklemesi tamamlandıktan sonra. **Kapat**’a tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. **Yönet**'e tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. Merhaba, **SAML** bölümü. Seçin **Azure Active Directory (Azure AD)** hello gelen **Ekle kimlik sağlayıcısı** açılır.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. Abonelik düzeyi olarak **temel**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. Merhaba üzerinde **uygulama özellikleri** bölümünde, şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    a. Kopya hello **uygulama kimliği URI'si** değer ve olarak kullanmak **tanımlayıcısı, yanıt URL'si ve oturum açma URL'si** hello üzerinde **Kantega SSO Bitbucket etki alanı ve URL'ler için** Azure portalı bölümünde.

    b. **İleri**’ye tıklayın.

17. Merhaba üzerinde **meta veri içeri aktarma** bölümünde, şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    a. Seçin **meta veri dosyası bilgisayarımda**ve Azure portalından karşıdan yükleme meta veri dosyası.

    b. **İleri**’ye tıklayın.

18. Merhaba üzerinde **adı ve SSO konumunu** bölümünde, şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    a. Merhaba kimlik sağlayıcısı adını ekleyin, **kimlik sağlayıcı adı** textbox (örneğin Azure AD).

    b. **İleri**’ye tıklayın.

19. Merhaba imzalama sertifikası doğrulayın ve tıklatın **sonraki**.    

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. Merhaba üzerinde **Bitbucket kullanıcı hesapları** bölümünde, şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    a. Seçin **gerekirse Bitbucket'ınızın iç dizinde kullanıcılar oluşturma** ve kullanıcıların hello grubunun adı uygun hello girin (olabilir birden çok yok. virgülle ayrılmış grupları).

    b. **İleri**’ye tıklayın.

21. **Son**'a tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. Merhaba üzerinde **için Azure AD etki alanları bilinen** bölümünde, şu adımları gerçekleştirin:   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    a. Seçin **etki alanları bilinen** hello sayfasının sol hello panelinden.

    b. Hello etki alanı adı girin **etki alanları bilinen** metin kutusu.

    c. **Kaydet** düğmesine tıklayın.  

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a>Kantega SSO Bitbucket test kullanıcısı için oluşturma

tooenable Azure AD kullanıcıların toolog tooBitbucket bunların Bitbucket sağlanması gerekir. Bitbucket için Kantega SSO içinde sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour Bitbucket şirket site yönetici olarak oturum açın.

2. Ayarlar simgesine tıklayın.

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. Altında **Yönetim** bölüm sekmesini tıklatın, **kullanıcılar**.

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. Tıklatın **kullanıcı oluşturma**.

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. Merhaba üzerinde **kullanıcı oluştur** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    a. Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.
    
    b. Merhaba, **tam adı** metin kutusuna, Britta Simon gibi hello kullanıcının tam adını yazın.
    
    c. Merhaba, **e-posta adresi** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.

    d. Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.  

    e. Merhaba, **parolayı onayla** metin kutusuna, kullanıcının parolasını hello.

    f. Tıklatın **kullanıcı oluşturma**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, Bitbucket için erişim tooKantega SSO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooKantega Bitbucket, SSO hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Kantega SSO Bitbucket için**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Kantega SSO hello erişim paneli Bitbucket parçasında tıkladığınızda, Bitbucket uygulaması için otomatik olarak oturum açma Kantega SSO tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

