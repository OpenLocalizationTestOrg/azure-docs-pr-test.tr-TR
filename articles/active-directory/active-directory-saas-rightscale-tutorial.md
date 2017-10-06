---
title: "Öğretici: Azure Active Directory Tümleştirme ile Rightscale | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Rightscale arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Öğretici: Azure Active Directory Tümleştirme Rightscale ile

Bu öğreticide, bilgi nasıl toointegrate Rightscale Azure Active Directory'ye (Azure AD).

Rightscale Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooRightscale sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooRightscale (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Rightscale ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Rightscale çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Rightscale ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-rightscale-from-hello-gallery"></a>Merhaba Galerisi'nden Rightscale ekleme
Azure AD'ye tooconfigure hello tümleştirme Rightscale, tooadd Rightscale hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Rightscale hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Rightscale**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. Merhaba Sonuçlar panelinde seçin **Rightscale**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Rightscale sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Rightscale içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Rightscale hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Rightscale içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Rightscale ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Rightscale test kullanıcısı oluşturma](#creating-a-rightscale-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Rightscale içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Rightscale uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Rightscale, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Rightscale** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. Merhaba üzerinde **Rightscale etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu** hello uygulama zaten Azure ile önceden tümleştirilmiştir, tooperform herhangi bir adım yoktur.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. Merhaba üzerinde **Rightscale etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları**.

    b. Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü hello URL'si:`https://login.rightscale.com/`

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **Rightscale yapılandırma** 'yi tıklatın **yapılandırma Rightscale** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour RightScale Kiracı yönetici olarak gerekir.

    a. Hello'nde hello üstte, hello menüsünü **ayarları** sekmesinde ve seçin **çoklu oturum açma**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Merhaba tıklayın "**yeni**" düğmesine tooadd **bilgisayarınızı SAML kimlik sağlayıcısı**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. Merhaba metin kutusuna **görünen adı**, şirket adınızı girin.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Seçin **izin RightScale tarafından başlatılan SSO'yu bir bulma ipucu kullanarak** ve giriş, **etki alanı adı** metin kutusu altında hello içinde.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Yapıştırma hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan **SAML SSO Endpoint** RightScale içinde.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Yapıştırma hello değerini **SAML varlık kimliği** Azure portalından kopyalanan **SAML Entityıd** RightScale içinde.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Tıklatın **tarayıcı** Azure Portalı'ndan indirilen düğmesi tooupload hello sertifika.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. **Kaydet** düğmesine tıklayın.
<CE>
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-rightscale-test-user"></a>Rightscale test kullanıcısı oluşturma

Bu bölümde, RightScale içinde Britta Simon adlı bir kullanıcı oluşturun. Çalışmak [Rightscale istemci destek ekibi](mailto:support@rightscale.com) tooadd hello kullanıcılar hello RightScale Platform.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooRightscale vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooRightscale hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Rightscale**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.  

Merhaba RightScale hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour RightScale uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

