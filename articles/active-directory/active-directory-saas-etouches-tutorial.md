---
title: "Öğretici: Azure Active Directory Tümleştirme ile etouches | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile etouches arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>Öğretici: Azure Active Directory Tümleştirme etouches ile

Bu öğreticide, bilgi nasıl toointegrate etouches Azure Active Directory'ye (Azure AD).

Etouches Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooetouches sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooetouches (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure etouches ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir etouches çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden etouches ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-etouches-from-hello-gallery"></a>Merhaba Galerisi'nden etouches ekleme
Azure AD'ye tooconfigure hello tümleştirme etouches, tooadd etouches hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**Merhaba galerisinden tooadd etouches hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **etouches**seçin **etouches** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı etouches sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen etouches içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı etouches hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri etouches içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve etouches ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir etouches test kullanıcısı oluşturma](#create-an-etouches-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir etouches içinde.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma etouches uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile etouches, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **etouches** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. Merhaba üzerinde **etouches etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![etouches etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Hello ile gerçek hello değeri güncelleştirin URL ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcı oturum açın.
    > 

4. etouches uygulama hello SAML onaylar belirli bir biçimde bekler. Bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı özniteliği** hello uygulamasının. Ekran aşağıdaki hello bunun bir örneği gösterir. 

    ![Kullanıcı özniteliği](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ------------------- | -------------------- |
    | E-posta | User.Mail |    
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Öznitelik Ekle](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Öznitelik iletişim ekleyin](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. **Tamam**’a tıklayın. 

6. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget uygulamanız için yapılandırılmış SSO Merhaba etouches uygulaması adımlarını izleyerek hello gerçekleştirin: 

    ![etouches yapılandırma](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    a. Oturum açma çok**etouches** hello yönetici hakları kullanarak uygulama.
   
    b. Toohello Git **SAML** yapılandırma.

    c. Merhaba, **genel ayarları** bölümünde, Not Defteri'nde, kopyalama Merhaba içeriğine Azure Portalı'ndan indirilen sertifikanızı açın ve hello IDP meta verileri metin kutusuna yapıştırın. 

    d. Tıklatın hello üzerinde **kalmak & Kaydet** düğmesi.
  
    e. Tıklatın hello üzerinde **güncelleştirme meta verilerini** hello SAML meta veri bölümünden düğmesini. 

    f. Bu açılır sayfa hello ve SSO gerçekleştirin. Merhaba kullanıcı adına ayarlayın, sonra bir kez hello SSO çalışmaktadır.

    g. Merhaba Hello kullanıcı adı alanında seçin **emailaddress** hello resimde gösterildiği gibi. 

    h. Kopyalama hello **SP varlık kimliği** değer ve hello yapıştırma **tanımlayıcısı** bulunduğu textbox **etouches etki alanı ve URL'leri** Azure Portal'daki bölüm.

    ı. Kopyalama hello **SSO URL / ACS** değer ve hello yapıştırma **URL üzerinde oturum** bulunduğu textbox **etouches etki alanı ve URL'leri** Azure Portal'daki bölüm.
   
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-an-etouches-test-user"></a>Bir etouches test kullanıcısı oluşturma

Bu bölümde, etouches içinde Britta Simon adlı bir kullanıcı oluşturun. Çalışmak [etouches istemci destek ekibi](https://www.etouches.com/event-software/support/customer-support/) tooadd hello kullanıcılar hello etouches Platform.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooetouches vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooetouches hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **etouches**.

    ![Merhaba etouches bağlantı hello uygulamalar listesinde](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin


Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba erişim paneli etouches döşeme hello tıkladığınızda, otomatik olarak oturum açma tooyour etouches uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

