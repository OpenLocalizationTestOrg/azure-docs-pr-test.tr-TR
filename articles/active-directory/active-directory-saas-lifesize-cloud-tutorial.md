---
title: "Öğretici: Azure Active Directory Tümleştirme Lifesize bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Lifesize bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>Öğretici: Azure Active Directory Tümleştirme Lifesize bulut ile

Bu öğreticide, bilgi toointegrate Lifesize bulut nasıl Azure Active Directory (Azure AD) ile.

Lifesize bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLifesize bulut sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooLifesize bulut (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Lifesize bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Lifesize bulut çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Lifesize bulut ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-lifesize-cloud-from-hello-gallery"></a>Merhaba Galerisi'nden Lifesize bulut ekleme
Azure AD'ye tooconfigure hello tümleştirme Lifesize bulutun tooadd Lifesize bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Lifesize bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Lifesize bulut**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. Merhaba Sonuçlar panelinde seçin **Lifesize bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve Lifesize bulut ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen Lifesize bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Lifesize bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Lifesize buluta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Lifesize bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Lifesize bulut test kullanıcısı oluşturma](#creating-a-lifesize-cloud-test-user)**  -toohave karşılık gelen, Britta Simon Lifesize bulutta kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Lifesize bulut uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Lifesize bulut ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Lifesize bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. Merhaba üzerinde **Lifesize bulut etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.lifesizecloud.com/ls/?acs`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.lifesizecloud.com/<companyname>`

     
4. Denetleme **Göster Gelişmiş URL ayarları**, adım aşağıdaki hello gerçekleştirin:  
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    Merhaba, **geçiş durumu** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >Lütfen bu hello gerçek değerler olmadığına dikkat edin. tooupdate hello ile bu değerlere sahip gerçek oturum açma URL'si, geçiş durumunu ve tanımlayıcısı. Kişi [Lifesize bulut istemci destek ekibi](https://www.lifesize.com/support) tooget oturum açma URL'si ve tanımlayıcı değerlerini ve alabilirsiniz geçiş durum değeri SSO yapılandırmasından hello öğreticinin ilerleyen bölümlerinde açıklanmıştır.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Lifesize bulut Yapılandırması** 'yi tıklatın **Lifesize bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. tooget SSO hello Lifesize bulut uygulama yönetici ayrıcalıklarıyla oturum uygulamanız için yapılandırılmış.

8. Merhaba sağ üst köşedeki adınızın tıklayın ve üzerinde hello ardından **Gelişmiş ayarları**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. Gelişmiş şimdi ayarları üzerinde hello hello içinde **SSO yapılandırma** bağlantı. Örneğiniz için hello SSO yapılandırma sayfası açılır.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. Şimdi hello SSO yapılandırma kullanıcı Arabirimi değerleri aşağıdaki hello yapılandırın.    
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    a. İçinde **kimlik sağlayıcısı veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.

    b.  İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    c. Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **X.509 sertifikası** metin kutusu.
  
    d. Hello SAML özniteliği hello değeri olarak eşlemeleri hello adı metin kutusuna girin **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    e. Merhaba SAML öznitelik eşlemesinde hello **Soyadı** metin kutusuna girin hello değeri olarak **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. Merhaba SAML öznitelik eşlemesinde hello **e-posta** metin kutusuna girin hello değeri olarak **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. Merhaba üzerinde tıklayabilirsiniz toocheck hello yapılandırma **Test** düğmesi.
   
    >[!NOTE]
    >Başarılı test erişim toousers veya hello testi gerçekleştirebilirsiniz grupları da sağlar ve Azure AD içinde toocomplete hello Yapılandırma Sihirbazı'nı gerekir.

12. Merhaba üzerinde denetleyerek Hello SSO etkinleştirmek **etkinleştirmek SSO** düğmesi.

13. Şimdi üzerinde hello tıklayın **güncelleştirme** böylece kaydedilen tüm hello ayarları düğmesi. Bu hello RelayState değer oluşturur. Kopya hello hello metin kutusuna oluşturulur, RelayState değeri yapıştırın, hello **geçiş durumunu** metin kutusu altında **Lifesize bulut etki alanı ve URL'leri** bölümü. 

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-lifesize-cloud-test-user"></a>Lifesize bulut test kullanıcısı oluşturma

Bu bölümde, Britta Simon Lifesize bulutta adlı bir kullanıcı oluşturun. Lifesize bulut otomatik kullanıcı sağlamayı desteklemiyor. Azure AD, başarılı kimlik doğrulamasından sonra hello kullanıcı otomatik olarak hello uygulamada sağlanacak. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooLifesize bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLifesize bulut hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Lifesize bulut**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Lifesize bulut döşeme hello erişim paneli hello tıkladığınızda, oturum açma sayfasına Lifesize bulut uygulamasının almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

