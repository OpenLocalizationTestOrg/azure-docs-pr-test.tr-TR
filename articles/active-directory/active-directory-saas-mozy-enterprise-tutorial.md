---
title: "Öğretici: Azure Active Directory Tümleştirme Mozy kuruluş ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mozy kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a>Öğretici: Azure Active Directory Tümleştirme Mozy kuruluş ile

Bu öğreticide, bilgi nasıl toointegrate Mozy kuruluş Azure Active Directory'ye (Azure AD).

Mozy kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooMozy Kurumsal sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooMozy Enterprise (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Mozy Kurumsal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Mozy Kurumsal çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Mozy Kurumsal ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-mozy-enterprise-from-hello-gallery"></a>Merhaba Galerisi'nden Mozy Kurumsal ekleme
Azure AD'ye tooconfigure hello tümleştirme Mozy Enterprise tooadd Mozy Kurumsal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Mozy Kurumsal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Mozy Kurumsal**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. Merhaba Sonuçlar panelinde seçin **Mozy Kurumsal**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmak ve Mozy kuruluş ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen Mozy kuruluştaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Mozy kuruluştaki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Mozy kuruluşta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Mozy kuruluş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Mozy Kurumsal test kullanıcısı oluşturma](#creating-a-mozy-enterprise-test-user)**  -toohave karşılık gelen, Britta Simon Mozy kuruluştaki kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mozy Kurumsal uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Mozy kuruluş ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Mozy Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. Merhaba üzerinde **Mozy kuruluş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.Mozyenterprise.com`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Mozy Kurumsal İstemci destek ekibi](http://support.mozy.com/) tooget bu değer.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Mozy Kurumsal yapılandırma** 'yi tıklatın **Mozy Kurumsal yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. Farklı web tarayıcısı penceresinde Mozy Kurumsal şirket sitenize yönetici olarak oturum açın.

8. Merhaba, **yapılandırma** 'yi tıklatın **kimlik doğrulama İlkesi**.
   
   ![Kimlik doğrulama İlkesi](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "kimlik doğrulama İlkesi")

9. Merhaba üzerinde **kimlik doğrulama İlkesi** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kimlik doğrulama İlkesi](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "kimlik doğrulama İlkesi")
   
   a. Seçin **dizin hizmeti** olarak **sağlayıcı**.
   
   b. Seçin **LDAP göndermeyi kullanmak**.
   
   c. Merhaba tıklatın **SAML kimlik doğrulaması** sekmesi.
   
   d. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **kimlik doğrulaması URL'sini** metin kutusu.
   
   e. Yapıştır **SAML varlık kimliği**, hello hello Azure portal ' Kopyalanan **SAML Endpoint** metin kutusu.
   
   f. İndirilen base-64 kodlanmış sertifika kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve yapıştırın içine tüm sertifika hello **SAML sertifika** metin kutusu.
   
   g. Seçin **etkinleştirmek SSO Admins toolog, ağ kimlik bilgilerini oturum için**.
   
   h. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-mozy-enterprise-test-user"></a>Mozy Kurumsal test kullanıcısı oluşturma

Mozy Kurumsal içine sipariş tooenable Azure AD kullanıcıların toolog bunlar Mozy kuruma sağlanmalıdır. Mozy Kurumsal Hello durumda sağlama bir el ile bir görevdir.

>[!NOTE]
>API AAD kullanıcı hesaplarının Mozy Kurumsal tooprovision tarafından sağlanan veya herhangi diğer Mozy Kurumsal kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour oturum **Mozy Kurumsal** Kiracı.

2. Tıklatın **kullanıcılar**ve ardından **yeni kullanıcı Ekle**.
   
   ![Kullanıcıların](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "kullanıcılar")
   
   >[!NOTE]
   >Merhaba **yeni kullanıcı Ekle** seçeneği ise yalnızca görüntülenen **Mozy** altında hello sağlayıcısı olarak seçilen **kimlik doğrulama İlkesi**. SAML kimlik doğrulaması yapılandırılmışsa, ardından hello kullanıcılar otomatik olarak çoklu oturum açma aracılığıyla kendi ilk oturum üzerinde üzerinde eklenir.
    
3. Merhaba yeni kullanıcı iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcıları ekleme](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "kullanıcı ekleme")
   
   a. Merhaba gelen **bir grubu seçin** listesinde, bir grup seçin.
   
   b. Merhaba gelen **kullanıcı türüne** listesinde, bir tür seçin.
   
   c. Merhaba, **kullanıcıadı** metin kutusuna, tür hello hello Azure AD kullanıcı adını.
   
   d. Merhaba, **e-posta** metin kutusuna, hello Azure AD kullanıcısının hello e-posta adresini yazın.
   
   e. Seçin **kullanıcı yönerge e-posta Gönder**.
   
   f. Tıklatın **kullanıcıları eklemek**.

     >[!NOTE]
     > Merhaba kullanıcı oluşturduktan sonra onu etkinleştirilmeden önce bir bağlantı tooconfirm hello hesabı içeren toohello Azure AD kullanıcı bir e-posta gönderilir.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooMozy Kurumsal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooMozy Kurumsal hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Mozy Kurumsal**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Mozy Kurumsal döşeme hello erişim paneli hello tıkladığınızda, Mozy Kurumsal uygulama oturum açma sayfasında almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

