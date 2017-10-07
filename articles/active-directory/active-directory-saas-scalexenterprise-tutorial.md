---
title: "Öğretici: Azure Active Directory Tümleştirme ScaleX kuruluş ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ScaleX kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Öğretici: Azure Active Directory Tümleştirme ScaleX kuruluş ile

Bu öğreticide, bilgi nasıl toointegrate ScaleX kuruluş Azure Active Directory'ye (Azure AD).

ScaleX kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooScaleX Kurumsal sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooScaleX Enterprise (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz. Uygulama erişimi ve çoklu oturum açma ile nedir [Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure ScaleX Kurumsal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir ScaleX Kurumsal çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden ScaleX Kurumsal ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Merhaba Galerisi'nden ScaleX Kurumsal ekleme
tooAzure AD içinde tooconfigure hello tümleştirme ScaleX Enterprise tooadd ScaleX Kurumsal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd ScaleX Kurumsal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **ScaleX Kurumsal**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. Merhaba Sonuçlar panelinde seçin **ScaleX Kurumsal**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve ScaleX kuruluş ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı

Tek toowork'ın oturum açma hangi hello karşılık gelen ScaleX kuruluştaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve ScaleX kuruluştaki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ScaleX kuruluştaki.

tooconfigure ve ScaleX kuruluş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[ScaleX Kurumsal test kullanıcısı oluşturma](#creating-a-scalex-enterprise-test-user)**  -toohave karşılık gelen, Britta Simon ScaleX kuruluştaki kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ScaleX Kurumsal uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ScaleX kuruluş ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **ScaleX Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. Merhaba üzerinde **ScaleX kuruluş etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://platform.rescale.com/saml2/<company id>/`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Bunlar hello gerçek değerleri değildir. Bu değerleri gerçek tanımlayıcısı, yanıt URL'si veya oturum açma URL'si hello ile güncelleştirin. Kişi [ScaleX Kurumsal İstemci destek ekibi](http://info.rescale.com/contact_sales) tooget bu değerleri. 

5. ScaleX uygulamanızı hello SAML onaylar, toomodify özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor. ' I tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** onay kutusunu tooopen hello özel öznitelikleri ayarlar.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Merhaba özniteliği sağ tıklatın **adı** ve Sil'i tıklatın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Tıklatın **emailaddress** özniteliği tooopen hello öznitelik Düzenle penceresi. Kendi değerini değiştirmek **user.mail** çok**user.userprincipalname** ve Tamam'ı tıklatın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. Merhaba üzerinde **ScaleX Kurumsal yapılandırma** 'yi tıklatın **ScaleX Kurumsal yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure çoklu oturum açma üzerinde **ScaleX Kurumsal** tarafı, yönetici olarak oturum açma toohello ScaleX Kurumsal şirket Web sitesi.

9. Merhaba hello üst menüde sağ tıklayın ve **Contoso Yönetim**.

    > [!NOTE] 
    > Contoso yalnızca bir örnektir. Bu, gerçek şirket adınızı olmalıdır. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Seçin **tümleştirmeler** hello üst menüsünden ve select **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Merhaba form aşağıdaki gibi tamamlayın:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Seçin **"SSO ile doğrulanabilir herhangi bir kullanıcı oluşturun."**

    b. **Hizmet sağlayıcısı saml**: yapıştırma hello değeri ***urn: OASIS: adları: tc: SAML:2.0:nameid-biçimi: kalıcı***

    c. **ACS yanıt kimlik sağlayıcısı e-posta alanının adı**: hello değeri yapıştırın`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **Kimlik sağlayıcısı EntityDescriptor varlık Tanıtıcısı:** Yapıştır hello **SAML varlık kimliği** değer hello Azure portal ' kopyalanır.

    e. **Kimlik sağlayıcısı SingleSignOnService URL'si:** Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello Azure Portalı'ndan.

    f. **Kimlik sağlayıcısı ortak X509 sertifikası:** not defteri ve Yapıştır hello içeriği bu kutuya hello Azure'ndan indirilen açık hello X509 sertifika. Hiçbir satır hello hello sertifika içeriğini Orta sonlarını emin olun.
    
    g. Aşağıdaki onay kutularını hello denetleyin: **etkin, NameID şifrelemek ve oturum AuthnRequests.**

    h. Tıklatın **güncelleştirme SSO ayarlarını** toosave hello ayarları.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>ScaleX Kurumsal test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooScaleX kuruluş'da, bunlar tooScaleX Kurumsal sağlanması gerekir. Merhaba durumda ScaleX Enterprise sağlama otomatik bir görevdir ve el ile yapılan hiçbir adım gerekli değildir. SSO kimlik bilgileriyle kimlik doğrulamasını başarıyla herhangi bir kullanıcı ScaleX yan hello üzerinde otomatik olarak sağlanacak.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kullanıcı erişim tooScaleX Kurumsal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooScaleX Kurumsal hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ScaleX Kurumsal**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

ScaleX Kurumsal döşeme hello erişim paneli hello tıklatın tooyour ScaleX Kurumsal uygulama otomatik olarak oturum açmış olursunuz. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

