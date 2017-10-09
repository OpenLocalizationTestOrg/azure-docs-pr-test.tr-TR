---
title: "Öğretici: Azure Active Directory Tümleştirme ile ADP Globalview | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ADP Globalview arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a>Öğretici: Azure Active Directory Tümleştirme ADP Globalview ile

Bu öğreticide, bilgi nasıl toointegrate ADP Globalview Azure Active Directory'ye (Azure AD).

ADP Globalview Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooADP Globalview sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooADP Globalview (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure ADP Globalview ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir ADP Globalview çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden ADP Globalview ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-adp-globalview-from-hello-gallery"></a>Merhaba Galerisi'nden ADP Globalview ekleme
Azure AD'ye tooconfigure hello tümleştirme ADP Globalview, tooadd ADP Globalview hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd ADP Globalview hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **ADP Globalview**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. Merhaba Sonuçlar panelinde seçin **ADP Globalview**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve ADP Globalview ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı

Tek toowork'ın oturum açma hangi hello karşılık gelen ADP Globalview içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ADP Globalview hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ADP Globalview içinde.

tooconfigure ve ADP Globalview ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[ADP Globalview test kullanıcısı oluşturma](#creating-an-adp-globalview-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ADP Globalview içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ADP Globalview uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ADP Globalview ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **ADP Globalview** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. Merhaba üzerinde **ADP Globalview etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<subdomain>.globalview.adp.com/federate` veya`https://<subdomain>.globalview.adp.com/federate2`

    > [!NOTE] 
    > Merhaba değeri gerçek değil. Merhaba değeri ile Merhaba güncelleştirin gerçek tanımlayıcısı. Kişi [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) tooget hello değeri.
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. Merhaba ADP GlobalView uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor. 

6. Aşağıdaki ekran görüntüsü hello için bir örneği gösterir. Merhaba talep adlarının her zaman olması **"PersonImmutableID"** ve hangisinin biz eşlenen içeren tooExtensionAttribute2 hello değeri hello hello kullanıcının EmployeeID. Burada Azure AD tooADP GlobalView hello kullanıcı eşlemeyi EmployeeID hello üzerinde gerçekleştirilir ancak tooa farklı değer de uygulama ayarlarınızı temel alan eşleyebilirsiniz. İş hello ADP GlobalView takım ilk toouse hello doğru tanıtıcısı bir kullanıcı ile ve bu değerle hello eşleyin **"PersonImmutableID"** talep. Ayrıca hello resimde görüldüğü gibi hello e-posta ve UserID talep eşleyebilirsiniz.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ------------------- | -------------------- |    
    | personalimmutableid | User.extensionattribute2 |
    | E-posta               | User.Mail |
    | Kullanıcı Kimliği              | User.userPrincipalName|
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. **Tamam**’a tıklayın.

    > [!NOTE] 
    > Merhaba SAML onayı yapılandırmadan önce toocontact gerekir, [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) ve kiracınız için hello benzersiz tanımlayıcı özniteliği hello değerini isteyin. Değer bu tooconfigure hello özel talep uygulamanız gerekir. 

8. Merhaba üzerinde **ADP Globalview yapılandırma** 'yi tıklatın **yapılandırma ADP Globalview** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. tooconfigure çoklu oturum açma üzerinde **ADP Globalview** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx).

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-adp-globalview-test-user"></a>ADP Globalview test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon ADP GlobalView adlı bir kullanıcı var. Çalışmak [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) tooadd hello hello ADP GlobalView hesap kullanıcılar. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooADP Globalview vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooADP Globalview, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ADP Globalview**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.  

ADP GlobalView döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma ADP GlobalView uygulama tooyour almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

