---
title: "Öğretici: Azure Active Directory Tümleştirme bağdaştırıcısıyla Five9 artı (CTI, kişi Center aracıları) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Öğretici: Azure Active Directory Tümleştirme bağdaştırıcısıyla Five9 artı (CTI, kişi Center aracıları)

Bu öğreticide, bilgi nasıl toointegrate Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) ile Azure Active Directory (Azure AD).

Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooFive9 olan Azure AD artı bağdaştırıcı (CTI, kişi Center aracıları) kontrol edebilirsiniz
- Oturum açmış kullanıcıların tooautomatically get tooFive9 artı bağdaştırıcı (CTI, kişi Center aracıları) etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

bağdaştırıcısıyla Five9 artı (aşağıdaki öğelerindeki hello ihtiyacınız CTI, kişi Center aracıları), tooconfigure Azure AD tümleştirme:

- Bir Azure AD aboneliği
- Bir Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a>Merhaba Galerisi'nden Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) ekleme
Azure AD'ye tooconfigure hello tümleştirme Five9 artı bağdaştırıcısının (CTI, kişi Center aracıları) hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) gerekir.

**tooadd Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. Merhaba Sonuçlar panelinde seçin **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Five9 artı "Britta Simon" adlı bir test kullanıcıya bağlı bağdaştırıcı (CTI, kişi Center aracıları) ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Five9 artı bağdaştırıcısında (CTI, kişi Center aracıları) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Five9 artı bağdaştırıcısında (CTI, kişi Center aracıları) arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Five9 artı bağdaştırıcısında (CTI, kişi Center aracıları) atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Five9 artı bağdaştırıcı (yapı taşları aşağıdaki toocomplete hello ihtiyacınız CTI, kişi Center aracıları), Azure AD çoklu oturum açma testiyle:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) test kullanıcısı oluşturma](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave Britta Simon Five9 yanı sıra kullanıcı bağlantılı toohello Azure AD gösterimidir bağdaştırıcısı (CTI, kişi Center aracıları) içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure bağdaştırıcısıyla Five9 artı (CTI, kişi Center aracıları) hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. Merhaba üzerinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:

    |    Ortam      |       URL      |
    | :-- | :-- |
    | "Five9 Plus bağdaştırıcısı Microsoft Dynamics CRM için" | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | "Five9 Plus bağdaştırıcısı Zendesk için" | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | "Five9 Plus bağdaştırıcısı Aracısı Masaüstü araç seti için" | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:

    |      Ortam     |      URL      |
    | :--                  | :--           |
    | "Five9 Plus bağdaştırıcısı Microsoft Dynamics CRM için" | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | "Five9 Plus bağdaştırıcısı Zendesk için" | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | "Five9 Plus bağdaştırıcısı Aracısı Masaüstü araç seti için" | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) yapılandırmasını** 'yi tıklatın **yapılandırma Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)** tooopen **oturum açmayapılandırma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64), Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) destek ekibi](https://www.five9.com/about/contact). Ayrıca ek olarak, SSO daha fazla yapılandırmak için lütfen hello aşağıdaki toohello bağdaştırıcısı göre adımları izleyin:

    a. "Five9 artı bağdaştırıcısı Aracısı Masaüstü araç seti için" Yönetici Kılavuzu: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. "Five9 artı bağdaştırıcısı Microsoft Dynamics CRM için" Yönetici Kılavuzu: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. "Five9 artı bağdaştırıcısı Zendesk için" Yönetici Kılavuzu: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) test kullanıcısı oluşturma

Bu bölümde, Britta Simon Five9 artı bağdaştırıcısı (CTI, kişi Center aracıları) adlı bir kullanıcı oluşturun. Çalışmak [Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) destek ekibi](https://www.five9.com/about/contact) hello Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) platformu hello kullanıcıları eklemek için. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooFive9 artı bağdaştırıcı (CTI, kişi Center aracıları) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooFive9 artı bağdaştırıcı (CTI, kişi Center aracıları) hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Five9 artı bağdaştırıcı (CTI, kişi Center aracıları)**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Five9 artı bağdaştırıcı (CTI, kişi Center aracıları) uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

