---
title: "Öğretici: SAP Business ByDesign Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SAP Business ByDesign arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Öğretici: SAP Business ByDesign ile Azure Active Directory tümleştirme

Bu öğreticide, nasıl toointegrate SAP öğrenin iş ByDesign Azure Active Directory'ye (Azure AD).

SAP Business ByDesign Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSAP iş ByDesign sahip Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooSAP iş ByDesign (çoklu oturum açma) etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

SAP Business ByDesign ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir SAP Business ByDesign çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAP Business ByDesign hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>SAP Business ByDesign hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme SAP Business ByDesign, tooadd SAP Business ByDesign hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**SAP Business ByDesign hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **SAP Business ByDesign**seçin **SAP Business ByDesign** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![SAP Business ByDesign hello sonuçları listesinde](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SAP Business "Britta Simon" adlı bir test kullanıcı tabanlı ByDesign ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen SAP Business ByDesign içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP Business ByDesign hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.

SAP Business ByDesign içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve SAP Business ByDesign ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SAP Business ByDesign test kullanıcısı oluşturma](#create-an-sap-business-bydesign-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SAP Business ByDesign içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SAP Business ByDesign uygulamanızda yapılandırın.

**SAP Business ByDesign ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **SAP Business ByDesign** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. Merhaba üzerinde **SAP Business ByDesign etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![SAP Business ByDesign etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.sapbydesign.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [SAP Business ByDesign istemci destek ekibi](https://www.sap.com/products/cloud-analytics.support.html) tooget bu değerleri.

4. Merhaba üzerinde **kullanıcı öznitelikleri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![SAP Business ByDesign özniteliği bölümü](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. İçinde **kullanıcı tanımlayıcısı** listesi, select hello **ExtractMailPrefix()** işlevi.
    
    b. Merhaba gelen **posta** listesi, uygulamanız için kullanmak istediğiniz toouse select hello kullanıcı özniteliği. Örneğin, toouse hello benzersiz kullanıcı tanımlayıcısı olarak EmployeeID istiyorsanız ve hello ExtensionAttribute2 hello öznitelik değeri depoladığınız ardından user.extensionattribute2 seçin.   

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **SAP Business ByDesign yapılandırma** 'yi tıklatın **yapılandırma SAP Business ByDesign** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![SAP Business ByDesign yapılandırma](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget uygulamanız için yapılandırılmış SSO hello aşağıdaki adımları gerçekleştirin:
   
    a. Yönetici haklarıyla tooyour SAP Business ByDesign Portal'da oturum açın.
   
    b. Çok gidin**uygulama ve kullanıcı yönetimi görevinin** hello tıklatıp **kimlik sağlayıcısı** sekmesi.
   
    c. Tıklatın **yeni kimlik sağlayıcısı** ve hello Azure portal ' indirmiş select hello meta veri XML dosyası. Merhaba meta verileri içe aktararak hello sistem otomatik olarak hello gerekli imza sertifikası ve şifreleme sertifikası karşıya yükleme.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. tooinclude hello **onaylama tüketici hizmeti URL'si** hello SAML isteği seçin **onaylama tüketici hizmeti URL'si dahil**.
   
    e. Tıklatın **çoklu oturum açmayı etkinleştirme**.
   
    f. Yaptığınız değişiklikleri kaydedin.
   
    g. Merhaba tıklatın **My sistem** sekmesi.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hangi hello Azure portal ' Merhaba, kopyaladığınız **Azure AD oturum açma URL'si** metin kutusu.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    ı. Kullanıcı kimliği ve parola veya SSO ile seçerek oturum açma arasında Hello çalışan el ile seçip seçemeyeceğini belirtin **el ile kimlik sağlayıcısı seçimi**.
   
    j. Merhaba, **SSO URL** bölümünde, hello çalışan toologon toohello sistem tarafından kullanılması gereken hello URL'sini belirtin. 
    Hello URL gönderilen tooEmployee açılır listesinde, aşağıdaki seçenekleri şu hello arasında seçim yapabilirsiniz:
   
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

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>SAP Business ByDesign test kullanıcısı oluşturma

Bu bölümde, SAP Business ByDesign Britta Simon adlı bir kullanıcı oluşturun. Lütfen çalışmak [SAP Business ByDesign istemci destek ekibi](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello kullanıcılar hello SAP Business ByDesign Platform. 

> [!NOTE]
> Lütfen NameID değeri hello SAP Business ByDesign platform hello kullanıcıadı alanıyla eşleşmelidir emin olun.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooSAP iş ByDesign vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooSAP iş ByDesign hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SAP Business ByDesign**.

    ![Merhaba SAP Business ByDesign bağlantı hello uygulamalar listesinde](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba SAP Business ByDesign hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SAP Business ByDesign uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

