---
title: "Öğretici: Azure Active Directory Tümleştirme ile Sprinklr | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Sprinklr arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Öğretici: Azure Active Directory Tümleştirme Sprinklr ile

Bu öğreticide, bilgi nasıl toointegrate Sprinklr Azure Active Directory'ye (Azure AD).

Sprinklr Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSprinklr sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSprinklr (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Sprinklr ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Sprinklr çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Sprinklr ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sprinklr-from-hello-gallery"></a>Merhaba Galerisi'nden Sprinklr ekleme
Azure AD'ye tooconfigure hello tümleştirme Sprinklr, tooadd Sprinklr hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Sprinklr hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Sprinklr**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. Merhaba Sonuçlar panelinde seçin **Sprinklr**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Sprinklr ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Sprinklr içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Sprinklr hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Sprinklr içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Sprinklr ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Sprinklr test kullanıcısı oluşturma](#creating-a-sprinklr-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Sprinklr içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Sprinklr uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Sprinklr, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Sprinklr** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. Merhaba üzerinde **Sprinklr etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.sprinklr.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Merhaba değeri ile Merhaba güncelleştirin gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Sprinklr istemci destek ekibi](https://www.sprinklr.com/contact-us/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Sprinklr yapılandırma** 'yi tıklatın **yapılandırma Sprinklr** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

7. Farklı web tarayıcısı penceresinde tooyour Sprinklr şirket sitede yönetici olarak oturum açın.

8. Çok Git**Yönetim \> ayarları**.
   
    ![Yönetim](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Yönetim")

9. Çok Git**iş ortağı yönetme \> çoklu oturum açma** üzerinde hello sol bölmesinden.
   
    ![İş ortağı yönetme](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "iş ortağı yönetme")

10. Tıklatın **+ çoklu oturum açmaların eklemek**.
   
    ![Çoklu oturum açmaların](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "çoklu oturum açmaların")

11. Merhaba üzerinde **çoklu oturum açma** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmaların](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "çoklu oturum açmaların")

    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: *WAADSSOTest*).

    b. Seçin **etkin**.

    c. Seçin **yeni SSO sertifikayı kullanmak**.
             
    e. Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **kimlik sağlayıcısı sertifikası** metin kutusu.

    f. Yapıştır hello **SAML varlık kimliği** hello Azure portalından kopyalandığından değeri **varlık kimliği** metin kutusu.

    g. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello Azure portalından kopyalandığından değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.

    h. Yapıştır hello **Sign-Out URL** hello Azure portalından kopyalandığından değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.
     
    ı. Olarak **SAML kullanıcı kimliği türü**seçin **onaylamayı içeren kullanıcı "s sprinklr.com kullanıcıadı**.

    j. Olarak **SAML kullanıcı kimliği konumu**seçin **kullanıcı kimliğidir hello ad tanımlayıcısı öğesinde hello konu deyimi**.

    k. **Kaydet** düğmesine tıklayın.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sprinklr-test-user"></a>Sprinklr test kullanıcısı oluşturma

1. İçinde tooyour Sprinklr şirket site yönetici olarak oturum açın.

2. Çok Git**Yönetim \> ayarları**.
   
    ![Yönetim](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Yönetim")

3. Çok Git**yönetmek istemci \> kullanıcılar** hello sol bölmesinden.
   
    ![Ayarları](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "ayarları")

4. Tıklatın **kullanıcı ekleme**.
   
    ![Ayarları](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "ayarları")

5. Merhaba üzerinde **düzenleme kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı düzenleme](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "düzenleme kullanıcı") 

    a. Merhaba, **e-posta**, **ad** ve **Soyadı** metin kutuları, tooprovision istediğiniz bir Azure AD kullanıcı hesabının türü hello bilgileri.

    b. Seçin **parola devre dışı**.

    c. Seçin **dil**.

    d. Seçin **kullanıcı türü**.

    e. Tıklatın **güncelleştirme**.
   
     >[!IMPORTANT]
     >**Parola devre dışı** seçili tooenable içinde kullanıcı toolog bir kimlik sağlayıcısı aracılığıyla olması gerekir. 
     
6. Çok Git**rol**ve ardından hello aşağıdaki adımları gerçekleştirin:
   
    ![İş ortağı rolleri](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "ortak rolleri")

    a. Merhaba gelen **Global** listesinde **tüm\_izinleri**.  

    b. Tıklatın **güncelleştirme**.

>[!NOTE]
>API'leri, Azure AD kullanıcı hesapları Sprinklr tooprovision tarafından sağlanan veya herhangi diğer Sprinklr kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSprinklr vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSprinklr hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Sprinklr**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Sprinklr hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Sprinklr uygulama hello erişim paneli hakkında daha fazla bilgi almak, bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

