---
title: "Öğretici: Azure Active Directory Tümleştirme ile xMatters OnDemand | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile xMatters OnDemand arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Öğretici: Azure Active Directory Tümleştirme xMatters OnDemand ile

Bu öğreticide, bilgi nasıl toointegrate xMatters OnDemand Azure Active Directory'ye (Azure AD).

XMatters OnDemand Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooxMatters OnDemand sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooxMatters OnDemand (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure xMatters OnDemand ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Abonelik xMatters OnDemand çoklu oturum açma etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden xMatters OnDemand ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a>Merhaba Galerisi'nden xMatters OnDemand ekleme
Azure AD'ye tooconfigure hello tümleştirme xMatters OnDemand, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd xMatters OnDemand gerekir.

**tooadd xMatters OnDemand hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **xMatters OnDemand**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. Merhaba Sonuçlar panelinde seçin **xMatters OnDemand**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı OnDemand tabanlı xMatters ile test etme.

Tek toowork'ın oturum açma Azure AD tooknow hangi hello gereken xMatters OnDemand karşılık gelen kullanıcı tooa kullanıcı Azure AD içinde değil. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı xMatters hello arasında bir bağlantı ilişkisi OnDemand kurulan toobe gerekir.

Merhaba hello değerini xMatters OnDemand'da, Ata **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve xMatters OnDemand ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[XMatters OnDemand test kullanıcısı oluşturma](#creating-a-xmatters-ondemand-test-user)**  -toohave bir Britta Simon karşılık gelen xMatters kullanıcı bağlantılı toohello Azure AD gösterimidir OnDemand içinde.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma xMatters OnDemand uygulama yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile xMatters OnDemand, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **xMatters OnDemand** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. Merhaba üzerinde **xMatters OnDemand etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [xMatters OnDemand destek ekibi](https://www.xmatters.com/company/contact-us/) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyasını yerel olarak kaydedin **c:\\XMatters OnDemand.cer**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > Tooforward hello sertifika toohello gerek [xMatters OnDemand destek ekibi](https://www.xmatters.com/company/contact-us/). Merhaba sertifikanın oturum açma hello tek yapılandırmasını son haline getirmek önce hello xMatters destek ekibi tarafından karşıya toobe gerekir. 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **xMatters OnDemand yapılandırma** 'yi tıklatın **xMatters OnDemand yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. Farklı web tarayıcısı penceresinde içinde tooyour XMatters OnDemand şirket site yönetici olarak oturum.

8. Merhaba üstte Hello araç çubuğunda **yönetici**ve ardından **şirket ayrıntıları** yan sol hello hello gezinti çubuğunda.
   
    ![Yönetici](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "yönetici")

9. Merhaba üzerinde **SAML Yapılandırması** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML Yapılandırması](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML yapılandırması")
   
    a. Seçin **etkinleştirmek SAML**.
   
    b. Yapıştır **SAML varlık kimliği**, hello hello Azure portal ' Kopyalanan **kimlik sağlayıcı kimliği** metin kutusu.
   
    c. Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **üzerinde tek oturum URL'si** metin kutusu.
   
    d. Yapıştır **Sign-Out URL**, hello hello Azure portal ' Kopyalanan **çoklu oturum kapatma URL'si** metin kutusu.
   
    e. Merhaba üstünde hello şirket Ayrıntıları sayfası tıklayın **Değişiklikleri Kaydet**.
    
    ![Şirket ayrıntıları](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "şirket ayrıntıları")

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-xmatters-ondemand-test-user"></a>XMatters OnDemand test kullanıcısı oluşturma

TooXMatters OnDemand içinde sipariş tooenable Azure AD kullanıcıların toolog bunların XMatters OnDemand sağlanmalıdır. XMatters OnDemand Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:
1. İçinde tooyour oturum **XMatters OnDemand** Kiracı.

2.  Tıklatın **kullanıcılar** sekmesini ve ardından **Kullanıcı Ekle**.
  
    ![Kullanıcıların](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "kullanıcılar")

3. Merhaba, **kullanıcı ekleme** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı ekleme](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "kullanıcı ekleme")

    a. Seçin **etkin**.

    b. Merhaba, **kullanıcı kimliği** metin kutusuna, türü hello kullanıcının kimliği gibi Brittasimon@contoso.com.
   
    c. Merhaba, **ad** metin kutusuna, adı Britta gibi hello kullanıcı türü.

    d. Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını Simon gibi.
    
    e. Merhaba, **Site** metin kutusu, geçerli bir Azure Enter hello geçerli site tooprovision istediğiniz AD hesabı.
    
    f. **Kaydet** düğmesine tıklayın.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooxMatters OnDemand vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooxMatters OnDemand, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **xMatters OnDemand**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba xMatters hello erişim paneli OnDemand parçasında tıkladığınızda, otomatik olarak oturum açma tooyour xMatters OnDemand uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

