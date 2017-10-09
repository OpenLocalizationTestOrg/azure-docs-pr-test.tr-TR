---
title: "Öğretici: Azure Active Directory Tümleştirme ile StatusPage | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile StatusPage arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a>Öğretici: Azure Active Directory Tümleştirme StatusPage ile

Bu öğreticide, bilgi nasıl toointegrate StatusPage Azure Active Directory'ye (Azure AD).

StatusPage Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooStatusPage sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooStatusPage (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure StatusPage ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir StatusPage çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden StatusPage ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-statuspage-from-hello-gallery"></a>Merhaba Galerisi'nden StatusPage ekleme
Azure AD'ye tooconfigure hello tümleştirme StatusPage, tooadd StatusPage hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd StatusPage hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **StatusPage**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. Merhaba Sonuçlar panelinde seçin **StatusPage**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı StatusPage sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen StatusPage içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı StatusPage hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri StatusPage içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve StatusPage ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[StatusPage test kullanıcısı oluşturma](#creating-a-statuspage-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir StatusPage içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma StatusPage uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile StatusPage, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **StatusPage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. Merhaba üzerinde **StatusPage etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > Merhaba StatusPage destek ekibi ile iletişime geçin [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest meta veri gerekli tooconfigure çoklu oturum açma. 
    >
    >a. Merhaba meta verilerden hello veren değerini kopyalayın ve hello yapıştırma **tanımlayıcısı** metin kutusu.
    >
    >b. Merhaba meta verilerden hello yanıt URL'si kopyalayıp hello yapıştırın **yanıt URL'si** metin kutusu.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **StatusPage yapılandırma** 'yi tıklatın **yapılandırma StatusPage** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. Başka bir tarayıcı penceresinde tooyour StatusPage şirket sitesinde yönetici olarak oturum açın.

8. Merhaba ana araç çubuğunda **hesabı Yönet**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. Merhaba tıklatın **çoklu oturum açma** sekmesi. 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. Merhaba SSO Kurulum sayfasında hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    a. Merhaba, **SSO hedef URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.

    b. İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **sertifika** metin kutusu. 

    c. Tıklatın **yapılandırma kaydetme**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-statuspage-test-user"></a>StatusPage test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde StatusPage adlı bir kullanıcı ' dir.

Yalnızca zaman sağlama StatusPage destekler. İçinde zaten etkinleştirdiğiniz [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).

**toocreate StatusPage içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Yönetici olarak oturum açma tooyour StatusPage şirket sitesi.

2. Hello içinde hello üst menüsünde **hesabı Yönet**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. Merhaba tıklatın **ekip üyelerinin** sekmesi. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. Tıklatın **Ekle ekip ÜYESİNE**. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. Türü hello **e-posta adresi**, **ad**, ve **soyad** geçerli bir kullanıcı olarak hello tooprovision istediğiniz ilgili metin kutuları. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. Olarak **rol**, seçin **İstemci Yöneticisi**.

7. Tıklatın **hesap oluştur**.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooStatusPage vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooStatusPage hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **StatusPage**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba StatusPage hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour StatusPage uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

