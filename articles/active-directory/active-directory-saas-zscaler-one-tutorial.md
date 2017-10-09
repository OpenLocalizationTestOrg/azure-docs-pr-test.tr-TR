---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler bir | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler bir arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 5179cb2cc54482334d574951a1ac64e722e5f578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a>Öğretici: Azure Active Directory Tümleştirme ile Zscaler bir

Bu öğreticide, bilgi nasıl toointegrate Zscaler bir Azure Active Directory'ye (Azure AD).

Zscaler bir Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooZscaler biri olan Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooZscaler biri (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Zscaler bir ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Zscaler bir çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Zscaler bir hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-zscaler-one-from-hello-gallery"></a>Zscaler bir hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme, Zscaler bir hello galeri tooyour yönetilen SaaS uygulamaları listesinden Zscaler bir tooadd gerekir.

**tooadd Zscaler bir hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Zscaler bir**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. Merhaba Sonuçlar panelinde seçin **Zscaler bir**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Zscaler "Britta Simon" adlı bir test kullanıcı tabanlı bir test.

Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler bir içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Zscaler bir arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bir Zscaler içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Zscaler bir ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları
3. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
4. **[Zscaler bir test kullanıcısı oluşturma](#creating-a-zscaler-one-test-user)**  -toohave Britta Simon Zscaler bağlantılı toohello Azure AD kullanıcı gösterimi olan bir içinde karşılık gelen.
5. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
6. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler bir uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Zscaler bir hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Zscaler bir** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. Merhaba üzerinde **Zscaler bir etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    Merhaba oturum açma URL'si metin kutusuna, kullanıcıların toosign üzerinde tooyour tarafından Zscaler bir uygulama kullanılan hello URL'sini yazın.

    > [!NOTE] 
    > Bu değeri hello ile tooupdate sahip gerçek oturum açma URL'si. Kişi [Zscaler bir istemci destek ekibi](https://www.zscaler.com/company/contact) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Zscaler bir yapılandırma** 'yi tıklatın **Zscaler bir yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Zscaler bir şirket sitede yönetici olarak oturum açın.

8. Hello içinde hello üst menüsünde **Yönetim**.
   
    ![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Yönetim")

9. Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.   
            
    ![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")

10. Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:   
                
    ![Kimlik doğrulama](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "kimlik doğrulaması")
   
    a. Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.

    b. Tıklatın **SAML çoklu oturum açma parametreleri**.

11. Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**

    ![Çoklu oturum açma](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "çoklu oturum açma")
    
    a. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.
    
    b. Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.
    
    c. tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.
    
    d. Seçin **SAML otomatik sağlamayı etkinleştir**.

12. Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Yönetim")
    
    a. **Kaydet** düğmesine tıklayın.

    b. Tıklatın **şimdi etkinleştirmek**.

## <a name="configuring-proxy-settings"></a>Proxy ayarlarını yapılandırma
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>Internet Explorer'da tooconfigure hello proxy ayarları

1. Başlat **Internet Explorer**.

2. Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.   
    
     ![Internet Seçenekleri](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Seçenekleri")

3. Merhaba tıklatın **bağlantıları** sekmesi.   
  
     ![Bağlantıları](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "bağlantıları")

4. Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.

5. Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:   
   
    ![Proxy sunucusu](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy sunucusu")

    a. Seçin **AĞINIZ için bir proxy sunucusu kullan**.

    b. Başlangıç adresi metin kutusuna yazın **gateway.zscalerone.net**.

    c. Başlangıç bağlantı noktası metin kutusuna yazın **80**.

    d. Seçin **yerel adresler için proxy sunucuyu atla**.

    e. Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.

6. Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-zscaler-one-test-user"></a>Zscaler bir test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooZscaler biri, sağlanan tooZscaler biri olması gerekir. Merhaba Zscaler bir içinde sağlama el ile bir görev durumudur.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:

1. İçinde tooyour oturum **Zscaler bir** Kiracı.

2. Tıklatın **Yönetim**.   
   
    ![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Yönetim")

3. Tıklatın **kullanıcı yönetimi**.   
        
     ![Ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "ekleme")

4. Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.
      
    ![Ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "ekleme")

5. Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:
        
    ![Kullanıcı ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "kullanıcı ekleme")
   
    a. Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** geçerli bir Azure AD hesabının tooprovision istiyor.

    b. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> API'leri, Azure AD kullanıcı hesapları Zscaler bir tooprovision tarafından sağlanan veya herhangi diğer Zscaler bir kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooZscaler biri vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooZscaler bir hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Zscaler bir**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Zscaler bir hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zscaler bir uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

