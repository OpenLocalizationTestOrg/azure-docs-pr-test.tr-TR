---
title: "Öğretici: Azure Active Directory Tümleştirme ile Work.com | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Work.com arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Öğretici: Azure Active Directory Tümleştirme Work.com ile

Bu öğreticide, bilgi nasıl toointegrate Work.com Azure Active Directory'ye (Azure AD).

Work.com Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooWork.com sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooWork.com (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Work.com ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Work.com çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Work.com ekleme
2. Yapılandırma ve Azure AD çoklu oturum açmayı test etme

## <a name="add-workcom-from-hello-gallery"></a>Merhaba Galerisi'nden Work.com ekleme
Azure AD'ye tooconfigure hello tümleştirme Work.com, tooadd Work.com hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Work.com hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Work.com**seçin **Work.com** sonuçları panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Galerisi'nden ekleme](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Work.com sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Work.com içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Work.com hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Work.com içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Work.com ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Work.com test kullanıcısı oluşturma](#create-a-workcom-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Work.com içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Work.com uygulamanızda yapılandırın.

>[!NOTE]
>tooconfigure çoklu oturum açma, toosetup özel bir Work.com etki alanı adı henüz gerekir. Toodefine en az bir etki alanına ihtiyacınız adı, etki alanı adınızı test ve kuruluşun tamamına tooyour dağıtın.

**tooconfigure Azure AD çoklu oturum açma ile Work.com, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Work.com** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. Merhaba üzerinde **Work.com etki alanı ve URL'leri** bölümünde, hello aşağıdakileri yapın:

    ![Work.com etki alanı ve URL'ler bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Work.com istemci destek ekibi](https://help.salesforce.com/articleView?id=000159855&type=3) tooget bu değer. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Kaydet Düğmesi](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Work.com yapılandırma** 'yi tıklatın **yapılandırma Work.com** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Work.com yapılandırma bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. İçinde tooyour Work.com Kiracı yönetici olarak oturum açın.

8. Çok Git**Kurulum**.
   
    ![Kurulum](./media/active-directory-saas-work-com-tutorial/ic794108.png "Kurulumu")

9. Merhaba de hello sol gezinti bölmesindeki **Yönet** 'yi tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello  **Etki alanım** sayfası. 
   
    ![Etki alanım](./media/active-directory-saas-work-com-tutorial/ic767825.png "etki alanım")

10. etki alanınızın doğru olarak ayarlanmış tooverify alanında olduğundan emin olun "**4 adım dağıtılan tooUsers**" ve gözden geçirin, "**My etki alanı ayarları**".
   
    ![Etki alanı dağıtıldı tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "etki alanı dağıtılan tooUser")

11. İçinde tooyour Work.com Kiracı oturum açın.

12. Çok Git**Kurulum**.
    
    ![Kurulum](./media/active-directory-saas-work-com-tutorial/ic794108.png "Kurulumu")

13. Merhaba genişletin **güvenlik denetimleri** menüsüne ve ardından **çoklu oturum açma ayarları**.
    
    ![Çoklu oturum açma ayarları](./media/active-directory-saas-work-com-tutorial/ic794113.png "tek oturum açma ayarları")

14. Merhaba üzerinde **çoklu oturum açma ayarları** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
    
    ![SAML etkin](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML etkin")
    
    a. Seçin **SAML etkin**.
    
    b. **Yeni**’ye tıklayın.

15. Merhaba, **SAML çoklu oturum açma ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
    
    ![Oturum açma SAML tek ayar](./media/active-directory-saas-work-com-tutorial/ic794114.png "oturum açma SAML tek ayar")
    
    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.  
       
    > [!NOTE]
    > İçin bir değer sağlama **adı** hello otomatik olarak doldurulması **API adı** metin kutusu.
    
    b. İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.
    
    c. Azure portalından tooupload indirilen hello sertifikayı tıklatın **Gözat**.
    
    d. Merhaba, **varlık kimliği** metin kutusuna, türü `https://salesforce-work.com`.
    
    e. Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.
    
    f. Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentfier öğesinde hello konu deyimi**.
    
    g. İçinde **kimlik sağlayıcısı oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    h. İçinde **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.
    
    ı. Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP Post**.
    
    j. **Kaydet** düğmesine tıklayın.

16. Merhaba sol gezinti bölmesinde, Work.com Klasik Portalı'nda tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello **My etki alanı**sayfası. 
    
    ![Etki alanım](./media/active-directory-saas-work-com-tutorial/ic794115.png "etki alanım")

17. Merhaba üzerinde **My etki alanı** sayfasında hello **oturum açma sayfası markalama** 'yi tıklatın **Düzenle**.
    
    ![Oturum açma sayfası markalama](./media/active-directory-saas-work-com-tutorial/ic767826.png "oturum açma sayfası markalama")

14. Merhaba üzerinde **oturum açma sayfası markalama** sayfasında hello **kimlik doğrulama hizmeti** bölümü, hello adını, **SAML SSO ayarları** görüntülenir. Seçin ve ardından **kaydetmek**.
    
    ![Oturum açma sayfası markalama](./media/active-directory-saas-work-com-tutorial/ic784366.png "oturum açma sayfası markalama")

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Kullanıcıların ve grupların tüm kullanıcılar ->](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Ekle](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-workcom-test-user"></a>Work.com test kullanıcısı oluşturma
Azure Active Directory Kullanıcıları toobe mümkün toosign için bunların sağlanan tooWork.com olması gerekir. Work.com Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:
1. Üzerinde tooyour Work.com şirket site yönetici olarak oturum açın.

2. Çok Git**Kurulum**.
   
    ![Kurulum](./media/active-directory-saas-work-com-tutorial/IC794108.png "Kurulumu")
3. Çok Git**kullanıcıları yönetme \> kullanıcılar**.
   
    ![Kullanıcıları yönetme](./media/active-directory-saas-work-com-tutorial/IC784369.png "kullanıcıları yönetme")

4. Tıklatın **yeni kullanıcı**.
   
    ![Tüm kullanıcılar](./media/active-directory-saas-work-com-tutorial/IC794117.png "tüm kullanıcılar")

5. Geçerli bir Azure özniteliklerini içindeki adımları izleyerek hello Hello kullanıcı Düzenle bölümüne, gerçekleştirmek istediğiniz tooprovision hello AD hesabının ilgili metin kutularına:
   
    ![Kullanıcı düzenleme](./media/active-directory-saas-work-com-tutorial/ic794118.png "kullanıcı düzenleme")
   
    a. Merhaba, **ad** metin kutusuna, türü hello **ad** hello kullanıcının **Britta**.
    
    b. Merhaba, **Soyadı** metin kutusuna, türü hello **Soyadı** hello kullanıcının **Simon**.
    
    c. Merhaba, **diğer** metin kutusuna, türü hello **adı** hello kullanıcının **BrittaS**.
    
    d. Merhaba, **e-posta** metin kutusuna, türü hello **e-posta adresi** kullanıcının  **Brittasimon@contoso.com** .
    
    e. Merhaba, **kullanıcı adı** metin kutusuna, türü kullanıcının kullanıcı adını ister  **Brittasimon@contoso.com** .
    
    f. Merhaba, **takma ad** metin kutusuna, bir **takma ad** kullanıcının **Simon**.
    
    g. Seçin **rol**, **kullanıcı lisansı**, ve **profil**.
    
    h. **Kaydet** düğmesine tıklayın.  
      
    > [!NOTE]
    > Hello Azure AD hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabı da dahil olmak üzere bir e-posta alırsınız.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooWork.com vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooWork.com hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Work.com**.

    ![Uygulamanın listesinde Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Work.com hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Work.com uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

