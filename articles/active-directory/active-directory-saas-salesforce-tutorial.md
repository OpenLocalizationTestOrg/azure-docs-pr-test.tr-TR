---
title: "Öğretici: Azure Active Directory Tümleştirme Salesforce ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Öğretici: Salesforce Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Salesforce Azure Active Directory'ye (Azure AD).

Salesforce Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSalesforce sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSalesforce (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Salesforce ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Salesforce çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Salesforce hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-salesforce-from-hello-gallery"></a>Salesforce hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Salesforce, tooadd Salesforce hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd hello galerisinden Salesforce hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Salesforce**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. Merhaba Sonuçlar panelinde seçin **Salesforce**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Salesforce ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Salesforce içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Salesforce hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Salesforce içinde.

tooconfigure ve Salesforce ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Salesforce test kullanıcısı oluşturma](#creating-a-salesforce-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Salesforce içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Salesforce uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Salesforce ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Salesforce** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Merhaba üzerinde **Salesforce etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri: 
   * Kurumsal hesap:`https://<subdomain>.my.salesforce.com`
   * Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Bu değerler hello gerçek değildir. Bu değerleri hello gerçek oturum açma URL'si ile güncelleştirin. Kişi [Salesforce istemci destek ekibi](https://help.salesforce.com/support) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Salesforce yapılandırma** 'yi tıklatın **yapılandırma Salesforce** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.** 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Tarayıcınızda yeni bir sekme açın ve oturum tooyour Salesforce yönetici hesabı.

8.  Merhaba altında **yönetici** Gezinti bölmesinde, tıklatın **güvenlik denetimleri** tooexpand hello ilgili bölümü. Ardından **çoklu oturum açma ayarları**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  Merhaba üzerinde **çoklu oturum açma ayarları** hello sayfasında, **Düzenle** düğmesi.
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Salesforce hesabınız için oluşturulamıyor tooenable çoklu oturum açma ayarları varsa, toocontact gerekebilir [Salesforce istemci destek ekibi](https://help.salesforce.com/support). 

10. Seçin **SAML etkin**ve ardından **kaydetmek**.

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. SAML çoklu oturum açma ayarlarınızı tooconfigure tıklatın **yeni**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. Merhaba üzerinde **SAML çoklu oturum açma ayarını Düzenle** sayfasında, aşağıdaki yapılandırmaları hello olun:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Hello için **adı** alanına, bu yapılandırma için bir kolay ad yazın. İçin bir değer sağlama **adı** hello otomatik olarak doldurulması **API adı** metin kutusu.

    b. Yapıştır **SMAL varlık kimliği** hello değerine **veren** Salesforce alanındaki.

    c. Merhaba, **varlık kimliği textbox**, desen aşağıdaki hello kullanarak Salesforce etki alanı adınızı yazın:
      
      * Kurumsal hesap:`https://<subdomain>.my.salesforce.com`
      * Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Tıklatın **Gözat** veya **Dosya Seç** tooopen hello **Dosya Seç tooUpload** iletişim kutusunda, Salesforce sertifikanızı seçin ve ardından **açmak**tooupload hello sertifika.

    e. İçin **SAML kimlik türü**seçin **onaylamayı kullanıcının salesforce.com kullanıcı adını içeren**.

    f. İçin **SAML kimlik konumu**seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**

    g. Yapıştır **çoklu oturum açma hizmet URL'si** hello içine **kimlik sağlayıcısı oturum açma URL'si** Salesforce alanındaki.
    
    h. İçin **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP yeniden yönlendirme**.
    
    ı. Son olarak, tıklatın **kaydetmek** tooapply, SAML çoklu oturum açma ayarları.

13. Merhaba sol gezinti Salesforce bölmesinde **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Toohello aşağı **kimlik doğrulama Yapılandırması** bölümünde ve hello tıklatın **Düzenle** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. Merhaba, **kimlik doğrulama hizmeti** bölümünde, SAML SSO yapılandırmanızın hello kolay ad seçin ve ardından **kaydetmek**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Birden fazla kimlik doğrulama hizmeti seçili ise, hangi kimlik doğrulama hizmeti oldukları gibi istendiğinde tooselect kullanıcılardır tek oturum açma tooyour Salesforce ortamını başlatma sırasında toosign ile. Toohappen istemediğiniz sonra yapmanız gerekenler **diğer tüm kimlik doğrulama hizmetleri işaretlemeden bırakın**.
<CE>    
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesindeki **Azure portal**, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-salesforce-test-user"></a>Salesforce test kullanıcısı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce'ta oluşturulur. Salesforce yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.
Bu bölümde, eylem öğe yok. Bir kullanıcı zaten Salesforce'ta yoksa, tooaccess Salesforce çalıştığında yeni bir tane oluşturulur.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSalesforce vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSalesforce hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Salesforce**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

tootest, çoklu oturum açma ayarları, açık hello adresinden erişim Paneli'nde [https://myapps.microsoft.com](https://myapps.microsoft.com/)hello test hesaba oturum açın ve tıklatın **Salesforce**.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

