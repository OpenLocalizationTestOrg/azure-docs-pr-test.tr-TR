---
title: "Öğretici: Azure Active Directory Tümleştirme Rally yazılımı ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Rally yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Öğretici: Azure Active Directory Tümleştirme Rally yazılımı

Bu öğreticide, bilgi nasıl toointegrate Rally yazılımı Azure Active Directory'ye (Azure AD).

RALLY yazılımı Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooRally yazılım sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooRally yazılım (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Rally yazılımı ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Rally yazılımı çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. RALLY yazılımı hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-rally-software-from-hello-gallery"></a>RALLY yazılımı hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Rally yazılımı tooadd Rally yazılımı hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Rally yazılımı hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Rally yazılımı**seçin **Rally yazılımı** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçlar listesinde rally yazılımı](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırmak ve yazılım Rally "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Rally yazılım tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Rally yazılımı hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

RALLY yazılımı hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Rally yazılımı ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Rally yazılımı test kullanıcısı oluşturma](#create-a-rally-software-test-user)**  -toohave Britta Simon Rally kullanıcı bağlantılı toohello Azure AD gösterimidir yazılım, karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Rally yazılımı uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Rally yazılımı ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Rally yazılımı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. Merhaba üzerinde **Rally yazılımı etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Rally yazılımı etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.rally.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.rally.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Rally yazılımı istemci destek ekibi](https://help.rallydev.com/) tooget bu değerleri. 
 


4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Rally yazılımı Yapılandırması** 'yi tıklatın **Rally yazılımı Yapılandır** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**

    ![Rally yazılımı yapılandırması](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. İçinde tooyour oturum **Rally yazılımı** Kiracı.

8. Merhaba üstte Hello araç çubuğunda **Kurulum**ve ardından **abonelik**.
   
    ![Abonelik](./media/active-directory-saas-rally-software-tutorial/ic769531.png "abonelik")

9. Merhaba tıklatın **eylem** düğmesi. Seçin **Düzenle abonelik** hello üst sağ tarafında hello araç.

10. Merhaba üzerinde **abonelik** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **Kaydet ve Kapat**:
   
    ![Kimlik doğrulama](./media/active-directory-saas-rally-software-tutorial/ic769542.png "kimlik doğrulaması")
   
    a. Seçin **yarışı veya SSO kimlik doğrulaması** gelen kimlik doğrulama açılır.

    b. Merhaba, **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan. 

    c. Merhaba, **SSO oturum kapatma** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-rally-software-test-user"></a>Rally yazılımı test kullanıcısı oluşturma

Sağlanan toohello Rally yazılımı uygulama Azure Active Directory kullanıcı adlarını kullanarak Azure AD kullanıcıların toobe mümkün toosign için olmaları gerekir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour Rally yazılımı Kiracı oturum açın.

2. Çok Git**Kurulum \> kullanıcılar**ve ardından **+ yeni Ekle**.
   
    ![Kullanıcıların](./media/active-directory-saas-rally-software-tutorial/ic781039.png "kullanıcılar")

3. Merhaba yeni kullanıcı metin kutusuna hello adını yazın ve ardından **ayrıntılarla Ekle**.

4. Merhaba, **kullanıcı oluştur** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı oluşturma](./media/active-directory-saas-rally-software-tutorial/ic781040.png "kullanıcı oluştur")

    a. Merhaba, **kullanıcı adı** metin kutusuna, tür hello gibi kullanıcı adını **Brittsimon**.
   
    b. İçinde **e-posta adresi** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .

    c. İçinde **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.

    d. İçinde **Soyadı** metin kutusuna, hello kullanıcının soyadını gibi girin **Simon**.

    e. Tıklatın **Kaydet ve Kapat**.

   >[!NOTE]
   >API'leri, Azure AD kullanıcı hesapları Rally yazılımı tooprovision tarafından sağlanan veya herhangi diğer Rally yazılımı kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooRally yazılım vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooRally yazılım, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Rally yazılımı**.

    ![Merhaba Rally yazılımı bağlantı hello uygulamalar listesinde](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Rally yazılımı hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma Rally yazılımı uygulama tooyour almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

