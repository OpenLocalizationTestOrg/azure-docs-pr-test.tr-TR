---
title: "Öğretici: Azure Active Directory Tümleştirme ile Syncplicity | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Syncplicity arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>Öğretici: Syncplicity Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Syncplicity Azure Active Directory'ye (Azure AD).

Syncplicity Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSyncplicity sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSyncplicity (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Syncplicity ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Syncplicity çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Syncplicity hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-syncplicity-from-hello-gallery"></a>Syncplicity hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Syncplicity, tooadd Syncplicity hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Syncplicity hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Syncplicity**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. Merhaba Sonuçlar panelinde seçin **Syncplicity**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Syncplicity ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Syncplicity içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Syncplicity hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Syncplicity içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Syncplicity ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Syncplicity test kullanıcısı oluşturma](#creating-a-syncplicity-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Syncplicity içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Syncplicity uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Syncplicity, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Syncplicity** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. Merhaba üzerinde **Syncplicity etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.syncplicity.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Syncplicity istemci destek ekibi](https://www.syncplicity.com/contact-us) tooget bu değerleri. 
 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Syncplicity yapılandırma** 'yi tıklatın **yapılandırma Syncplicity** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. İçinde tooyour oturum **Syncplicity** Kiracı.

8. Hello içinde hello üst menüsünde **yönetici**seçin **ayarları**ve ardından **özel etki alanı ve çoklu oturum açma**.
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. Merhaba üzerinde **çoklu oturum açma (SSO)** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    a. Merhaba, **özel etki alanı** metin kutusuna, etki alanınızın türü hello adı.
  
    b. Seçin **etkin** olarak **tek oturum açma durumu**.

    c. Merhaba, **varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.

    d. Merhaba, **oturum açma sayfası URL'si** metin kutusuna, Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    e. Merhaba, **oturum kapatma sayfası URL'si** metin kutusuna, Yapıştır hello **Sign-Out URL** Azure portalından kopyalanan.

    f. İçinde **kimlik sağlayıcısı sertifikası**, tıklatın **dosya**ve hello Azure portal ' indirilen hello sertifikasını karşıya yükleyin. 

    g. Tıklatın **değişiklikleri kaydetme**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-syncplicity-test-user"></a>Syncplicity test kullanıcısı oluşturma
AAD kullanıcılar toobe mümkün toosign için bunların sağlanan tooSyncplicity uygulama olması gerekir. Bu bölümde, nasıl Syncplicity içinde toocreate AAD kullanıcı hesapları açıklanmaktadır.

**bir kullanıcı hesabı tooSyncplicity tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Syncplicity** Kiracı (örneğin: `https://company.Syncplicity.com`).

2. Tıklatın **yönetici** seçip **kullanıcı hesaplarını**.

3. Tıklatın **kullanıcı ekleme**.
   
    ![Kullanıcıları yönetme](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "kullanıcıları yönetme")

4. Türü hello **e-posta addressess** tooprovision, select istediğiniz bir AAD hesabın **kullanıcı** olarak **rol**ve ardından **sonraki**.
   
    ![Hesap bilgileri](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "hesap bilgileri")
   
    >[!NOTE]
    >Merhaba AAD hesap sahibi bağlantı tooconfirm dahil olmak üzere bir e-posta alır ve hello hesabını etkinleştirebilir. 
    > 

5. Yeni kullanıcı bir üyesi haline gelir ve ardından, şirketinizde bir grup seçin **sonraki**.
   
    ![Grup üyelikleri](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "grup üyelikleri")
   
    >[!NOTE]
    >Listelenen hiçbir grup varsa tıklatın **sonraki**. 
    > 

6. Merhaba kullanıcının bilgisayarındaki Syncplicity'nın denetimindeki tooplace ister ve ardından hello klasörleri seçin **sonraki**.
   
    ![Syncplicity klasörleri](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity klasörleri")

>[!NOTE]
>API AAD kullanıcı hesaplarının Syncplicity tooprovision tarafından sağlanan veya herhangi diğer Syncplicity kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSyncplicity vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSyncplicity hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Syncplicity**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Syncplicity hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Syncplicity uygulama almanız gerekir.
## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

