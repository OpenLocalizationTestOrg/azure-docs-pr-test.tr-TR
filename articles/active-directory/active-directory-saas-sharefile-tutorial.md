---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix ShareFile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Citrix ShareFile arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Öğretici: Citrix ShareFile Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Citrix ShareFile Azure Active Directory'ye (Azure AD).

Citrix ShareFile Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooCitrix ShareFile sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooCitrix ShareFile (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Citrix ShareFile ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Citrix ShareFile çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Citrix ShareFile hello Galerisi'nden ekleme
2. Yapılandırma ve Azure AD çoklu oturum açmayı test etme

## <a name="add-citrix-sharefile-from-hello-gallery"></a>Citrix ShareFile hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Citrix ShareFile, tooadd Citrix ShareFile hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Citrix ShareFile hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Citrix ShareFile**seçin **Citrix ShareFile** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba, Citrix ShareFile listesi sonuçları](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırmanız ve Citrix ShareFile ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen Citrix ShareFile içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Citrix ShareFile hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.

Citrix ShareFile içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Citrix ShareFile ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Citrix ShareFile test kullanıcısı oluşturma](#create-a-citrix-sharefile-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Citrix ShareFile içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Citrix ShareFile uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Citrix ShareFile ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Citrix ShareFile** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. Merhaba üzerinde **Citrix ShareFile etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Citrix ShareFile etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Citrix ShareFile istemci destek ekibi](https://www.citrix.co.in/products/sharefile/support.html) tooget bu değer. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Citrix ShareFile yapılandırma** 'yi tıklatın **yapılandırma Citrix ShareFile** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Citrix ShareFile yapılandırma](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. Farklı web tarayıcısı penceresinde oturum açın, **Citrix ShareFile** yönetici olarak şirket site.

8. Merhaba üstte Hello araç çubuğunda **yönetici**.

9. Merhaba sol gezinti bölmesinde seçin **yapılandırma çoklu oturum açma**.
   
    ![Hesap Yönetimi](./media/active-directory-saas-sharefile-tutorial/ic773627.png "hesap yönetimi")

10. Merhaba üzerinde **çoklu oturum açma / SAML 2.0 yapılandırma** iletişim sayfasında altında **temel ayarları**, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma](./media/active-directory-saas-sharefile-tutorial/ic773628.png "çoklu oturum açma")
   
    a. Tıklatın **etkinleştirmek SAML**.
    
    b. İçinde **bilgisayarınızı IDP veren / varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.

    c. Tıklatın **değişiklik** sonraki toohello **X.509 sertifikası** alan ve karşıya yükleme hello sertifika'ndan indirilen hello Azure portalı.
    
    d. İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
    
    e. İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.

11. Tıklatın **kaydetmek** hello Citrix ShareFile yönetim portalı üzerinde.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Citrix ShareFile test kullanıcısı oluşturma

Citrix ShareFile içine sipariş tooenable Azure AD kullanıcıların toolog bunlar Citrix ShareFile sağlanmalıdır. Citrix ShareFile Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Citrix ShareFile** Kiracı.

2. Tıklatın **kullanıcıları yönetme \> kullanıcıların giriş yönetmek \> + çalışan oluşturma**.
   
   ![Çalışan oluşturma](./media/active-directory-saas-sharefile-tutorial/IC781050.png "çalışan oluşturma")

3. Merhaba üzerinde **temel bilgileri** bölümünde, aşağıdaki adımları gerçekleştirin:
   
   ![Temel bilgileri](./media/active-directory-saas-sharefile-tutorial/IC799951.png "temel bilgileri")
   
   a. Merhaba, **e-posta adresi** metin kutusuna, türü hello e-posta adresi Britta Simon  **brittasimon@contoso.com** .
   
   b. Merhaba, **ad** metin kutusuna, türü **ad** kullanıcının **Britta**.
   
   c. Merhaba, **Soyadı** metin kutusuna, türü **Soyadı** kullanıcının **Simon**.

4. Tıklatın **kullanıcı ekleme**.
  
   >[!NOTE]
   >Hello Azure AD hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin. API'leri, Azure AD kullanıcı hesapları Citrix ShareFile tooprovision tarafından sağlanan veya herhangi diğer Citrix ShareFile kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooCitrix ShareFile vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooCitrix ShareFile, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Citrix ShareFile**.

    ![Merhaba hello uygulamalar listesinde Citrix ShareFile bağlantı](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Citrix ShareFile döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Citrix ShareFile uygulama tooyour almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

