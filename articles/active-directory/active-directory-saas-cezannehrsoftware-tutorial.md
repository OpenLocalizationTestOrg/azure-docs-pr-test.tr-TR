---
title: "Öğretici: Azure Active Directory Tümleştirme Cezanne ik yazılımıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Cezanne ik yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Öğretici: Azure Active Directory Cezanne ik yazılım ile tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Cezanne ik yazılım Azure Active Directory'ye (Azure AD).

Cezanne HR yazılım Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar. Şunları yapabilirsiniz:

- Erişim tooCezanne sahip Azure AD'de ik yazılım denetler.
- Kullanıcıların tooautomatically oturum açma tooCezanne ik yazılımıyla çoklu oturum açma (SSO) ile Azure AD hesaplarına etkinleştirin.
- Hesaplarınızı tek bir merkezi konumda yönetme: Azure portal hello.

toolearn yazılım olarak Azure AD ile hizmet (SaaS) uygulama tümleştirmesi hakkında daha fazla bilgi görmek [uygulama erişimi ve SSO ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Cezanne ik yazılım ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Cezanne HR yazılım abonelik SSO'su etkin

> [!NOTE]
> tootest hello adımları Bu öğreticide, bir üretim ortamında kullanmamanızı öneririz.

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD SSO bir test ortamında test. 

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

* Merhaba Galerisi'nden Cezanne ik yazılım ekleme
* Yapılandırma ve Azure AD SSO test etme

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Merhaba Galerisi'nden Cezanne ik yazılım Ekle
Azure AD'ye Cezanne ik yazılımın tooconfigure hello tümleştirme hello galeri tooyour listesinden yönetilen SaaS uygulamaları Cezanne ik yazılım ekleyin.

tooadd Cezanne ik yazılım hello galerisinden hello aşağıdaki:

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi. 

    ![Merhaba "Azure Active Directory" düğmesi][1]

2. Seçin **kurumsal uygulamalar** > **tüm uygulamaları**.

    ![Merhaba "Tüm uygulamaları" bağlantı][2]
    
3. tooadd hello hello üstündeki yeni bir uygulama **tüm uygulamaları** iletişim kutusunda **yeni uygulama**.

    !["Yeni uygulamayı" Merhaba düğmesi][3]

4. Merhaba arama kutusuna yazın **Cezanne ik yazılım**.

    ![Merhaba arama kutusu](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Merhaba sonuçlar listesinde seçin **Cezanne ik yazılım** seçip hello **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD SSO Cezanne ik yazılım "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ile test etme

SSO toowork için Azure AD tooknow hello Cezanne ik yazılım karşılık gelen toohello Azure AD kullanıcısının gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı arasında bir bağlantı ilişkisi hello Cezanne ik yazılım oluşturmanız gerekir.

tooestablish hello bağlantı ilişkisi, Ata hello Cezanne ik yazılım **kullanıcı adı** değeri hello Azure AD olarak **kullanıcıadı** değeri.

tooconfigure ve test Cezanne ik yazılım, yapı taşları aşağıdaki tam hello kullanarak Azure AD SSO.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO yapılandırın

Bu bölümde, hello Azure portalında Azure AD SSO'yu etkinleştirmek ve hello aşağıdakileri yaparak Cezanne ik yazılım uygulamanızda SSO yapılandırın:

1. Merhaba hello üzerinde Azure portal'ın **Cezanne ik yazılım** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.

    ![komutu "çoklu oturum açmayı" Merhaba][4]

2. Merhaba içinde SSO tooenable **çoklu oturum açma** iletişim kutusu, select hello **modu** olarak **SAML tabanlı oturum açma**.
 
    ![Merhaba "Modu" kutusu](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. Altında **Cezanne ik yazılım etki alanı ve URL'leri**, aşağıdaki hello:

    ![Merhaba "Cezanne ik yazılım etki alanı ve URL'leri" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. Merhaba, **oturum açma URL'si** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. Merhaba, **yanıt URL'si** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Merhaba önceki değerleri gerçek değildir. Bunları hello gerçek yanıt URL'si ve hello oturum açma URL'si ile güncelleştirin. tooobtain hello değerleri, kişi hello [Cezanne ik yazılım istemci destek ekibi](mailto:info@cezannehr.com).

4. Altında **SAML imzalama sertifikası**seçin **sertifika (Base64)**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba "SAML imzalama sertifikası" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. **Kaydet**’i seçin.

    ![Merhaba "Kaydet" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. Altında **Cezanne ik yazılım yapılandırma**seçin **Cezanne ik yazılımı Yapılandır** tooopen hello **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmeti** hello URL'den **hızlı başvuru** bölümü.

    ![Merhaba "Cezanne ik yazılım yapılandırma" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Cezanne ik yazılım Kiracı yönetici olarak oturum.

8. Merhaba sol bölmesinde seçin **sistem kurulumu**. Seçin **güvenlik ayarları** > **tek oturum açma yapılandırması**.

    ![Merhaba "Yapılandırma tek oturum açma" bağlantısı](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. Merhaba, **çoklu oturum açma (SSO) Hizmetleri aşağıdaki hello kullanarak kullanıcıların toolog izin** bölmesinde, select hello **SAML 2.0** onay kutusunu ve select hello **Gelişmiş Yapılandırma** seçeneği.

    ![Çoklu oturum açma hizmetleri seçenekleri](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Seçin **yeni Ekle**.

    ![Merhaba "Yeni Ekle" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. Altında **SAML 2.0 kimlik sağlayıcısı**, aşağıdaki hello:

    ![Merhaba "SAML 2.0 kimlik sağlayıcısı" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. Merhaba, **görünen adı** kutusuna, kimlik sağlayıcısının hello adı girin.

    b. Merhaba, **varlık tanımlayıcısı** kutusunda, hello Yapıştır **SAML varlık kimliği** hello Azure portal ' kopyaladığınız. 

    c. Merhaba, **SAML bağlama** liste kutusunda **POST**.

    d. Merhaba, **güvenlik belirteci Hizmeti uç noktası** kutusunda, hello Yapıştır **SAML çoklu oturum açma hizmeti** hello Azure portal ' kopyaladığınız URL. 
    
    e. Merhaba, **kullanıcı kimliği öznitelik adı** kutusuna `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. tooupload hello Azure AD'den select hello sertifika indirilen **karşıya** düğmesi.
    
    g. **Tamam**’ı seçin. 

12. **Kaydet**’i seçin.

    ![Merhaba "Kaydet" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Merhaba uygulama ayarlama gibi hello yönergeleri önceki hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com). Hello hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümü, select hello **çoklu oturum açma** sekmesi. Ardından erişim hello hello belgelerinden katıştırılmış **yapılandırma** bölümü. 

toolearn hello embedded belgeler özelliği hakkında daha fazla bilgi görmek [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde, test kullanıcı Britta Simon hello Azure portal oluşturun.

![Merhaba test kullanıcısı Britta Simon][100]

Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki:

1. Merhaba, **Azure portal**, buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi.

    ![Merhaba "Azure Active Directory" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. Kullanıcıların, select toodisplay hello listesini **kullanıcılar ve gruplar** > **tüm kullanıcılar**.
    
    ![Merhaba "Tüm kullanıcılar" bağlantı](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Merhaba **tüm kullanıcılar** iletişim kutusu açılır.

3. tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.
 
    ![Merhaba "Ekle" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki hello:
 
    ![Merhaba "Kullanıcı" iletişim kutusu](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna kullanıcı Britta Simon'ın yazın **e-posta adresi**.

    c. Select hello **Göster parola** onay kutusunu ve ardından hello oluşturulan Not hello değeri **parola** kutusu.

    d. **Oluştur**’u seçin.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Cezanne HR yazılım test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toosign tooCezanne ik yazılımda bunlar Cezanne ik yazılımına sağlanması gerekir. Cezanne HR yazılım Hello durumda sağlama bir el ile bir görevdir.

Bir kullanıcı hesabı hello aşağıdakileri yaparak sağlayın:

1.  İçinde tooyour Cezanne ik yazılım şirket site yönetici olarak oturum açın.

2.  Merhaba sol bölmesinde seçin **sistem kurulumu** > **kullanıcıları yönetme** > **yeni kullanıcı Ekle**.

    ![Merhaba "Yeni Kullanıcı Ekle" bağlantı](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "yeni kullanıcı")

3.  Altında **kişi ayrıntıları**, aşağıdaki hello:

    ![Merhaba "Kişi Ayrıntıları" bölümü](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "yeni kullanıcı")
    
    a. Ayarlama **iç kullanıcı** olarak **OFF**.
    
    b. Merhaba, **ad** kutusu, türü hello kullanıcının ilk adını, örneğin, **Britta**.  
 
    c. Merhaba, **Soyadı** kutusu, türü hello kullanıcının soyadını, örneğin, **Simon**.
    
    d. Merhaba, **e-posta** hello kullanıcının e-posta adresi, örneğin, yazın Brittasimon@contoso.com.

4.  Altında **hesap bilgilerini**, aşağıdaki hello:

    ![Merhaba "Hesap bilgisi" bölümünde](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "yeni kullanıcı")
    
    a. Merhaba, **kullanıcıadı** hello kullanıcının e-posta adresi, örneğin, yazın Brittasimon@contoso.com.
    
    b. Merhaba, **parola** hello kullanıcının parolasını yazın.
    
    c. Merhaba, **güvenlik rolü** kutusunda **ik Professional**.
    
    d. **Tamam**’ı seçin.

5. Merhaba üzerinde **çoklu oturum açma** sekmede hello **SAML 2.0 tanımlayıcıları** bölümünde, select **yeni Ekle**.

    ![Merhaba "Yeni Ekle" düğmesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "kullanıcı")

6. Merhaba, **kimlik sağlayıcısı** liste kutusunda, kimlik sağlayıcısı seçin. Merhaba, **kullanıcı tanımlayıcısı** kutusunda, test kullanıcı Britta Simon'ın hesabının hello e-posta adresi girin.

    ![Merhaba "Kimlik sağlayıcısı" ve "Kullanıcı tanımlayıcısı" kutuları](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "kullanıcı")
    
7. **Kaydet**’i seçin.

    ![Merhaba "Kaydet" düğmesini](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "kullanıcı")

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, test kullanıcısı Britta Simon toouse Azure SSO erişimi tooCezanne ik yazılım vererek etkinleştirin.

![Test kullanıcı erişimi][200] 

1. Hello Azure portal, hello uygulamaları görünümünü açın ve toohello dizini görünümü gidin. Seçin **kurumsal uygulamalar** > **tüm uygulamaları**.

    ![Merhaba "Tüm uygulamaları" bağlantı][201] 

2. Merhaba uygulamalar listesinde **Cezanne ik yazılım**.

    ![Merhaba "Uygulamaları" listesi](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. Merhaba soldaki Hello menüde seçin **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. **Add (Ekle)** seçeneğini belirleyin. Merhaba sonra **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantı][203]

5. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinde **Britta Simon**.

6. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **seçin**.

7. Merhaba, **eklemek atama** iletişim kutusunda **atamak**.
    
### <a name="test-sso"></a>Test SSO

Bu bölümde, hello erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.

Merhaba erişim paneli hello Cezanne ik yazılım döşeme seçtiğinizde, otomatik olarak tooyour üzerinde Cezanne ik yazılım uygulaması imzalayın.

## <a name="next-steps"></a>Sonraki adımlar

* [İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve SSO ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

