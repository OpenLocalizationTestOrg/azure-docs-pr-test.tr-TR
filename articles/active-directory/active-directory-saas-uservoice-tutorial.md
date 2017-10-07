---
title: "Öğretici: Azure Active Directory Tümleştirme ile UserVoice | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile UserVoice arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Öğretici: Azure Active Directory Tümleştirme UserVoice ile

Bu öğreticide, bilgi nasıl toointegrate UserVoice Azure Active Directory'ye (Azure AD).

UserVoice Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooUserVoice sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooUserVoice (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure UserVoice ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir UserVoice çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. UserVoice hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-uservoice-from-hello-gallery"></a>UserVoice hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme UserVoice, tooadd UserVoice hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd UserVoice hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **UserVoice**seçin **UserVoice** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![UserVoice hello sonuçları listesinde](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UserVoice sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen UserVoice içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı UserVoice hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

UserVoice içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve UserVoice ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[UserVoice test kullanıcısı oluşturma](#create-a-uservoice-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir UserVoice içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma UserVoice uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile UserVoice, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **UserVoice** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. Merhaba üzerinde **UserVoice etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![UserVoice etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.UserVoice.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.UserVoice.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [UserVoice istemci destek ekibi](https://www.uservoice.com/) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **UserVoice yapılandırma** 'yi tıklatın **yapılandırma UserVoice** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![UserVoice yapılandırma](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour UserVoice şirket sitede yönetici olarak oturum açın.

8. Merhaba üstte Hello araç çubuğunda **ayarları**ve ardından **Web portalı** hello menüsünde.
   
    ![Uygulama tarafında ayarları bölümünde](./media/active-directory-saas-uservoice-tutorial/ic777519.png "ayarları")

9. Merhaba üzerinde **Web portalı** sekmede hello **kullanıcı kimlik doğrulaması** 'yi tıklatın **Düzenle** tooopen hello **kullanıcı kimlik doğrulamasını Düzenle** iletişim Sayfa.
   
    ![Web portalı sekmesini](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portalı")

10. Merhaba üzerinde **kullanıcı kimlik doğrulamasını Düzenle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı kimlik doğrulamasını Düzenle](./media/active-directory-saas-uservoice-tutorial/ic777521.png "düzenleme kullanıcı kimlik doğrulaması")
   
    a. Tıklatın **çoklu oturum açma (SSO)**.
 
    b. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **SSO uzaktan oturum açma** metin kutusu.

    c. Yapıştır hello **Sign-Out URL** hello hello Azure portal ' kopyaladığınız değeri **SSO uzak Sign-Out textbox**.
 
    d. Yapıştır hello **parmak izi** Azure portalından kopyaladığınız değeri **geçerli SHA1 sertifika parmak izi** metin kutusu.
    
    e. Tıklatın **kimlik doğrulama ayarlarını Kaydet**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-uservoice-test-user"></a>UserVoice test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooUserVoice bunların UserVoice sağlanması gerekir. UserVoice Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:
1. İçinde tooyour oturum **UserVoice** Kiracı.

2. Çok Git**ayarları**.
   
    ![Ayarları](./media/active-directory-saas-uservoice-tutorial/ic777811.png "ayarları")

3. Tıklatın **genel**.

4. Tıklatın **aracıları ve izinleri**.
   
    ![Aracılar ve izinleri](./media/active-directory-saas-uservoice-tutorial/ic777812.png "aracıları ve izinleri")

5. Tıklatın **yöneticileri ekleyin**.
   
    ![Yöneticileri ekleyin](./media/active-directory-saas-uservoice-tutorial/ic777813.png "yöneticileri ekleyin")

6. Merhaba üzerinde **davet admins** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yöneticileri davet](./media/active-directory-saas-uservoice-tutorial/ic777814.png "davet yöneticileri")
   
    a. Merhaba e-postaları metin kutusuna tooprovision istediğiniz ve ardından hello hesap hello e-posta adresini yazın **Ekle**.
   
    b. Tıklatın **davet**.

> [!NOTE]
> API AAD kullanıcı hesaplarının UserVoice tooprovision tarafından sağlanan veya herhangi diğer UserVoice kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooUserVoice vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooUserVoice hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **UserVoice**.

    ![Merhaba UserVoice bağlantı hello uygulamalar listesinde](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba UserVoice hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour UserVoice uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

