---
title: "Öğretici: Azure Active Directory Tümleştirme Mimecast Yönetici Konsolu ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mimecast Yönetici Konsolu arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Öğretici: Azure Active Directory Tümleştirme Mimecast Yönetici Konsolu ile

Bu öğreticide, bilgi toointegrate Mimecast Yönetici Konsolu nasıl Azure Active Directory (Azure AD) ile.

Mimecast Yönetici Konsolu Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooMimecast Yönetici konsolunda olan Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooMimecast Yönetim Konsolu (çoklu oturum açma) etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Mimecast Yönetim Konsolu ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Mimecast Yönetici Konsolu çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Hello Galerisi'nden Mimecast Yönetici Konsolu'nu ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a>Hello Galerisi'nden Mimecast Yönetici Konsolu'nu ekleme
Azure AD'ye tooconfigure hello tümleştirme Mimecast yönetici konsolunun tooadd Mimecast Yönetici Konsolu hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Mimecast Yönetici Konsolu hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Hello arama kutusuna yazın **Mimecast Yönetici Konsolu**seçin **Mimecast Yönetici Konsolu** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Mimecast Yönetim Konsolu](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Mimecast Yönetici Konsolu ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Mimecast Yönetici konsolunda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Mimecast Yönetici konsolunda hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Mimecast Yönetici konsolunda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Mimecast Yönetici Konsolu ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Mimecast Yönetici Konsolu test kullanıcısı oluşturma](#create-a-mimecast-admin-console-test-user) ** -toohave karşılık gelen, Britta Simon Mimecast Yönetici konsolunda, kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mimecast Yönetici Konsolu uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Mimecast yönetim konsoluyla hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Mimecast Yönetici Konsolu** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. Merhaba üzerinde **Mimecast Yönetici Konsolu etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Mimecast Yönetici Konsolu etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > Merhaba oturum açma URL'si belirli bölgedir.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Mimecast Yönetici Konsolu Yapılandırması** 'yi tıklatın **Mimecast Yönetim Konsolu** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Mimecast Yönetici Konsolu yapılandırması](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. Farklı web tarayıcısı penceresinde Mimecast Yönetici konsolunda bir yönetici olarak oturum açın.

8. Çok Git**Hizmetleri \> uygulama**.

    ![Hizmetleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Hizmetleri")

9. Tıklatın **kimlik doğrulaması profilleri**.

    ![Kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "kimlik doğrulaması profilleri")
    
10. Tıklatın **yeni kimlik doğrulama profili**.

    ![Yeni kimlik doğrulama profilleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "yeni kimlik doğrulama profilleri")

11. Merhaba, **kimlik doğrulama profili** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Kimlik doğrulama profili](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "kimlik doğrulama profili")
    
    a. Merhaba, **açıklama** metin kutusuna, yapılandırmanız için bir ad yazın.
    
    b. Seçin **Mimecast Yönetici Konsolu için SAML kimlik doğrulaması zorunlu**.
    
    c. Olarak **sağlayıcı**seçin **Azure Active Directory**.
    
    d. Yapıştır **SAML varlık kimliği**, hello hello Azure portal ' Kopyalanan **veren URL'si** metin kutusu.
    
    e. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **oturum açma URL'si** metin kutusu.

    f. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **oturum kapatma URL'si** metin kutusu.
    
    >[!NOTE]
    >Merhaba Mimecast Yönetici Konsolu hello aynı hello oturum açma URL'si değeri ve hello oturum kapatma URL'si değeri olursunuz.
    
    g. Base-64 sertifikanızı Not Defteri'nde, Azure Portalı'ndan indirilen açık hello ilk satırı Kaldır ("*--*") ve hello son satır ("*--*"), bu içerik kalan kopyalama hello Pano, içine toohello yapıştırın **kimlik sağlayıcısı sertifikası (meta verileri)** metin kutusu.
    
    h. Seçin **çoklu oturum açmaya izin verme**.
    
    ı. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-mimecast-admin-console-test-user"></a>Mimecast Yönetici Konsolu test kullanıcısı oluşturma

Mimecast yönetici konsoluna sipariş tooenable Azure AD kullanıcıların toolog bunlar Mimecast Yönetici konsolunda sağlanmalıdır. Mimecast Yönetici Konsolu Hello durumda sağlama bir el ile bir görevdir.

* Kullanıcıların oluşturabilmeniz için önce tooregister bir etki alanı gerekir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. Tooyour üzerinde oturum **Mimecast Yönetici Konsolu** yönetici olarak.
2. Çok Git**dizinleri \> dahili**.
   
   ![Dizinleri](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "dizinleri")
3. Tıklatın **kayıt yeni bir etki alanı**.
   
   ![Yeni etki alanı kayıt](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "kayıt yeni bir etki alanı")
4. Yeni etki alanınızın oluşturulduktan sonra tıklatın **yeni adresi**.
   
   ![Yeni bir adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "yeni adresi")
5. Merhaba yeni adresi iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kaydet](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Kaydet")
   
   a. Türü hello **e-posta adresi**, **genel adı**, **parola**, ve **parolayı onayla** öznitelikleri geçerli bir Azure ad hesabına istiyor metin kutuları hello içine tooprovision ilgili.

   b. **Kaydet** düğmesine tıklayın.

>[!NOTE]
>Herhangi bir Mimecast Yönetim Konsolu kullanıcı hesabı oluşturma araçlarını veya Mimecast Yönetici Konsolu tooprovision Azure AD kullanıcı hesapları tarafından sağlanan API'leri kullanabilirsiniz. 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooMimecast Yönetici Konsolu vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooMimecast yönetici konsolunu hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Mimecast Yönetici Konsolu**.

    ![Hello Mimecast yönetici konsolunu bağlantısı hello uygulamalar listesinde](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Mimecast Yönetici Konsolu hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Mimecast yönetici konsol uygulaması almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

