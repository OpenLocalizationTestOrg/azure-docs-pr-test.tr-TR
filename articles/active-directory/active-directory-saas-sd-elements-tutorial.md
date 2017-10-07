---
title: "Öğretici: Azure Active Directory Tümleştirme SD öğelerle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SD öğeleri arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a>Öğretici: Azure Active Directory Tümleştirme SD öğeleri

Bu öğreticide, bilgi nasıl toointegrate SD öğeleri Azure Active Directory'ye (Azure AD).

SD öğeleri Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSD öğeleri sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSD öğeleri (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure SD öğeleri ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir SD öğeleri çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden SD öğeleri ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sd-elements-from-hello-gallery"></a>Merhaba Galerisi'nden SD öğeleri ekleme
Azure AD'ye tooconfigure hello tümleştirme SD öğelerinin tooadd SD öğeleri hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SD öğeleri hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SD öğeleri**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. Merhaba Sonuçlar panelinde seçin **SD öğeleri**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SD "Britta Simon" adlı bir test kullanıcıya bağlı öğeleri ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen SD öğelerinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı SD öğeleri arasında bir bağlantı ilişkisi kurulan toobe gerekir.

SD öğelerinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve SD öğeleri ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SD öğeleri test kullanıcısı oluşturma](#creating-a-sd-elements-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SD öğelerinde, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SD öğeleri uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma SD öğelerle hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **SD öğeleri** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. Merhaba üzerinde **SD öğeleri etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.sdelements.com/sso/saml2/metadata`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.sdelements.com/sso/saml2/acs/`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [SD öğeleri destek ekibi](mailto:support@sdelements.com) tooget bu değerleri.

4. SD öğeleri uygulama hello SAML onaylar belirli bir biçimde bekler. Bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Kullanıcı özniteliği"** hello uygulama sekmesinde. Ekran aşağıdaki hello bunun bir örneği gösterir.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin: 

    | Öznitelik adı | Öznitelik değeri |
    | --- | --- |
    | E-posta |User.Mail |
    | FirstName |User.givenName |
    | Soyadı |User.surname |

    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.

    d. **Tamam**’a tıklayın.
 
6. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. Merhaba üzerinde **SD öğeleri yapılandırma** 'yi tıklatın **yapılandırma SD öğeleri** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. tooget tekli etkin oturum kişi, [SD öğeleri destek ekibi](mailto:support@sdelements.com) ve hello indirilen sertifika dosyasıyla verin. 

10. Farklı bir tarayıcı penceresinde bir yönetici olarak oturum açma tooyour SD öğeleri Kiracı.

11. Hello içinde hello üst menüsünde **sistem**ve ardından **çoklu oturum açma**. 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. Merhaba üzerinde **çoklu oturum açma ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    a. Olarak **SSO türü**seçin **SAML**.
   
    b. Merhaba, **kimlik sağlayıcısı varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan. 
   
    c. Merhaba, **kimlik sağlayıcısı çoklu oturum açma hizmeti** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan. 
   
    d. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sd-elements-test-user"></a>SD öğeleri test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate SD öğelerinde Britta Simon adlı bir kullanıcı var. SD öğeleri Hello durumda SD öğeleri kullanıcıları oluşturarak bir el ile bir görevdir.

**toocreate Britta Simon SD öğelerinde hello aşağıdaki adımları gerçekleştirin:**

1. Bir web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour SD öğeleri şirket site.

2. Hello içinde hello üst menüsünde **kullanıcı yönetimi**ve ardından **kullanıcılar**.
   
    ![SD öğeleri test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. Tıklatın **yeni kullanıcı Ekle**.
   
    ![SD öğeleri test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. Merhaba üzerinde **yeni kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![SD öğeleri test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    a. Merhaba, **e-posta** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .
   
    b. Merhaba, **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.
   
    c. Merhaba, **Soyadı** metin kutusuna, hello son gibi kullanıcı adını girin **Simon**.
   
    d. Olarak **rol**seçin **kullanıcı**. 
   
    e. Tıklatın **kullanıcı oluşturma**.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, tooSD öğeleri erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSD öğeleri hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SD öğeleri**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.
  
SD öğeleri hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak imzalanmış üzerinde SD öğeleri uygulama tooyour almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

