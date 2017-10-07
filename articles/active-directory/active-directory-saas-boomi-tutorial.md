---
title: "Öğretici: Azure Active Directory Tümleştirme ile Boomi | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Boomi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Öğretici: Azure Active Directory Tümleştirme Boomi ile

Bu öğreticide, bilgi nasıl toointegrate Boomi Azure Active Directory'ye (Azure AD).

Boomi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooBoomi sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooBoomi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Boomi ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Boomi çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Boomi ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-boomi-from-hello-gallery"></a>Merhaba Galerisi'nden Boomi ekleme
Azure AD'ye tooconfigure hello tümleştirme Boomi, tooadd Boomi hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Boomi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Boomi**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. Merhaba Sonuçlar panelinde seçin **Boomi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Boomi sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Boomi içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Boomi hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Boomi içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Boomi ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Boomi test kullanıcısı oluşturma](#creating-a-boomi-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Boomi içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Boomi uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Boomi, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Boomi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. Merhaba üzerinde **Boomi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://platform.boomi.com/sso/<accountname>/saml`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [Boomi destek ekibi](https://boomi.com/company/contact/) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Boomi uygulama hello SAML onaylar belirli bir biçimde bekler. Lütfen bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, hello aşağıdaki tabloda, gösterilen her satır için gerçekleştirme adımları izleyerek hello:

    | Öznitelik adı | Öznitelik değeri |
    | -------------- | --------------- |
    | FEDERATION_ID | User.Mail |
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. **Tamam**’a tıklayın.

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **Boomi yapılandırma** 'yi tıklatın **yapılandırma Boomi** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. Farklı web tarayıcısı penceresinde Boomi şirket sitenize yönetici olarak oturum açın. 

9. Çok gidin**şirket adı** ve çok Git**ayarlanan**.

10. Merhaba tıklatın **SSO seçenekleri** sekmesinde ve aşağıdaki adımları gerçekleştirin.

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Denetleme **etkinleştirmek SAML çoklu oturum açma** onay kutusu.

    b. Tıklatın **alma** tooupload hello sertifika çok Azure AD'den indirilen**kimlik sağlayıcısı sertifikası**.
    
    c. Merhaba, **kimlik sağlayıcısı oturum açma URL'si** hello değerini put textbox **SAML çoklu oturum açma hizmet URL'si** Azure AD uygulama yapılandırma penceresinden.

    d. Olarak **Federasyon kimliği konumu**seçin **Federasyon kimliğidir FEDERATION_ID özniteliği öğesinde** radyo düğmesi. 

    e. Tıklatın **kaydetmek** düğmesi.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-boomi-test-user"></a>Boomi test kullanıcısı oluşturma

TooBoomi içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Boomi sağlanmalıdır. Boomi Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:

1. İçinde tooyour Boomi şirket site yönetici olarak oturum açın.

2. Oturum açtıktan sonra çok gidin**kullanıcı yönetimi** ve çok Git**kullanıcılar**.

    ![Kullanıcıların](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "kullanıcılar")

3. Tıklatın ** + ** simgesi ve hello **Ekle/Koru kullanıcı rolleri** iletişim kutusunu açar.

    ![Kullanıcıların](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "kullanıcılar")

    ![Kullanıcıların](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "kullanıcılar")

    a. Merhaba, **kullanıcı e-posta adresi** metin kutusuna, kullanıcının türü hello e-posta ister BrittaSimon@contoso.com.
    
    b. Merhaba, **ad** metin kutusuna, türü hello Britta gibi kullanıcı adı.

    c. Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını Simon gibi.
    
    d. Merhaba kullanıcının girin **Federasyon kimliği**. Her kullanıcının hello kullanıcı hello hesabı içinde benzersiz olarak tanıtan bir Federasyon kimliği olmalıdır.
    
    e. Merhaba atamak **standart kullanıcı** rol toohello kullanıcı. Hello yöneticisi rolü, kendisine normal Atmosfer erişim yanı sıra tek oturum açma erişimini vereceği için atamayın.
    
    f. **Tamam** düğmesine tıklayın.
    
    > [!NOTE]
    > Merhaba kullanıcı parolasını hello kimlik sağlayıcısı olarak yönetildiğinden toohello AtomSphere hesabı içinde kullanılan toolog olabilir bir parola içeren bir Hoş Geldiniz bildirim e-posta alırsınız. API AAD kullanıcı hesaplarının Boomi tooprovision tarafından sağlanan veya herhangi diğer Boomi kullanıcı hesabı oluşturma araçlarını kullanabilir. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooBoomi vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooBoomi hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Boomi**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Boomi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Boomi uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

