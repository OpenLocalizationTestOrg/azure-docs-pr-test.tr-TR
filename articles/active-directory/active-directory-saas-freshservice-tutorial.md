---
title: "Öğretici: Azure Active Directory Tümleştirme ile Freshservice | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Freshservice arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a>Öğretici: Azure Active Directory Tümleştirme Freshservice ile

Bu öğreticide, bilgi nasıl toointegrate Freshservice Azure Active Directory'ye (Azure AD).

Freshservice Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooFreshservice sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooFreshservice (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Freshservice ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Freshservice çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Freshservice ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-freshservice-from-hello-gallery"></a>Merhaba Galerisi'nden Freshservice ekleme
Azure AD'ye tooconfigure hello tümleştirme Freshservice, tooadd Freshservice hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Freshservice hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Freshservice**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. Merhaba Sonuçlar panelinde seçin **Freshservice**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Freshservice sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Freshservice içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Freshservice hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Freshservice içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Freshservice ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Freshservice test kullanıcısı oluşturma](#creating-a-freshservice-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Freshservice içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Freshservice uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Freshservice, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Freshservice** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. Merhaba üzerinde **Freshservice etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<democompany>.freshservice.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<democompany>.freshservice.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Freshservice istemci destek ekibi](https://support.freshservice.com/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Freshservice yapılandırma** 'yi tıklatın **yapılandırma Freshservice** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Freshservice şirket sitede yönetici olarak oturum açın.

8. Hello içinde hello üst menüsünde **yönetici**.
   
    ![Yönetici](./media/active-directory-saas-freshservice-tutorial/ic790814.png "yönetici")

9. Merhaba, **müşteri portalı**, tıklatın **güvenlik**.
   
    ![Güvenlik](./media/active-directory-saas-freshservice-tutorial/ic790815.png "güvenlik")

10. Merhaba, **güvenlik** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı](./media/active-directory-saas-freshservice-tutorial/ic790816.png "çoklu oturum açmayı")
   
    a. Anahtar **çoklu oturum açmayı**.

    b. Seçin **SAML SSO**.

    c. Merhaba, **SAML oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    d. Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.

    e. İçinde **güvenlik sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak İZİ** Azure portalından kopyaladığınız sertifika değeri.

    f. Tıklatın **Kaydet**
   
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-freshservice-test-user"></a>Freshservice test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooFreshService bunların FreshService sağlanması gerekir. FreshService Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **FreshService** yönetici olarak şirket site.

2. Hello içinde hello üst menüsünde **yönetici**.
   
    ![Yönetici](./media/active-directory-saas-freshservice-tutorial/ic790814.png "yönetici")

3. Merhaba, **kullanıcı yönetimi** 'yi tıklatın **sahiplerini**.
   
    ![Sahiplerini](./media/active-directory-saas-freshservice-tutorial/ic790818.png "sahiplerini")

4. Tıklatın **yeni istek**.
   
    ![Yeni sahiplerini](./media/active-directory-saas-freshservice-tutorial/ic790819.png "yeni sahiplerini")

5. Merhaba, **yeni istek** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni İstek](./media/active-directory-saas-freshservice-tutorial/ic790820.png "yeni istek")   

    a. Merhaba girin **ad** ve **e-posta** hello tooprovision istediğiniz geçerli bir Azure Active Directory hesabı özniteliklerini ilgili metin kutuları.

    b. **Kaydet** düğmesine tıklayın.
   
    >[!NOTE]
    >Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabı da dahil olmak üzere bir e-posta alır
    >  

>[!NOTE]
>API AAD kullanıcı hesaplarının FreshService tooprovision tarafından sağlanan veya herhangi diğer FreshService kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
>  

![Kullanıcı atama][200] 

**tooassign Britta Simon tooFreshservice hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Freshservice**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Freshservice hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Freshservice uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

