---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Zscaler arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a>Öğretici: Azure Active Directory Tümleştirme Zscaler ile

Bu öğreticide, Azure Active Directory (Azure AD) ile Zscaler tümleştirmek öğrenin.

Zscaler Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- Zscaler erişimi, Azure AD'de kontrol edebilirsiniz
- Otomatik olarak için Zscaler (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Zscaler ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Zscaler çoklu oturum açma abonelik etkin

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden Zscaler ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-zscaler-from-the-gallery"></a>Galeriden Zscaler ekleme
Azure AD Zscaler tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Zscaler eklemeniz gerekir.

**Galeriden Zscaler eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.

    ![Uygulamalar][3]

4. Arama kutusuna **Zscaler**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. Sonuçlar panelinde seçin **Zscaler**ve ardından **Ekle** uygulama eklemek için düğmesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zscaler sınayın.

Tekli çalışmaya oturum için Azure AD Zscaler karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının Zscaler ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Zscaler içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.

Yapılandırma ve Azure AD çoklu oturum açma Zscaler ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  - Internet Explorer proxy ayarlarını yapılandırmak için
3. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
4. **[Zscaler test kullanıcısı oluşturma](#creating-a-zscaler-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Zscaler sağlamak için.
5. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
6. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Zscaler uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma ile Zscaler yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında üzerinde **Zscaler** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. Üzerinde **Zscaler etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.zsclaer.net`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer gerçek oturum açma URL'si ile güncelleştirin. Kişi [Zscaler istemci destek ekibi](https://www.zscaler.com/company/contact) bu değeri alınamıyor. 

4. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. Üzerinde **Zscaler yapılandırma** 'yi tıklatın **yapılandırma Zscaler** açmak için **yapılandırma oturum açma** penceresi. Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. Farklı web tarayıcısı penceresinde ZScaler şirket sitenize yönetici olarak oturum açın.

8. Üstteki menüde tıklatın **Yönetim**.
   
    ![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Yönetim")

9. Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.   
            
    ![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")

10. İçinde **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, aşağıdaki adımları gerçekleştirin:   
                
    ![Kimlik doğrulama](./media/active-directory-saas-zscaler-tutorial/ic800208.png "kimlik doğrulaması")
   
    a. Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.

    b. Tıklatın **SAML çoklu oturum açma parametreleri**.

11. Üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfasında, aşağıdaki adımları uygulayın ve ardından **bitti**

    ![Çoklu oturum açma](./media/active-directory-saas-zscaler-tutorial/ic800209.png "çoklu oturum açma")
    
    a. Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **için kullanıcıların kimlik doğrulaması için gönderilir SAML portalın URL'sini** metin kutusu.
    
    b. İçinde **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.
    
    c. İndirilen sertifikanızı karşıya yüklemek için tıklayın **Zscaler pem**.
    
    d. Seçin **SAML otomatik sağlamayı etkinleştir**.

12. Üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:

    ![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Yönetim")
    
    a. **Kaydet** düğmesine tıklayın.

    b. Tıklatın **şimdi etkinleştirmek**.

## <a name="configuring-proxy-settings"></a>Proxy ayarlarını yapılandırma
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a>Internet Explorer proxy ayarlarını yapılandırmak için

1. Başlat **Internet Explorer**.

2. Seçin **Internet Seçenekleri** gelen **Araçları** açılan menü **Internet Seçenekleri** iletişim.   
    
     ![Internet Seçenekleri](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Seçenekleri")

3. Tıklatın **bağlantıları** sekmesi.   
  
     ![Bağlantıları](./media/active-directory-saas-zscaler-tutorial/ic769493.png "bağlantıları")

4. Tıklatın **LAN Ayarları** açmak için **LAN Ayarları** iletişim.

5. Proxy sunucu bölümünde, aşağıdaki adımları gerçekleştirin:   
   
    ![Proxy sunucusu](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy sunucusu")

    a. Seçin **AĞINIZ için bir proxy sunucusu kullan**.

    b. Adresi metin kutusuna yazın **gateway.zscaler.net**.

    c. Bağlantı noktası metin kutusuna yazın **80**.

    d. Seçin **yerel adresler için proxy sunucuyu atla**.

    e. Tıklatın **Tamam** kapatmak için **yerel ağ (LAN) ayarları** iletişim.

6. Tıklatın **Tamam** kapatmak için **Internet Seçenekleri** iletişim.

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!  Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    a. İçinde **adı** metin kutusuna, türü **BrittaSimon**.

    b. İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-zscaler-test-user"></a>Zscaler test kullanıcısı oluşturma

Azure AD kullanıcıları için ZScaler oturum açmak etkinleştirmek için bunlar için ZScaler sağlanmalıdır.  
ZScaler söz konusu olduğunda, sağlama bir el ile bir görevdir.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:

1. Oturum, **Zscaler** Kiracı.

2. Tıklatın **Yönetim**.   
   
    ![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Yönetim")

3. Tıklatın **kullanıcı yönetimi**.   
        
     ![Ekleme](./media/active-directory-saas-zscaler-tutorial/ic781036.png "ekleme")

4. İçinde **kullanıcılar** sekmesini tıklatın, **Ekle**.
      
    ![Ekleme](./media/active-directory-saas-zscaler-tutorial/ic781037.png "ekleme")

5. Kullanıcı Ekle bölümünde, aşağıdaki adımları gerçekleştirin:
        
    ![Kullanıcı ekleme](./media/active-directory-saas-zscaler-tutorial/ic781038.png "kullanıcı ekleme")
   
    a. Tür **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları** ve **departmanı** sağlamak istediğiniz geçerli bir AAD hesabının.

    b. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> API sağlama AAD kullanıcı hesaplarına ZScaler tarafından sağlanan veya herhangi diğer ZScaler kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atama

Bu bölümde, Britta Zscaler için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı atama][200] 

**Zscaler için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Zscaler**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Zscaler parçasında tıklattığınızda, otomatik olarak Zscaler uygulamanıza açan.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

