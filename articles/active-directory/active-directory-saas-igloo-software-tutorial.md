---
title: "Öğretici: Azure Active Directory Tümleştirme Igloo yazılımıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Igloo yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Öğretici: Azure Active Directory Tümleştirme Igloo yazılımıyla

Bu öğreticide, bilgi nasıl toointegrate Igloo yazılım Azure Active Directory'ye (Azure AD).

Igloo yazılım Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooIgloo yazılım sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooIgloo yazılım (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Igloo yazılım ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Igloo yazılım çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Igloo yazılım ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-igloo-software-from-hello-gallery"></a>Merhaba Galerisi'nden Igloo yazılım ekleme
Azure AD'ye tooconfigure hello tümleştirme Igloo yazılım tooadd Igloo yazılım hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Igloo yazılım hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Igloo yazılım**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. Merhaba Sonuçlar panelinde seçin **Igloo yazılım**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmak ve Igloo yazılım "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Igloo yazılım tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Igloo yazılım hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Igloo yazılımda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Igloo yazılım ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Igloo yazılım test kullanıcısı oluşturma](#creating-an-igloo-software-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Igloo yazılım, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Igloo yazılım uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Igloo yazılımıyla hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Igloo yazılım** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. Merhaba üzerinde **Igloo yazılım etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.igloocommmunities.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.igloocommmunities.com/saml.digest`

    c. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Kişi [Igloo yazılım istemci destek ekibi](https://www.igloosoftware.com/services/support) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. Merhaba üzerinde **Igloo yazılım yapılandırma** 'yi tıklatın **Igloo yazılımı Yapılandır** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Igloo yazılım şirket sitede yönetici olarak oturum açın.

8. Toohello Git **Denetim Masası**.
   
     ![Denetim Masası](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Denetim Masası")

9. Merhaba, **üyelik** sekmesini tıklatın, **ayarları oturum**.
   
    ![Ayarları'nda oturum](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Ayarları'nda oturum açın")

10. Hello SAML yapılandırma bölümü, tıklatın **SAML kimlik doğrulaması yapılandırma**.
   
    ![SAML Yapılandırması](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML yapılandırması")
   
11. Merhaba, **genel yapılandırma** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Genel yapılandırma](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "genel yapılandırma")

    a. Merhaba, **bağlantı adı** metin kutusuna, yapılandırmanız için özel bir ad yazın.
   
    b. Merhaba, **IDP oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
   
    c. Merhaba, **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.
    
    d. Seçin **oturum kapatma yanıt ve İstek HTTP türü** olarak **POST**.
   
    e. Açık, **base-64** kodlanmış sertifika Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde ve toohello yapıştırın **ortak sertifika** metin kutusu.
    
12. Merhaba, **yanıt ve kimlik doğrulama Yapılandırması**, hello aşağıdaki adımları gerçekleştirin:
    
    ![Yanıt ve kimlik doğrulama Yapılandırması](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "yanıt ve kimlik doğrulama yapılandırması")
  
      a. Olarak **kimlik sağlayıcısı**seçin **Microsoft ADFS**.
      
      b. Olarak **tanımlayıcı türü**seçin **e-posta adresi**. 

      c. Merhaba, **e-posta özniteliği** metin kutusuna, türü **emailaddress**.

      d. Merhaba, **ad özniteliği** metin kutusuna, türü **givenname**.

      e. Merhaba, **son Name özniteliği** metin kutusuna, türü **Soyadı**.

13. Aşağıdaki adımları toocomplete hello yapılandırma hello gerçekleştirin:
    
    ![Oturum açma kullanıcı oluşturma](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "oturum açma kullanıcı oluşturma") 

     a. Olarak **oturum açma kullanıcı oluşturma**seçin **yeni bir kullanıcı oturum sitenizdeki oluşturduğunuzda**.

     b. Olarak **ayarlarında oturum**seçin **"Oturum" ekranında kullanım SAML düğmesini**.

     c. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-igloo-software-test-user"></a>Bir Igloo yazılım test kullanıcısı oluşturma

TooIgloo yazılım sağlama, tooconfigure kullanıcı için eylem öğe yok.  

Yazılım tooIgloo kullanarak bir atanan kullanıcı çalıştığında toolog hello erişim paneli, Igloo yazılım hello kullanıcı var olup olmadığını denetler.  Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Igloo yazılım tarafından otomatik olarak oluşturulur.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooIgloo yazılım vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooIgloo yazılım, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Igloo yazılım**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Igloo yazılım hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Igloo yazılım uygulaması almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

