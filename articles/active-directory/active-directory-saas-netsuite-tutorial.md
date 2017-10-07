---
title: "Öğretici: Azure Active Directory Tümleştirme ile Netsuite | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Netsuite arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Öğretici: Azure Active Directory Tümleştirme Netsuite ile

Bu öğreticide, bilgi nasıl toointegrate Netsuite Azure Active Directory'ye (Azure AD).

Netsuite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooNetsuite sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooNetsuite (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Netsuite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Netsuite çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Netsuite ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-netsuite-from-hello-gallery"></a>Merhaba Galerisi'nden Netsuite ekleme
Azure AD'ye tooconfigure hello tümleştirme Netsuite, tooadd Netsuite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Netsuite hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Netsuite**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. Merhaba Sonuçlar panelinde seçin **Netsuite**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Netsuite ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Netsuite içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Netsuite hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Netsuite içinde.

tooconfigure ve Netsuite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Netsuite test kullanıcısı oluşturma](#creating-a-netsuite-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Netsuite içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Netsuite uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Netsuite, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Netsuite** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. Merhaba üzerinde **Netsuite etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Bu değer gerçek değeri değil. Güncelleştirme hello değerle hello gerçek yanıt URL'si. Kişi [Netsuite destek ekibi](http://www.netsuite.com/portal/services/support.shtml) tooget bu değer.
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Netsuite yapılandırma** 'yi tıklatın **yapılandırma Netsuite** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Tarayıcınızda yeni bir sekme açın ve Netsuite şirket sitenizin yönetici olarak oturum açın.

8. Merhaba sayfanın üst kısmındaki hello Hello araç çubuğunda **Kurulum**, ardından **Kurulum Yöneticisi**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. Merhaba gelen **kurulum görevlerini** listesinde **tümleştirme**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. Merhaba, **yönetmek kimlik doğrulama** 'yi tıklatın **SAML çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. Merhaba üzerinde **SAML Kurulumu** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    a. Kopya hello **SAML çoklu oturum açma hizmet URL'si** değeri **hızlı başvuru** bölümünü **yapılandırma oturum açma** ve hello yapıştırma **kimlik sağlayıcısı Oturum açma sayfasına** Netsuite alanındaki.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. Netsuite içinde seçin **birincil kimlik doğrulama yöntemini**.

    c. Etiketli hello alan için **SAMLV2 kimlik sağlayıcısı meta verileri**seçin **IDP meta veri dosyasını karşıya yükle**. Ardından **Gözat** Azure portalından indirdiğiniz tooupload hello meta veri dosyası.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Tıklatın **gönderme**.

12. Azure AD'de tıklayın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** onay kutusunu ve özniteliğini ekleyin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Hello için **öznitelik adı** alan, yazın `account`. Hello için **öznitelik değeri** alanında, Netsuite hesabı kimliğinizi yazın Bu, sabit ve hesap değişiklikle değerdir. Yönergeler toofind hesabı Kimliğiniz aşağıda bulunmaktadır:

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. Netsuite içinde tıklatın **Kurulum** hello üst gezinti menüsünde.

    b. Hello altında ardından **kurulum görevlerini** hello sol gezinti menüsünde, select hello bölümünü **tümleştirme** bölüm ve'ı tıklatın **Web Hizmetleri tercihleri**.

    c. Netsuite hesabı Kimliğinizi kopyalayın ve hello yapıştırın **öznitelik değeri** Azure AD alanındaki.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Kullanıcıların çoklu oturum açma Netsuite gerçekleştirmeden önce ilk hello Netsuite için uygun izinler atanmaları gerekir. Bu izinleri tooassign aşağıdaki Hello yönergeleri izleyin.

    a. Merhaba üst gezinti menüsünde **Kurulum**, ardından **Kurulum Yöneticisi**.
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. Merhaba sol gezinti menüsünde seçin **kullanıcıları/rolleri**, ardından **Rolleri Yönet**.
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Tıklatın **yeni rol**.

    d. Yazın bir **adı** yeni rol ve select hello **tek oturum açma yalnızca** onay kutusu.
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. **Kaydet** düğmesine tıklayın.

    f. Hello içinde hello üst menüsünde **izinleri**. Ardından **Kurulum**.
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Seçin **ayarlamak yukarı SAM çoklu oturum açma**ve ardından **Ekle**.

    h. **Kaydet** düğmesine tıklayın.

    ı. Merhaba üst gezinti menüsünde **Kurulum**, ardından **Kurulum Yöneticisi**.
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. Merhaba sol gezinti menüsünde seçin **kullanıcıları/rolleri**, ardından **kullanıcıları yönetme**.
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Bir test kullanıcı seçin. Ardından **Düzenle**.
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. Hello rolleri iletişim kutusunda, oluşturduğunuz ve'ı tıklatın hello rolü seçin **Ekle**.
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. **Kaydet** düğmesine tıklayın.
    
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-a-netsuite-test-user"></a>Netsuite test kullanıcısı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı Netsuite içinde oluşturulur. Netsuite yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.
Bu bölümde, eylem öğe yok. Bir kullanıcı Netsuite zaten yoksa, tooaccess Netsuite çalıştığında yeni bir tane oluşturulur.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooNetsuite vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooNetsuite hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Netsuite**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

tootest, çoklu oturum açma ayarları, açık hello adresinden erişim Paneli'nde [https://myapps.microsoft.com](https://myapps.microsoft.com/), oturum hello test dikkate ve tıklatın **Netsuite**.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

