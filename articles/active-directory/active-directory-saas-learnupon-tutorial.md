---
title: "Öğretici: Azure Active Directory Tümleştirme ile LearnUpon | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LearnUpon arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a>Öğretici: Azure Active Directory Tümleştirme LearnUpon ile

Bu öğreticide, bilgi nasıl toointegrate LearnUpon Azure Active Directory'ye (Azure AD).

LearnUpon Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLearnUpon sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooLearnUpon (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure LearnUpon ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir LearnUpon çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden LearnUpon ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-learnupon-from-hello-gallery"></a>Merhaba Galerisi'nden LearnUpon ekleme
Azure AD'ye tooconfigure hello tümleştirme LearnUpon, tooadd LearnUpon hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd LearnUpon hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **LearnUpon**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. Merhaba Sonuçlar panelinde seçin **LearnUpon**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LearnUpon sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen LearnUpon içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LearnUpon hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri LearnUpon içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve LearnUpon ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[LearnUpon test kullanıcısı oluşturma](#creating-a-learnupon-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LearnUpon içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LearnUpon uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile LearnUpon, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **LearnUpon** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. Merhaba üzerinde **LearnUpon etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.learnupon.com/saml/consumer`

    > [!NOTE] 
    > Lütfen bu hello gerçek değer olmadığını unutmayın. tooupdate hello gerçek yanıt URL'si ile bu değere sahip. Bu değer tooget başvurun [LearnUpon destek ekibi](https://www.learnupon.com/features/support/).



4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **LearnUpon yapılandırma** 'yi tıklatın **yapılandırma LearnUpon** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. Başka bir tarayıcı örneği ve oturum açma LearnUpon bir yönetici hesabıyla açın. 

8. Merhaba tıklatın **ayarları** sekmesi.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. Tıklatın **çoklu oturum açma - SAML**ve ardından **genel ayarları** tooconfigure SAML ayarlar.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. Merhaba, **genel ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    a. Seçin **etkin**.

    b. Seçin **sürüm** olarak **2.0**.

    c. Seçin **Skip koşullar** olarak **Hayır**.

    d. Merhaba, **SAML belirteci sonrası parametre adı** metin kutusuna, tür hello adı doğrulandı ve kimlik doğrulaması - örneğin hello SAML onayı toobe içeren SAML tüketici URL belirtilen yukarıda isteği post parametresi toohello  **SAMLResponse**.

    e. Merhaba, **ad tanımlayıcısı biçimi** metin kutusuna, türü hello SAML onayı hello kullanıcılarınızın tanımlayıcısı (e-posta adresi) - örneğin bulunduğu gösteren bir değer **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.
  
    f. Merhaba, **tanımlamak sağlayıcı konumu** metin kutusuna, türü hello kullanıcılar tooif gönderilen hello burada gösteren bir değer bunlar tıklayın, Azure portalı oturum açma ekranından karşıya yüklenen simge.
  
    g. Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello **Sign-Out URL** hello Azure portal ' Kopyalanan.
    
    h. Tıklatın **parmak baskı siparişi yönetmek**ve indirilen sertifikanızın hello parmak izi karşıya yükleyin.

11. Tıklatın **kullanıcı ayarlarını**ve ardından hello aşağıdaki adımları gerçekleştirin:
   
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    a. Merhaba, **ilk ad tanımlayıcısı biçimi** metin kutusuna, bize, SAML onayı hello kullanıcılar firstname burada içinde söyler türü hello değeri bulunduğu - örneğin: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
  
    b. Merhaba, **son ad tanımlayıcısı biçimi** metin kutusuna, bize, SAML onayı hello kullanıcılar lastname burada içinde söyler türü hello değeri bulunduğu - örneğin: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-learnupon-test-user"></a>LearnUpon test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon içinde LearnUpon adlı bir kullanıcı ' dir. LearnUpon yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümde, eylem öğe yok. Henüz yoksa yeni bir kullanıcı bir girişim tooaccess LearnUpon sırasında oluşturulur. [Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>Bir kullanıcı toocreate el ile gerekiyorsa, toocontact gerek [LearnUpon destek ekibi](https://www.learnupon.com/features/support/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooLearnUpon vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLearnUpon hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **LearnUpon**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba LearnUpon hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour LearnUpon uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

