---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler ZSCloud | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler ZSCloud arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>Öğretici: Azure Active Directory Tümleştirme Zscaler ZSCloud ile

Bu öğreticide, bilgi nasıl toointegrate Zscaler ZSCloud Azure Active Directory'ye (Azure AD).

Zscaler ZSCloud Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooZscaler ZSCloud sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooZscaler ZSCloud (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Zscaler ZSCloud ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Zscaler ZSCloud çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Zscaler ZSCloud ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>Merhaba Galerisi'nden Zscaler ZSCloud ekleme
Azure AD'ye tooconfigure hello tümleştirme Zscaler ZSCloud, tooadd Zscaler ZSCloud hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Zscaler ZSCloud hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Zscaler ZSCloud**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. Merhaba Sonuçlar panelinde seçin **Zscaler ZSCloud**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve Zscaler ZSCloud ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı

Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler ZSCloud içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zscaler ZSCloud hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Zscaler ZSCloud içinde.

tooconfigure ve Zscaler ZSCloud ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Zscaler ZSCloud test kullanıcısı oluşturma](#creating-a-zscaler-zscloud-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zscaler ZSCloud içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler ZSCloud uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Zscaler ZSCloud ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Zscaler ZSCloud** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. Merhaba üzerinde **Zscaler ZSCloud etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL, kullanıcıların toosign üzerinde tooyour tarafından ZScaler ZSCloud uygulama kullanılır.
    
    > [!NOTE] 
    > Bu değeri hello ile tooupdate sahip gerçek oturum açma URL'si. Kişi [Zscaler ZSCloud istemci destek ekibi](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Zscaler ZSCloud yapılandırma** 'yi tıklatın **yapılandırma Zscaler ZSCloud** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. Farklı web tarayıcısı penceresinde içinde tooyour ZScaler ZSCloud şirket site yönetici olarak oturum.

8. Hello içinde hello üst menüsünde **Yönetim**.
   
    ![Yönetim](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Yönetim")

9. Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.   
            
    ![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")

10. Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:   
                
    ![Kimlik doğrulama](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "kimlik doğrulaması")
   
    a. Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.

    b. Tıklatın **SAML çoklu oturum açma parametreleri**.

11. Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**

    ![Çoklu oturum açma](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "çoklu oturum açma")
    
    a. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello değerine **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.
    
    b. Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.
    
    c. tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.
    
    d. Seçin **SAML otomatik sağlamayı etkinleştir**.

12. Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Yönetim](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Yönetim")
    
    a. **Kaydet** düğmesine tıklayın.

    b. Tıklatın **şimdi etkinleştirmek**.

## <a name="configuring-proxy-settings"></a>Proxy ayarlarını yapılandırma
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>Internet Explorer'da tooconfigure hello proxy ayarları

1. Başlat **Internet Explorer**.

2. Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.   
    
     ![Internet Seçenekleri](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Seçenekleri")

3. Merhaba tıklatın **bağlantıları** sekmesi.   
  
     ![Bağlantıları](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "bağlantıları")

4. Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.

5. Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:   
   
    ![Proxy sunucusu](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy sunucusu")

    a. Seçin **AĞINIZ için bir proxy sunucusu kullan**.

    b. Başlangıç adresi metin kutusuna yazın **gateway.zscalerone.net**.

    c. Başlangıç bağlantı noktası metin kutusuna yazın **80**.

    d. Seçin **yerel adresler için proxy sunucuyu atla**.

    e. Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.

6. Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.

### <a name="creating-a-zscaler-zscloud-test-user"></a>Zscaler ZSCloud test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooZScaler ZSCloud, sağlanan tooZScaler ZSCloud olması gerekir.  
ZScaler ZSCloud Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:

1. İçinde tooyour oturum **Zscaler** Kiracı.

2. Tıklatın **Yönetim**.   
   
    ![Yönetim](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Yönetim")

3. Tıklatın **kullanıcı yönetimi**.   
        
     ![Ekleme](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "ekleme")

4. Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.
      
    ![Ekleme](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "ekleme")

5. Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:
        
    ![Kullanıcı ekleme](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "kullanıcı ekleme")
   
    a. Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** tooprovision istediğiniz geçerli bir AAD hesabının.

    b. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> API AAD kullanıcı hesaplarının ZScaler ZSCloud tooprovision tarafından sağlanan veya herhangi diğer ZScaler ZSCloud kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooZscaler ZSCloud vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooZscaler ZSCloud, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Zscaler ZSCloud**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.

Zscaler ZSCloud döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Zscaler ZSCloud uygulama tooyour almanız gerekir.

Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

