---
title: "Öğretici: Azure Active Directory Tümleştirme ile Hightail | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Hightail arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Öğretici: Azure Active Directory Tümleştirme Hightail ile

Bu öğreticide, bilgi nasıl toointegrate Hightail Azure Active Directory (Azure AD) ile.

Hightail Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooHightail sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooHightail (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Hightail ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Hightail çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Hightail ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-hightail-from-hello-gallery"></a>Merhaba Galerisi'nden Hightail ekleme
Azure AD'ye tooconfigure hello tümleştirme Hightail, tooadd Hightail hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Hightail hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Hightail**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. Merhaba Sonuçlar panelinde seçin **Hightail**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Hightail sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Hightail içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Hightail hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Hightail içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Hightail ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Hightail test kullanıcısı oluşturma](#creating-a-hightail-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Hightail içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Hightail uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Hightail, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Hightail** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. Merhaba üzerinde **Hightail etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL'si olarak:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE] 
    > Merhaba önceki değeri gerçek değeri değil. Merhaba değeri hello öğreticinin ilerleyen bölümlerinde açıklanan hello gerçek yanıt URL ile güncelleştirir.
 
4. Merhaba üzerinde **Hightail etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    a. Merhaba tıklatın **Göster Gelişmiş URL ayarları**.

    b. Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü hello URL'si olarak:`https://www.hightail.com/loginSSO`

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. Hightail uygulama belirli bir biçimde hello SAML onaylar bekler. Lütfen bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Atrribute"** hello uygulama sekmesinde. Ekran aşağıdaki hello bunun bir örneği gösterir. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ------------------- | -------------------- |
    | FirstName | User.givenName |
    | Soyadı | User.surname |
    | E-posta | User.Mail |    
    | Userıdentity | User.Mail |
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.

    d. Merhaba bırakın **Namespace** boş.
    
    e. **Tamam**’a tıklayın.

7. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. Merhaba üzerinde **Hightail yapılandırma** 'yi tıklatın **yapılandırma Hightail** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    >Çoklu oturum açma Hello Hightail uygulamaya yapılandırmadan önce lütfen beyaz liste Hightail ile e-posta etki alanınızın ekip tüm bu etki alanını kullanan kullanıcılar hello çoklu oturum açma işlevini kullanabilirsiniz.


9. Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour Hightail Kiracı yönetici olarak gerekir.
   
    a. Hello'nde hello üstte, hello menüsünü **hesap** sekmesinde ve seçin **SAML yapılandırmak**.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    b. Hello onay kutusunu seçin **SAML kimlik doğrulamasını etkinleştir**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    c. Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **SAML belirteç imzalama sertifikası** metin kutusu.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    d. Merhaba, **SAML yetkilisi (Kimlik sağlayıcısı)** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalandığından.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    e. Tooconfigure hello uygulamada istiyorsanız **IDP başlatılan modu** seçin **"Kimlik sağlayıcıyı (IDP) başlatılan oturum açma"**. Varsa **SP tarafından başlatılan modu** seçin **"Hizmet sağlayıcısı (SP) başlatılan oturum açma"**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    f. Örneğiniz için Hello SAML tüketici URL'sini kopyalayın ve yapıştırın **yanıt URL'si** metin kutusuna **Hightail etki alanı ve URL'leri** Azure Portal'daki bölümü.
    
    g. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-hightail-test-user"></a>Hightail test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde Hightail adlı bir kullanıcı ' dir. 

Bu bölümde, eylem öğe yok. Yalnızca zaman kullanıcı sağlamayı hello özel taleplere dayanarak destekler hightail. Merhaba özel talep hello bölümünde gösterildiği gibi yapılandırdıysanız  **[yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on)**  yukarıdaki kullanıcı henüz yok hello uygulamada otomatik olarak oluşturulur. 

>[!NOTE]
>Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [Hightail destek ekibi](mailto:support@hightail.com). 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooHightail vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooHightail hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Hightail**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Hightail hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Hightail uygulama almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

