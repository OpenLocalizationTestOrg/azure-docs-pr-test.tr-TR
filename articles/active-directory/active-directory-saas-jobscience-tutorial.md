---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jobscience | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jobscience arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Öğretici: Azure Active Directory Tümleştirme Jobscience ile

Bu öğreticide, bilgi nasıl toointegrate Jobscience Azure Active Directory'ye (Azure AD).

Jobscience Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooJobscience sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooJobscience (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Jobscience ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Jobscience çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Jobscience ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-jobscience-from-hello-gallery"></a>Merhaba Galerisi'nden Jobscience ekleme
Azure AD'ye tooconfigure hello tümleştirme Jobscience, tooadd Jobscience hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Jobscience hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Jobscience**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. Merhaba Sonuçlar panelinde seçin **Jobscience**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Jobscience ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Jobscience içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Jobscience hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Jobscience içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Jobscience ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Jobscience test kullanıcısı oluşturma](#creating-a-jobscience-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Jobscience içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Jobscience uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Jobscience, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Jobscience** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. Merhaba üzerinde **Jobscience etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Bu değer alma [Jobscience istemci destek ekibi](https://www.jobscience.com/support) veya hello SSO profilinden hello öğreticinin ilerleyen bölümlerinde açıklanan oluşturur. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Jobscience yapılandırma** 'yi tıklatın **yapılandırma Jobscience** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. İçinde tooyour Jobscience şirket site yönetici olarak oturum açın.

8. Çok Git**Kurulum**.
   
   ![Kurulum](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Kurulumu")

9. Merhaba de hello sol gezinti bölmesindeki **Yönet** 'yi tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello ** Etki alanım** sayfası. 
   
   ![Etki alanım](./media/active-directory-saas-jobscience-tutorial/ic767825.png "etki alanım")

10. etki alanınızın doğru olarak ayarlanmış tooverify alanında olduğundan emin olun "**4 adım dağıtılan tooUsers**" ve gözden geçirin, "**My etki alanı ayarları**".

    ![Etki alanı dağıtıldı tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "etki alanı dağıtılan tooUser")

11. Merhaba Jobscience şirket sitesinde tıklatın **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.
    
    ![Güvenlik denetimleri](./media/active-directory-saas-jobscience-tutorial/ic784364.png "güvenlik denetimleri")

12. Merhaba, **çoklu oturum açma ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açma ayarları](./media/active-directory-saas-jobscience-tutorial/ic781026.png "tek oturum açma ayarları")
    
    a. Seçin **SAML etkin**.

    b. **Yeni**’ye tıklayın.

13. Merhaba üzerinde **SAML çoklu oturum açma ayarını Düzenle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
    
    ![Oturum açma SAML tek ayar](./media/active-directory-saas-jobscience-tutorial/ic784365.png "oturum açma SAML tek ayar")
    
    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.

    b. İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.

    c. Merhaba, **varlık kimliği** metin kutusuna, türü`https://salesforce-jobscience.com`

    d. Tıklatın **Gözat** tooupload Azure AD sertifikanızı.

    e. Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.

    f. Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentfier öğesinde hello konu deyimi**.

    g. İçinde **kimlik sağlayıcısı oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.

    h. İçinde **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.

    ı. **Kaydet** düğmesine tıklayın.

14. Merhaba de hello sol gezinti bölmesindeki **Yönet** 'yi tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello ** Etki alanım** sayfası. 
    
    ![Etki alanım](./media/active-directory-saas-jobscience-tutorial/ic767825.png "etki alanım")

15. Merhaba üzerinde **My etki alanı** sayfasında hello **oturum açma sayfası markalama** 'yi tıklatın **Düzenle**.
    
    ![Oturum açma sayfası markalama](./media/active-directory-saas-jobscience-tutorial/ic767826.png "oturum açma sayfası markalama")

16. Merhaba üzerinde **oturum açma sayfası markalama** sayfasında hello **kimlik doğrulama hizmeti** bölümü, hello adını, **SAML SSO ayarları** görüntülenir. Seçin ve ardından **kaydetmek**.
    
    ![Oturum açma sayfası markalama](./media/active-directory-saas-jobscience-tutorial/ic784366.png "oturum açma sayfası markalama")

17. tooget hello SP tarafından başlatılan çoklu oturum açma hello üzerinde oturum açma URL'si tıklatıldığında **çoklu oturum açma ayarları** hello içinde **güvenlik denetimleri** menü bölümü.

    ![Güvenlik denetimleri](./media/active-directory-saas-jobscience-tutorial/ic784368.png "güvenlik denetimleri")
    
    Merhaba Yukarıdaki adımda oluşturduğunuz hello SSO profiline tıklayın. Bu sayfa hello çoklu oturum açma URL'SİNDE şirketiniz için gösterir (örneğin, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-jobscience-test-user"></a>Jobscience test kullanıcısı oluşturma

TooJobscience içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Jobscience sağlanmalıdır. Jobscience Hello durumda sağlama bir el ile bir görevdir.

>[!NOTE]
>API, kullanıcı hesaplarını Jobscience tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer Jobscience kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
>  
        
**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Jobscience** yönetici olarak şirket site.

2. TooSetup gidin.
   
   ![Kurulum](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Kurulumu")
3. Çok Git**kullanıcıları yönetme \> kullanıcılar**.
   
   ![Kullanıcıların](./media/active-directory-saas-jobscience-tutorial/ic784369.png "kullanıcılar")
4. Tıklatın **yeni kullanıcı**.
   
   ![Tüm kullanıcılar](./media/active-directory-saas-jobscience-tutorial/ic784370.png "tüm kullanıcılar")
5. Merhaba üzerinde **kullanıcı düzenleme** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı düzenleme](./media/active-directory-saas-jobscience-tutorial/ic784371.png "kullanıcı düzenleme")
   
   a. Merhaba, **ad** metin kutusuna, Britta gibi hello kullanıcının ilk adını yazın.
   
   b. Merhaba, **Soyadı** metin kutusuna, Simon gibi hello kullanıcının soyadını yazın.
   
   c. Merhaba, **diğer** metin kutusuna, hello kullanıcı brittas gibi diğer adını yazın.

   d. Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.

   e. Merhaba, **kullanıcı adı** metin kutusuna, türü kullanıcının kullanıcı adını ister Brittasimon@contoso.com.

   f. Merhaba, **takma ad** metin kutusu, kullanıcı Simon gibi takma adını yazın.

   g. **Kaydet** düğmesine tıklayın.

    
> [!NOTE]
> Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooJobscience vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooJobscience hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Jobscience**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Jobscience hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Jobscience uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

