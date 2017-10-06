---
title: "Öğretici: Azure Active Directory Tümleştirme JIRA SAML SSO Microsoft tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Microsoft tarafından JIRA SAML SSO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>Öğretici: Microsoft tarafından JIRA SAML SSO Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate JIRA SAML SSO Microsoft Azure Active Directory'ye (Azure AD).

Microsoft tarafından JIRA SAML SSO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Microsoft tarafından SAML SSO erişimi tooJIRA sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooJIRA SAML SSO (çoklu oturum açma) Microsoft tarafından etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Microsoft tarafından JIRA SAML SSO ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Windows 64-bit sunucuda (şirket içi veya hello bulut Iaas altyapı) yüklü JIRA sunucu uygulaması
- HTTPS etkinleştirilmiş JIRA sunucusudur
- Not hello desteklenen sürümleri JIRA eklentisi için varsayılan olarak, aşağıdaki bölümünün içinde açıklanan.
- JIRA sunucusudur Internet üzerinden ulaşılabilir özellikle tooAzure AD oturum açma sayfasında kimlik doğrulaması için ve mümkün tooreceive Azure AD'den belirteci hello
- Yönetici kimlik bilgileri JIRA ayarlanır
- WebSudo JIRA içinde devre dışı bırakıldı
- Test kullanıcısı Hello JIRA sunucu uygulaması oluşturuldu

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamında JIRA birini kullanarak önermiyoruz. Merhaba tümleştirme ilk geliştirme veya hazırlama ortamı hello uygulamasının ve kullanım hello üretim ortamında test edin.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-jira"></a>JIRA desteklenen sürümleri 

Şimdi itibariyle JIRA aşağıdaki sürümleri desteklenir:

- JIRA çekirdek ve yazılım: 6.0 too7.2.0
- JIRA hizmet masasına: 3.0 too3.2

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Microsoft tarafından JIRA SAML SSO hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>Microsoft tarafından JIRA SAML SSO hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme, Microsoft tarafından JIRA SAML SSO tooadd JIRA SAML SSO Microsoft tarafından hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd JIRA SAML SSO hello Galerisi'nden Microsoft tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **JIRA SAML SSO Microsoft tarafından**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. Merhaba Sonuçlar panelinde seçin **JIRA SAML SSO Microsoft tarafından**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma JIRA SAML SSO "Britta Simon." olarak adlandırılan bir test kullanıcıyı temel alarak Microsoft tarafından test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen JIRA SAML SSO Microsoft tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve Microsoft tarafından JIRA SAML SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Microsoft tarafından JIRA SAML SSO içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Microsoft tarafından JIRA SAML SSO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Microsoft test kullanıcı tarafından JIRA SAML SSO oluşturma](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave Britta Simon JIRA SAML SSO kullanıcı bağlantılı toohello Azure AD gösterimidir Microsoft tarafından karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Microsoft uygulaması tarafından JIRA SAML SSO yapılandırın.

**Microsoft tarafından JIRA SAML SSO ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **JIRA SAML SSO Microsoft tarafından** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. Merhaba üzerinde **JIRA SAML SSO Microsoft Domain ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/plugins/servlet/saml/auth`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/`

    c. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Adlandırılmış bir URL olması durumunda bağlantı noktası isteğe bağlıdır. Bu değerleri hello öğreticinin ilerleyen bölümlerinde açıklanan Jira eklentisi hello yapılandırması sırasında alınır.
 
4. toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:

    a. Tıklatın **uygulama kayıtlar**.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. Şimdi toohello özellik sayfasında gidin **JIRA SAML SSO Microsoft tarafından** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    e. Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` ve daha sonra hello eklentisi hello yapılandırması için kullanılan bu değer Not Defteri'nde kopyalayın.

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. Kişi [Microsoft](mailto:waadpartners@microsoft.com) bilgi hello JIRA eklentisi için aşağıdaki hello ile.
    
    *   Müşteri adı:
    *   Birincil etki alanı adı:
    *   Azure AD Premium: Evet/Hayır (eklentisi kullanılabilir tooall hello müşteri ücretsiz, temel ve Premium SKU olacaktır)
    *   Bu tümleştirme kullanarak kullanıcıların sayısı:
    *   JIRA sürümü:
    *   Açıklama:

7. Farklı web tarayıcısı penceresinde tooyour JIRA örneğinde yönetici olarak oturum açın.

8. Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. Eklentiler sekmesi bölümü altında tıklatın **eklentileri yönetme**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. Microsoft tarafından sağlanan hello eklentisini el ile yükleyin. Merhaba eklentisi yüklendikten sonra görünür **kullanıcı yüklü** eklentileri bölümünü **yönetmek eklenti** bölümü.

11. Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.

12. Yapılandırma sayfasında şu adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    a. İçinde **meta veri URL'sini** hello yapıştırın **meta veri URL'sini** Azure AD'den oluşturulur ve hello tıklatın **gidermek** düğmesi. Merhaba IDP meta veri URL'sini okur ve tüm hello alanları bilgileri doldurur.

    > [!Note]
    > Varsayılan SAML kullanıcı kimliği konumu ad tanımlayıcısıdır. Bu tooan özniteliği seçeneği değiştirmek ve hello uygun öznitelik adı girin.

    > [!TIP]
    > Yani hata hello meta veri çözümlemede hello uygulamayı karşı eşlenen yalnızca bir sertifika olduğundan emin olun. Merhaba meta veri çözümleme sırasında birden fazla sertifika varsa yönetici bir hata alır.
    
    b. Kopya hello **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** değerleri ve bunları yapıştırın **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** kutularındaki sırasıyla içinde **JIRA SAML SSO Microsoft Domain ve URL'leri** Azure Portal'daki bölümü.

    c. İçinde **oturum açma düğmesi adı** türü hello adı düğmesine kuruluşunuz hello kullanıcılar toosee oturum açma ekranında istemektedir.

    d. İçinde **SAML kullanıcı kimliği konumları** seçin **kullanıcı kimliğidir hello NameIdentifier öğesinde hello konu deyimi** veya **kullanıcı kimliği olan bir öznitelik öğedeki**.  Bu kimliği toobe hello JIRA kullanıcı kimliği var. Merhaba kullanıcı kimliği eşleşmiyorsa, ardından sistemi kullanıcılar toolog izin vermez. 
    
    e. Seçerseniz **kullanıcı kimliği olan bir öznitelik öğedeki** seçeneği, sonra **öznitelik adı** kullanıcı kimliği beklenirken hello özniteliğinin textbox türü hello adı. 

    f. Azure AD ile Merhaba Federasyon etki alanını (örneğin, ADFS vb.) kullanıyorsanız, üzerinde hello'ı tıklatın **giriş bölgesi bulmayı etkinleştirmek** seçeneği ve hello yapılandırma **etki alanı adı**.
    
    g. İçinde **etki alanı adı** hello etki alanı adını buraya yazın hello ADFS tabanlı oturum açma durumunda.

    h. Denetleme **etkinleştirmek tek oturum kapatma** bir kullanıcı oturum açtığında JIRA Azure AD'den toolog çıkışı isterseniz. 

    ı. Tıklatın **kaydetmek** düğmesini toosave hello ayarları.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>Microsoft test kullanıcı tarafından JIRA SAML SSO oluşturma

tooenable Azure AD kullanıcıların toolog tooJIRA şirket içi Server'da, bunlar JIRA SAML SSO Microsoft tarafından sağlanmalıdır. Microsoft tarafından JIRA SAML SSO için sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour JIRA şirket içi sunucu yönetici olarak oturum.

2. Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. Yeniden yönlendirilen tooAdministrator erişim sayfası tooenter olduğunuz **parola** tıklatıp **Onayla** düğmesi.

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. Altında **kullanıcı yönetimi** bölüm sekmesini tıklatın, **kullanıcı oluşturma**.

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. Merhaba üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    a. Merhaba, **e-posta adresi** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.

    b. Merhaba, **tam adı** metin kutusuna, Britta Simon gibi hello kullanıcının tam adını yazın.

    c. Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.

    d. Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.

    e. Tıklatın **kullanıcı oluşturma**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, Microsoft tarafından SAML SSO erişimi tooJIRA vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooJIRA SAML SSO Microsoft tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **JIRA SAML SSO Microsoft tarafından**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba JIRA SAML SSO hello erişim paneli Microsoft parçasında tarafından tıkladığınızda, otomatik olarak oturum açma tooyour JIRA SAML SSO Microsoft uygulaması tarafından almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

