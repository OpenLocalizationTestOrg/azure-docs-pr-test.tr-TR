---
title: "Öğretici: Azure Active Directory Tümleştirme ile Samanage | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Samanage arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Öğretici: Azure Active Directory Tümleştirme Samanage ile

Bu öğreticide, bilgi nasıl toointegrate Samanage Azure Active Directory'ye (Azure AD).

Samanage Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSamanage sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSamanage (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Samanage ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Samanage çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Samanage ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-samanage-from-hello-gallery"></a>Merhaba Galerisi'nden Samanage ekleme
Azure AD'ye tooconfigure hello tümleştirme Samanage, tooadd Samanage hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Samanage hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Samanage**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. Merhaba Sonuçlar panelinde seçin **Samanage**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Samanage sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Samanage içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Samanage hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Samanage içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Samanage ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Samanage test kullanıcısı oluşturma](#creating-a-samanage-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Samanage içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Samanage uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Samanage, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Samanage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. Merhaba üzerinde **Samanage etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerler, oturum açma hello gerçek URL'si ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcısı ile güncelleştirin. Daha fazla ayrıntı başvurun [Samanage istemci destek ekibi](https://www.samanage.com/support).    
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Samanage yapılandırma** 'yi tıklatın **yapılandırma Samanage** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. Farklı web tarayıcısı penceresinde Samanage şirket sitenize yönetici olarak oturum açın.

8. Tıklatın **Pano** seçip **Kurulum** sol gezinti bölmesindeki.
   
    ![Pano](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Panosu")

9. Tıklatın **çoklu oturum açma**.
   
    ![Çoklu oturum açma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "çoklu oturum açma")

10. Çok gidin**SAML kullanarak oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML kullanarak oturum açma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "SAML ile oturum açın")
 
    a. Tıklatın **çoklu oturum açmayı etkinleştir SAML ile**.  
 
    b. Merhaba, **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.    
 
    c. Merhaba onaylayın **oturum açma URL'si** eşleşmeleri hello **oturum üzerinde URL'si** , **Samanage etki alanı ve URL'leri** Azure portalı bölümünde.
 
    d. Merhaba, **oturum kapatma URL'si** metin kutusuna, hello değeri girin **Sign-Out URL** Azure portalından kopyalanan.
 
    e. Merhaba, **SAML veren** metin kutusuna, türü hello uygulama kimliği URI kimlik sağlayıcınızı ayarlayın.
 
    f. Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, base-64 kodlanmış sertifikasını açın ve ardından toohello yapıştırın **, kimlik sağlayıcısı x.509 sertifika aşağıdaki Yapıştır** metin kutusu.
 
    g. Tıklatın **Samanage içinde yoksa, kullanıcılar oluşturma**.
 
    h. Tıklatın **güncelleştirme**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-samanage-test-user"></a>Samanage test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooSamanage bunların Samanage sağlanması gerekir.  
Samanage Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. Samanage şirket sitenize yönetici olarak oturum açın.

2. Tıklatın **Pano** seçip **Kurulum** sol gezinti bölmesinde.
   
    ![Kurulum](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Kurulumu")

3. Merhaba tıklatın **kullanıcılar** sekmesi
   
    ![Kullanıcıların](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "kullanıcılar")

4. Tıklatın **yeni kullanıcı**.
   
    ![Yeni kullanıcı](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "yeni kullanıcı")

5. Türü hello **adı** ve hello **e-posta adresi** tooprovision istediğiniz bir Azure Active Directory hesabının **kullanıcı oluşturma**.
   
    ![Kullanıcı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "kullanıcı oluştur")
   
   >[!NOTE]
   >Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin. API, kullanıcı hesaplarını Samanage tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer Samanage kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSamanage vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSamanage hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Samanage**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Samanage hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Samanage uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

