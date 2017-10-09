---
title: "Öğretici: Azure Active Directory Tümleştirme ile UNIFI | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile UNIFI arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a>Öğretici: Azure Active Directory Tümleştirme UNIFI ile

Bu öğreticide, bilgi nasıl toointegrate UNIFI Azure Active Directory'ye (Azure AD).

UNIFI Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooUNIFI sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooUNIFI (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure UNIFI ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir UNIFI çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden UNIFI ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-unifi-from-hello-gallery"></a>Merhaba Galerisi'nden UNIFI ekleme
Azure AD'ye tooconfigure hello tümleştirme UNIFI, tooadd UNIFI hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd UNIFI hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **UNIFI**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. Merhaba Sonuçlar panelinde seçin **UNIFI**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UNIFI sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen UNIFI içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı UNIFI hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri UNIFI içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve UNIFI ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Test kullanıcı bir UNIFI oluşturma](#creating-a-unifi-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir UNIFI içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma UNIFI uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile UNIFI, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **UNIFI** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. Merhaba üzerinde **UNIFI etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    Merhaba, **tanımlayıcısı** metin kutusuna, türü başlangıç değeri:`INVIEWlabs` 

4. Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://app.discoverunifi.com/login`

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. Merhaba üzerinde **UNIFI yapılandırma** 'yi tıklatın **yapılandırma UNIFI** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. Farklı web tarayıcısı penceresinde tooyour üzerinde oturum **UNIFI** yönetici olarak şirket site.

9. Tıklatın hello üzerinde **kullanıcılar**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. Tıklatın hello üzerinde **yeni kimlik sağlayıcı Ekle**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/app2.png)

11. Merhaba, **kimlik sağlayıcı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/app3.png) 

    a. Merhaba, **sağlayıcı adı** metin kutusuna, tür hello hello kimlik sağlayıcısı adını...

    b. Merhaba hello içinde **sağlayıcısı URL** metin kutusuna yapıştırın hello **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri.

    c. Açık hello hello Not Defteri'nde, Azure Portalı'ndan indirilen sertifika kaldırmak hello **---başlangıç sertifika---** ve **---son SERTİFİKAYI---** etiketi ve içeriği kalan hello yapıştırın Merhaba **sertifika** metin kutusu.

    d. Select hello **varsayılan bir sağlayıcı** onay kutusu.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-unifi-test-user"></a>UNIFI test kullanıcısı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı oluşturun. **UNIFI** hiçbir el ile yapılacak adımlar gerekli; bu nedenle otomatik kullanıcı sağlamayı destekler. Kullanıcılar, başarılı kimlik doğrulama hello Azure AD alanından sonra otomatik olarak oluşturulur.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooUNIFI vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooUNIFI hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **UNIFI**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

UNIFI döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma tooyour UNIFI uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

