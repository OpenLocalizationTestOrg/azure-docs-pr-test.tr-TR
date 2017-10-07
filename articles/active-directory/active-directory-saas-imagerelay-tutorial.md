---
title: "Öğretici: Azure Active Directory Tümleştirme ile görüntü geçiş | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve görüntü geçiş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a>Öğretici: Azure Active Directory Tümleştirme ile görüntü geçişi

Bu öğreticide, bilgi nasıl toointegrate görüntü geçiş Azure Active Directory'ye (Azure AD).

Görüntü geçiş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooImage geçiş sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooImage geçişi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure görüntü geçiş ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir görüntü geçiş çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Görüntü geçiş hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-image-relay-from-hello-gallery"></a>Görüntü geçiş hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme görüntü geçişinin hello galeri tooyour yönetilen SaaS uygulamaları listesinden görüntü geçiş tooadd gerekir.

**tooadd görüntü geçiş hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **görüntü geçiş**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. Merhaba Sonuçlar panelinde seçin **görüntü geçiş**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma görüntü "Britta Simon" adlı bir test kullanıcı tabanlı geçiş ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen görüntü geçiş içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve görüntü geçiş hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Görüntü geçiş hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve görüntü geçiş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir görüntü geçiş test kullanıcısı oluşturma](#creating-an-image-relay-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir görüntü geçiş içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma görüntü geçiş uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma görüntü geçiş ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **görüntü geçiş** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. Merhaba üzerinde **görüntü geçiş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.imagerelay.com/`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.imagerelay.com/sso/metadata`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [görüntü geçiş istemci destek ekibi](http://support.imagerelay.com/) tooget bu değerleri. 
 


4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **görüntü geçiş yapılandırma** 'yi tıklatın **yapılandırma görüntü geçiş** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out hizmet URL'sini ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. Başka bir tarayıcı penceresinde tooyour görüntü geçiş şirket sitede yönetici olarak oturum açın.

8. Merhaba hello üstte Hello araç çubuğunda tıklatın **kullanıcılar ve izinler** iş yükü.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. Tıklatın **oluşturma yeni izni**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. Merhaba, **tek oturum açma ayarları** iş yükü, select hello **bu grup için yalnızca oturum açma aracılığıyla çoklu oturum açma** onay kutusunu işaretleyin ve ardından **kaydetmek**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. Çok Git**hesap ayarlarını**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. Toohello Git **tek oturum açma ayarları** iş yükü.
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. Merhaba üzerinde **SAML ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    a. İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    b. İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **tek Sign-Out hizmeti URL'si** Azure portalından kopyalanan.

    c. Olarak **ad kimliği biçimi**seçin **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.

    d. Olarak **bağlama seçenekleri hello hizmet sağlayıcısı (görüntü geçiş) gelen istekleri için**seçin **POST bağlama**.

    e. Altında **x.509 sertifikası**, tıklatın **güncelleştirme sertifika**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    f. İndirilen hello sertifika Not Defteri'nde açın, hello içeriği Kopyala ve hello x.509 sertifikası metin kutusuna yapıştırın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    g. İçinde **Just-In-Time kullanıcı sağlamayı** bölümü, select hello **Just-In-Time kullanıcı sağlamayı etkinleştirin**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    h. Select hello izin grubu (örneğin, **SSO temel**) içinde toosign çoklu oturum açma yalnızca aracılığıyla izin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    ı. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-image-relay-test-user"></a>Bir görüntü geçiş test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate de görüntü geçişi Britta Simon adlı bir kullanıcı ' dir.

**toocreate Britta Simon görüntü geçiş adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Yönetici olarak oturum açma tooyour görüntü geçiş şirket sitesi.

2. Çok Git**kullanıcılar ve izinler** seçip **SSO kullanıcı oluştur**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. Merhaba girin **e-posta**, **ad**, **Soyadı**, ve **şirket** hello kullanıcısı tooprovision ve select hello izin grubu istediğiniz (örneğin, SSO temel) yalnızca çoklu oturum açma oturum açarak hello grup olduğu.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. **Oluştur**'a tıklayın.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooImage geçiş vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooImage geçiş hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **görüntü geçiş**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.    

Merhaba görüntü geçiş hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour görüntü geçiş uygulama almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

