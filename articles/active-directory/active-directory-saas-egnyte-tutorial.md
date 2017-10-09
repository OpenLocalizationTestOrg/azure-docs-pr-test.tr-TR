---
title: "Öğretici: Azure Active Directory Tümleştirme ile Egnyte | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Egnyte arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Öğretici: Azure Active Directory Tümleştirme Egnyte ile

Bu öğreticide, bilgi nasıl toointegrate Egnyte Azure Active Directory'ye (Azure AD).

Egnyte Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooEgnyte sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooEgnyte (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Egnyte ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Egnyte çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Egnyte ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-egnyte-from-hello-gallery"></a>Merhaba Galerisi'nden Egnyte ekleme
Azure AD'ye tooconfigure hello tümleştirme Egnyte, tooadd Egnyte hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Egnyte hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Egnyte**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. Merhaba Sonuçlar panelinde seçin **Egnyte**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Egnyte ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Egnyte içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Egnyte hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Egnyte içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Egnyte ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Egnyte test kullanıcısı oluşturma](#creating-an-egnyte-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Egnyte içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Egnyte uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Egnyte, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Egnyte** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. Merhaba üzerinde **Egnyte etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Egnyte istemci destek ekibi](https://www.egnyte.com/corp/contact_egnyte.html) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Egnyte yapılandırma** 'yi tıklatın **yapılandırma Egnyte** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Egnyte şirket sitede yönetici olarak oturum açın.

8. Tıklatın **ayarları**.
   
   ![Ayarları](./media/active-directory-saas-egnyte-tutorial/ic787819.png "ayarları")

9. Merhaba menüye tıklayın **ayarları**.

   ![Ayarları](./media/active-directory-saas-egnyte-tutorial/ic787820.png "ayarları")

10. Merhaba tıklatın **yapılandırma** sekmesini ve ardından **güvenlik**.

    ![Güvenlik](./media/active-directory-saas-egnyte-tutorial/ic787821.png "güvenlik")

11. Merhaba, **çoklu oturum açma kimlik doğrulaması** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açma kimlik doğrulaması](./media/active-directory-saas-egnyte-tutorial/ic787822.png "çoklu oturum açma kimlik doğrulaması")   
    
    a. Olarak **çoklu oturum açma kimlik doğrulaması**seçin **SAML 2.0**.
   
    b. Olarak **kimlik sağlayıcısı**seçin **Azuread'i**.
   
    c. Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello Azure portalından kopyalandığından **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.
   
    d. Yapıştır **SAML varlık kimliği** hello Azure portalından kopyalanan **kimlik sağlayıcısı varlık kimliği** metin kutusu.
      
    e. Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **kimlik sağlayıcısı sertifikası** metin kutusu.
   
    f. Olarak **kullanıcı eşlemesi varsayılan**seçin **e-posta adresi**.
   
    g. Olarak **etki alanına özgü veren değeriyle kullanın**seçin **devre dışı**.
   
    h. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-egnyte-test-user"></a>Bir Egnyte test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooEgnyte bunların Egnyte sağlanması gerekir. Egnyte Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour oturum **Egnyte** yönetici olarak şirket site.

2. Çok Git**ayarları \> kullanıcıları ve grupları**.

3. ' I tıklatın **yeni kullanıcı Ekle**ve ardından hello türünü seçin kullanıcının tooadd istediğiniz.
   
   ![Kullanıcıların](./media/active-directory-saas-egnyte-tutorial/ic787824.png "kullanıcılar")

4. Merhaba, **yeni standart kullanıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![Yeni standart kullanıcı](./media/active-directory-saas-egnyte-tutorial/ic787825.png "yeni standart kullanıcı")   

   a. Türü hello **e-posta**, **kullanıcıadı**ve diğer ayrıntılarını tooprovision istediğiniz geçerli bir Azure Active Directory hesabı.
   
   b. **Kaydet** düğmesine tıklayın.
    
    >[!NOTE]
    >Hello Azure Active Directory hesap sahibi bir bildirim e-posta alacaksınız.
    >

>[!NOTE]
>API AAD kullanıcı hesaplarının Egnyte tooprovision tarafından sağlanan veya herhangi diğer Egnyte kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooEgnyte vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooEgnyte hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Egnyte**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Egnyte hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Egnyte uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

