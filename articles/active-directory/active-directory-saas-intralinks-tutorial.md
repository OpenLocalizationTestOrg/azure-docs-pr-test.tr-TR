---
title: "Öğretici: Azure Active Directory Tümleştirme ile Intralinks | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Intralinks arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Öğretici: Azure Active Directory Tümleştirme Intralinks ile

Bu öğreticide, bilgi nasıl toointegrate Intralinks Azure Active Directory'ye (Azure AD).

Intralinks Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooIntralinks sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooIntralinks (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Intralinks ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Intralinks çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Intralinks ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-intralinks-from-hello-gallery"></a>Merhaba Galerisi'nden Intralinks ekleme
Azure AD'ye tooconfigure hello tümleştirme Intralinks, tooadd Intralinks hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Intralinks hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Intralinks**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Merhaba Sonuçlar panelinde seçin **Intralinks**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Intralinks sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Intralinks içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Intralinks hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Intralinks içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Intralinks ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Intralinks test kullanıcısı oluşturma](#creating-an-intralinks-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Intralinks içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Intralinks uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Intralinks, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Intralinks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. Merhaba üzerinde **Intralinks etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Intralinks istemci destek ekibi](https://www.intralinks.com/contact-1) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. tooconfigure çoklu oturum açma üzerinde **Intralinks** yan, indirilen toosend hello ihtiyacınız **meta veri XML** [Intralinks destek ekibi](https://www.intralinks.com/contact-1). Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-intralinks-test-user"></a>Bir Intralinks test kullanıcısı oluşturma

Bu bölümde, Intralinks içinde Britta Simon adlı bir kullanıcı oluşturun. Lütfen çalışmak [Intralinks destek ekibi](https://www.intralinks.com/contact-1) tooadd hello kullanıcılar hello Intralinks Platform.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooIntralinks vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooIntralinks hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Intralinks**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.

### <a name="add-intralinks-via-or-elite-application"></a>Intralinks aracılığıyla veya Elite uygulama ekleme

Intralinks kullandığı anlaşma Nexus uygulama hariç tüm diğer Intralinks uygulamalar için aynı SSO kimlik platformu hello. Başka bir Intralinks uygulama toouse düşünüyorsanız, bu nedenle daha sonra ilk tooconfigure SSO yukarıda açıklanan hello yordamı kullanarak birincil Intralinks uygulama için gerekir.

Bundan sonra yordamı tooadd aşağıda hello başka bir Intralinks uygulama kiracınızda hangi birincil bu uygulama için SSO yararlanabilirsiniz izleyebilirsiniz. 

>[!NOTE]
>Bu özellik kullanılabilir yalnızca tooAzure AD Premium SKU müşterileri içindir ve ücretsiz veya temel SKU müşteriler için kullanılamaz.

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]


2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Intralinks**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Üzerinde **uygulama Intralinks Ekle** hello aşağıdaki adımları gerçekleştirin:

    ![Intralinks aracılığıyla veya Elite uygulama ekleme](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    a. İçinde **adı** metin kutusuna, uygun Merhaba uygulaması örneğin adını **Intralinks Elite**.

    b. Tıklatın **Ekle** düğmesi.

6.  Hello hello üzerinde Azure portal'ın **Intralinks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

7. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **bağlantılı oturum açma**.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. Merhaba hello SP başlatılan SSO URL'den al [Intralinks takım](https://www.intralinks.com/contact-1) hello diğer Intralinks uygulama ve içinde girin **yapılandırma oturum açma URL'si** aşağıda gösterildiği gibi. 
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     Merhaba oturum üzerinde URL'si metin kutusuna desen aşağıdaki hello kullanarak kullanıcıların toosign üzerinde tooyour Intralinks uygulamanız tarafından kullanılan hello URL'yi yazın:
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. Merhaba bölümünde gösterildiği gibi Hello uygulama toouser veya grupları atama ** [atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Hello erişim paneli Intralinks döşeme hello tıkladığınızda, otomatik olarak oturum açma Intralinks uygulama tooyour almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

