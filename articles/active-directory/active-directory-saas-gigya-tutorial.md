---
title: "Öğretici: Azure Active Directory Tümleştirme ile Gigya | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Gigya arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a>Öğretici: Azure Active Directory Tümleştirme Gigya ile

Bu öğreticide, bilgi nasıl toointegrate Gigya Azure Active Directory'ye (Azure AD).

Gigya Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooGigya sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooGigya (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Gigya ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Gigya çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Gigya ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-gigya-from-hello-gallery"></a>Merhaba Galerisi'nden Gigya ekleme
Azure AD'ye tooconfigure hello tümleştirme Gigya, tooadd Gigya hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Gigya hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Gigya**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. Merhaba Sonuçlar panelinde seçin **Gigya**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Gigya sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Gigya içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Gigya hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Gigya içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Gigya ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Gigya test kullanıcısı oluşturma](#creating-a-gigya-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Gigya içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Gigya uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Gigya, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Gigya** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. Merhaba üzerinde **Gigya etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<companyname>.gigya.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://fidm.gigya.com/saml/v2.0/<companyname>`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Gigya istemci destek ekibi](https://www.gigya.com/support-policy/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Gigya yapılandırma** 'yi tıklatın **yapılandırma Gigya** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. Farklı web tarayıcısı penceresinde Gigya şirket sitenize yönetici olarak oturum açın.

8. Çok Git**ayarları \> SAML oturum açma**ve ardından hello **Ekle** düğmesi.
   
    ![SAML oturum açma](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML oturum açma")

9. Merhaba, **SAML oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML Yapılandırması](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML yapılandırması")
   
    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.
   
    b. İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure Portalı'ndan kopyalanan. 
   
    c. İçinde **çoklu oturum açma hizmet URL'si** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si** Azure Portalı'ndan kopyalanan.
   
    d. İçinde **ad kimliği biçimi** metin kutusuna, Yapıştır hello değerini **ad tanımlayıcısı biçimi** Azure Portalı'ndan kopyalanan.
   
    e. Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **X.509 sertifikası** metin kutusu.
   
    f. Tıklatın **ayarlarını kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-gigya-test-user"></a>Gigya test kullanıcısı oluşturma

Gigya içine sipariş tooenable Azure AD kullanıcıların toolog bunların Gigya sağlanmalıdır.  
Gigya Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:

1. İçinde tooyour oturum **Gigya** yönetici olarak şirket site.

2. Çok Git**yönetici \> kullanıcıları yönetme**ve ardından **kullanıcıları davet**.
   
    ![Kullanıcıları yönetme](./media/active-directory-saas-gigya-tutorial/ic789535.png "kullanıcıları yönetme")

3. Merhaba kullanıcıları davet iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcıları davet](./media/active-directory-saas-gigya-tutorial/ic789536.png "kullanıcıları davet et")
   
    a. Merhaba, **e-posta** metin kutusuna, tooprovision istediğiniz geçerli bir Azure Active Directory hesap türü hello e-posta diğer adı.
    
    b. Tıklatın **davet kullanıcı**.
      
    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alırsınız.
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooGigya vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooGigya hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Gigya**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba Gigya hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Gigya uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

