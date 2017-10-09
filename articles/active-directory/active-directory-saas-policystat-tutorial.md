---
title: "Öğretici: Azure Active Directory Tümleştirme ile PolicyStat | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PolicyStat arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Öğretici: Azure Active Directory Tümleştirme PolicyStat ile

Bu öğreticide, bilgi nasıl toointegrate PolicyStat Azure Active Directory'ye (Azure AD).

PolicyStat Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooPolicyStat sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooPolicyStat (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure PolicyStat ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir PolicyStat çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden PolicyStat ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-policystat-from-hello-gallery"></a>Merhaba Galerisi'nden PolicyStat ekleme
Azure AD'ye tooconfigure hello tümleştirme PolicyStat, tooadd PolicyStat hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd PolicyStat hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **PolicyStat**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. Merhaba Sonuçlar panelinde seçin **PolicyStat**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PolicyStat sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen PolicyStat içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PolicyStat hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri PolicyStat içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve PolicyStat ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[PolicyStat test kullanıcısı oluşturma](#creating-a-policystat-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir PolicyStat içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma PolicyStat uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile PolicyStat, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **PolicyStat** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. Merhaba üzerinde **PolicyStat etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.policystat.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [PolicyStat istemci destek ekibi](http://www.policystat.com/support/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooPolicyStat Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.

    Merhaba PolicyStat uygulama bekliyor hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, **SAML belirteci öznitelikleri** yapılandırma.  

     Aşağıdaki ekran görüntüsü hello bunun bir örneğini gösterir.

     ![Öznitelikleri](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "öznitelikleri")

6. tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:

    | Öznitelik adı    |   Öznitelik değeri |
    |------------------- | -------------------- |
    | Kullanıcı Kimliği | ExtractMailPrefix([mail]) |
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. Merhaba, **öznitelik adı** metin kutusuna, türü **uid**.

    c. Merhaba, **öznitelik değeri** metin kutusuna, select **ExtractMailPrefix()**.    
   
    d. Merhaba gelen **posta** listesinde **User.mail**.
    
    e. Tıklatın **Tamam**

7. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. Farklı web tarayıcısı penceresinde PolicyStat şirket sitenize yönetici olarak oturum açın.

9. Merhaba tıklatın **yönetici** sekmesini ve ardından **tek oturum açma yapılandırması** sol gezinti bölmesindeki.
   
    ![Yönetici menü](./media/active-directory-saas-policystat-tutorial/ic808633.png "yönetici menüsü")

10. Merhaba, **Kurulum** bölümünde, select **oturum açmayı etkinleştir tek tümleştirme**.
   
    ![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808634.png "tek oturum açma yapılandırması")

11. Tıklatın **öznitelikleri yapılandırma**ve ardından hello **öznitelikleri yapılandırma** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808635.png "tek oturum açma yapılandırması")
   
    a. Merhaba, **Username özniteliği** metin kutusuna, türü **uid**.

    b. Merhaba, **ad özniteliği** metin kutusuna, türü **firstname** kullanıcının **Britta**.

    c. Merhaba, **son Name özniteliği** metin kutusuna, türü **lastname** kullanıcının **Simon**.

    d. Merhaba, **e-posta özniteliği** metin kutusuna, türü **emailaddress** kullanıcının  **BrittaSimon@contoso.com** .

    e. Tıklatın **değişiklikleri kaydetmek**.

12. Tıklatın **bilgisayarınızı IDP meta veri**ve ardından hello **bilgisayarınızı IDP meta veri** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808636.png "tek oturum açma yapılandırması")
   
    a. İndirilen meta veri dosyası, içerik kopyalama hello açın ve hello yapıştırma **bilgisayarınızı kimlik sağlayıcısı meta verileri** metin kutusu.

    b. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-policystat-test-user"></a>PolicyStat test kullanıcısı oluşturma

PolicyStat içine sipariş tooenable Azure AD kullanıcıların toolog bunların PolicyStat sağlanmalıdır.  

Yalnızca zaman sağlama kullanıcı PolicyStat destekler. Yani, gereksinim tooadd hello kullanıcıları el ile tooPolicyStat. Merhaba kullanıcılar kendi ilk oturum açma SSO aracılığıyla üzerinde otomatik olarak eklenir.

>[!NOTE]
>API'leri, Azure AD kullanıcı hesapları PolicyStat tooprovision tarafından sağlanan veya herhangi diğer PolicyStat kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooPolicyStat vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooPolicyStat hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **PolicyStat**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba PolicyStat hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour PolicyStat uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

