---
title: "Öğretici: Azure Active Directory Tümleştirme Adobe işaretiyle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma Azure Active Directory ve Adobe oturum arasında bilgi edinin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Öğretici: Azure Active Directory Tümleştirme Adobe oturum

Bu öğreticide, bilgi Adobe toointegrate oturum nasıl Azure Active Directory (Azure AD) ile.

Adobe oturum Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAdobe oturum sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooAdobe oturum (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Adobe oturum ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Adobe oturum çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Adobe oturum hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-adobe-sign-from-hello-gallery"></a>Adobe oturum hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme, Adobe oturum tooadd Adobe oturum hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Adobe oturum hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Adobe oturum**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. Merhaba Sonuçlar panelinde seçin **Adobe oturum**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Adobe işaretiyle test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Adobe oturum içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Adobe oturum hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.

Adobe oturum açma hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Adobe işaretiyle Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Adobe oturum test kullanıcısı oluşturma](#creating-an-adobe-sign-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Adobe oturum içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Adobe oturum uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Adobe işaretiyle hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Adobe oturum** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. Merhaba üzerinde **Adobe oturum etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.echosign.com/`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Adobe oturum istemci destek ekibi](https://helpx.adobe.com/in/contact/support.html) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Adobe oturum yapılandırma** 'yi tıklatın **yapılandırma Adobe oturum** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. Farklı web tarayıcısı penceresinde tooyour Adobe oturum şirket sitede yönetici olarak oturum açın.

8. Hello üstte Hello menüde'ı tıklatın **hesap**ve ardından, hello sol tarafında hello Gezinti Bölmesi'nde **SAML ayarları** altında **hesap ayarlarını**.
   
   ![Hesap](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "hesabı")

9. Hello SAML Ayarlar bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![SAML ayarları](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML ayarları")
   
   a. Olarak **SAML modu**seçin **SAML zorunlu**.
   
   b. Seçin **EchoSign kimlik bilgilerini kullanarak EchoSign hesap yöneticileri izin toolog**.
   
   c. Olarak **kullanıcı oluşturma**seçin **otomatik olarak SAML kimliği doğrulanmış kullanıcılar eklemek**.

10. Taşıma, aşağıdaki hello gerçekleştirme adımları:

       ![SAML ayarları](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML ayarları")

    a. Yapıştır **SAML varlık kimliği**, hello Azure portalından kopyalanan **IDP varlık kimliği** metin kutusu.
    
    b. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello Azure portalından kopyalanan **IDP oturum açma URL'si** metin kutusu.
   
    c. Yapıştır **Sign-Out URL**, hello Azure portalından kopyalanan **IDP oturum kapatma URL'si** metin kutusu.

    d. İndirilen açmak **Certificate(Base64)** dosyasını Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello Yapıştır **IDP sertifika** metin kutusu

    e. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-adobe-sign-test-user"></a>Adobe oturum test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooAdobe oturum'da, bunlar Adobe oturum açın sağlanması gerekir. Adobe oturum Hello durumda sağlama bir el ile bir görevdir.

>[!NOTE]
>API AAD kullanıcı hesapları Adobe oturum tooprovision tarafından sağlanan veya herhangi diğer Adobe oturum kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Adobe oturum** yönetici olarak şirket site.

2. Hello üstte Hello menüde'ı tıklatın **hesap**ve ardından, hello sol tarafında hello Gezinti Bölmesi'nde **kullanıcıları ve grupları**ve ardından **yeni bir kullanıcı oluşturmak**.
   
   ![Hesap](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "hesabı")
   
3. Merhaba, **yeni kullanıcı oluştur** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "kullanıcı oluştur")
   
   a. Türü hello **e-posta adresi**, **ad**, ve **Soyadı** , metin kutuları hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.
   
   b. Tıklatın **kullanıcı oluşturma**.

>[!NOTE]
>Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alır. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooAdobe oturum vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooAdobe oturum, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Adobe oturum**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Adobe oturum hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak oturum açma Adobe oturum uygulama tooyour almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

