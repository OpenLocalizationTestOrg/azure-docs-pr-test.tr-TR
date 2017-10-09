---
title: "Öğretici: Müşteri için SAP bulut Azure Active Directory Tümleştirmesi | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve müşteri için SAP bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Öğretici: Müşteri için SAP bulut Azure Active Directory Tümleştirmesi

Bu öğreticide, nasıl toointegrate SAP öğrenmek için Azure Active Directory (Azure AD) ile müşteri bulut.

Azure AD ile müşteri için SAP bulut tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Müşteri için erişim tooSAP bulut olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına (çoklu oturum açma) müşteri için kullanıcılar tooautomatically get açan tooSAP bulut etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure müşteri için SAP bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- SAP Bulutu müşteri çoklu oturum açma için abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAP bulut müşteri için hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>SAP bulut müşteri için hello Galerisi'nden ekleme
Azure AD'ye müşteri için tooconfigure hello tümleştirme SAP bulutun tooadd SAP bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları için müşteri gerekir.

**tooadd hello galerisinden müşteri için SAP bulut hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **müşteri için SAP bulut**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. Merhaba Sonuçlar panelinde seçin **müşteri için SAP bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SAP bulut ile "Britta Simon" adlı bir test kullanıcıya bağlı müşteri için test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen müşteri için SAP bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve müşteri için SAP bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri müşteri SAP buluta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açma ile test SAP bulut müşteri için yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Müşteri test kullanıcısı için bir SAP bulut oluşturma](#creating-a-sap-cloud-for-customer-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir müşteri için SAP bulutta, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve SAP bulut müşteri uygulaması için çoklu oturum açmayı yapılandırın.

**Müşteri, SAP bulut ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **müşteri için SAP bulut** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. Merhaba üzerinde **müşteri etki alanı ve URL'ler için SAP bulut** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server name>.crm.ondemand.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [müşteri istemci destek ekibi için SAP bulut](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget bu değerleri. 

4. Merhaba üzerinde **kullanıcı öznitelikleri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. İçinde **kullanıcı tanımlayıcısı** listesi, select hello **ExtractMailPrefix()** işlevi.

    b. Merhaba gelen **posta** listesi, uygulamanız için kullanmak istediğiniz toouse select hello kullanıcı özniteliği.
    Örneğin, toouse hello benzersiz kullanıcı tanımlayıcısı olarak EmployeeID istiyorsanız ve hello ExtensionAttribute2 hello öznitelik değeri depoladığınız ardından user.extensionattribute2 seçin.  

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **müşteri yapılandırması için SAP bulut** 'yi tıklatın **müşteri için SAP bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget yapılandırılmış, SSO hello aşağıdaki adımları gerçekleştirin:
   
    a. Müşteri portalı yönetici haklarıyla oturum açma SAP buluta.
   
    b. Toohello gidin **uygulama ve kullanıcı yönetimi görevinin** hello tıklatıp **kimlik sağlayıcısı** sekmesi.
   
    c. Tıklatın **yeni kimlik sağlayıcısı** ve select hello meta veri XML dosyası hello Azure portal ' indirilir. Merhaba meta verileri içe aktararak hello sistem otomatik olarak hello gerekli imza sertifikası ve şifreleme sertifikası karşıya yükleme.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory hello SAML isteği onaylama tüketici hizmeti URL'si öğesinde hello gerektirir, bu nedenle hello seçin **onaylama tüketici hizmeti URL'si dahil** onay kutusu.
   
    e. Tıklatın **çoklu oturum açmayı etkinleştirme**.
   
    f. Yaptığınız değişiklikleri kaydedin.
   
    g. Merhaba tıklatın **My sistem** sekmesi.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. İçinde **Azure AD oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    ı. Kullanıcı kimliği ve parola veya SSO ile Merhaba seçerek oturum açma arasında Hello çalışan el ile seçip seçemeyeceğini belirtin **el ile kimlik sağlayıcısı seçimi**.
   
    j. Merhaba, **SSO URL** bölümünde, çalışanların toosign toohello sistemde tarafından kullanılması gereken hello URL'sini belirtin. 
    Merhaba, **URL gönderilen tooEmployee** listesinde, aşağıdaki seçenekleri şu hello arasında seçim yapabilir:
   
    **SSO olmayan URL'si**
   
    Merhaba sistemi yalnızca hello normal sistem URL toohello çalışan gönderir. Hello çalışan olamaz SSO kullanarak oturum açın ve parolayı kullanın veya gerekir bunun yerine sertifika.
   
    **SSO URL'Sİ** 
   
    Merhaba sistemi yalnızca hello SSO URL toohello çalışan gönderir. Merhaba çalışan SSO kullanarak oturum açabilir. Kimlik doğrulama isteği IDP hello yönlendirilir.
   
    **Otomatik Seçim**
   
    SSO etkin değilse, hello sistem hello normal sistem URL toohello çalışan gönderir. SSO etkin değilse, hello sistem hello çalışan bir parolaya sahip olup olmadığını denetler. Bir parola kullanılabilir durumdaysa, SSO URL'si ve olmayan SSO URL'si toohello çalışan gönderilir. Bununla birlikte, Hello çalışan parolası yoksa, yalnızca hello SSO URL toohello çalışan gönderilir.
   
    k. Yaptığınız değişiklikleri kaydedin.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Müşteri test kullanıcısı için bir SAP bulut oluşturma

Bu bölümde, Britta Simon SAP bulutta müşteri için adlı bir kullanıcı oluşturun. Lütfen çalışmak [müşteri destek ekibi için SAP bulut](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) hello SAP bulut müşteri platform için tooadd hello kullanıcılar. 

> [!NOTE]
> Lütfen NameID değeri hello SAP bulut müşteri platform için hello kullanıcıadı alanıyla eşleşmelidir emin olun.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, müşteri için erişim tooSAP bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSAP müşteri için bulut hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **müşteri için SAP bulut**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba SAP bulut hello erişim paneli müşteri parçasında tıkladığınızda, müşteri uygulaması için otomatik olarak imzalanmış üzerinde SAP bulut tooyour almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

