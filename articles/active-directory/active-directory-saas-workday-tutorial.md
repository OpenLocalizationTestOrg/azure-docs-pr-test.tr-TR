---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workday | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile iş günü arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Öğretici: Azure Active Directory Tümleştirme ile iş günü

Bu öğreticide, bilgi nasıl toointegrate Workday Azure Active Directory'ye (Azure AD).

Workday Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooWorkday sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooWorkday (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Workday ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir iş günü çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Workday hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-workday-from-hello-gallery"></a>Workday hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme gününün hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd Workday gerekir.

**tooadd Workday hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Workday**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. Merhaba Sonuçlar panelinde seçin **Workday**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Workday ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen iş günü içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve iş günü içinde hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** iş günü içinde.

tooconfigure ve Workday ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir iş günü test kullanıcısı oluşturma](#creating-a-workday-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir iş günü içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Workday uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile iş günü, başlangıç aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Workday** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Merhaba üzerinde **Workday etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Bu değerler hello gerçek değildir. Bu değerler, oturum açma hello gerçek URL'si ve yanıt URL'si ile güncelleştirin. Yanıt URL'si bir alt etki alanı gibi olmalıdır: www, wd2, wd3, wd3 impl, wd5, wd5 impl). Aşağıdakine benzer kullanarak "*http://www.myworkday.com*" çalışır, ancak "*http://myworkday.com*" desteklemez. Kişi [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html) tooget bu değerleri. 
 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Workday yapılandırma** 'yi tıklatın **yapılandırma Workday** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. Farklı web tarayıcısı penceresinde tooyour Workday şirket sitede yönetici olarak oturum açın.

8. Çok Git**menü \> çalışma ekranı**.
   
    ![Çalışma ekranı](./media/active-directory-saas-workday-tutorial/IC782923.png "çalışma ekranı")

9. Çok Git**hesap yönetimini**.
   
    ![Hesap Yönetimi](./media/active-directory-saas-workday-tutorial/IC782924.png "hesap yönetimi")

10. Çok Git**Kiracı kurulumunu Düzenle – güvenlik**.
   
    ![Kiracı Güvenliği Düzenle](./media/active-directory-saas-workday-tutorial/IC782925.png "Kiracı güvenlik Düzenle")

11. Merhaba, **yönlendirme URL'lerini** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yönlendirme URL'lerini](./media/active-directory-saas-workday-tutorial/IC7829581.png "yeniden yönlendirme URL'leri")
   
    a. Tıklatın **Satır Ekle**.
   
    b. Merhaba, **oturum açma yeniden yönlendirme URL'si** textbox ve hello **mobil yeniden yönlendirme URL'sini** metin kutusuna, türü hello **oturum açma URL'si** üzerinde hello girdiğiniz **Workday etki alanı ve URL'leri** hello Azure portalı bölümü.
   
    c. Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **Sign-Out URL**ve hello yapıştırma **oturumu kapatıp tekrar yönlendirme URL'sini** metin kutusu.
   
    d.  İçinde **ortam** metin kutusuna, türü hello ortam adı.  

    >[!NOTE]
    > Merhaba hello ortamı özniteliğinin değeri bağlı hello Kiracı URL toohello değeri:  
    >-Hello Workday kiracısı URL'si hello etki alanı adı ile impl örneğin başlayıp başlamadığını: *https://impl.workday.com/\<Kiracı\>/login-saml2.htmld*), hello **ortam** öznitelik tooImplementation ayarlamanız gerekir.  
    >-Hello etki alanı adı başka bir şey ile başlayan, toocontact gerekir [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello eşleşen **ortam** değeri.

12. Merhaba, **SAML Kurulumu** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML Kurulumu](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Kurulumu")
   
    a.  Seçin **SAML kimlik doğrulamasını etkinleştirme**.
   
    b.  Tıklatın **Satır Ekle**.

13. Hello SAML kimlik sağlayıcısı bölümü, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML kimlik sağlayıcısı](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML kimlik sağlayıcısı")
   
    a. Merhaba kimlik sağlayıcı adı metin kutusuna bir sağlayıcı adı yazın (örneğin: *SPInitiatedSSO*).
   
    b. Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **SAML varlık kimliği** değer ve hello yapıştırma **veren** metin kutusu.
   
    c. Seçin **etkinleştirmek iş günü başlatılan oturum kapatma**.
   
    d. Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **Sign-Out URL** değer ve hello yapıştırma **oturum kapatma istek URL'si** metin kutusu.

    e. Tıklatın **kimlik sağlayıcısı ortak anahtar sertifikası**ve ardından **oluşturma**. 

    ![Oluşturma](./media/active-directory-saas-workday-tutorial/IC782928.png "oluşturma")

    f. Tıklatın **x509 oluşturma ortak anahtar**. 

    ![Oluşturma](./media/active-directory-saas-workday-tutorial/IC782929.png "oluşturma")


14. Merhaba, **görünüm x509 ortak anahtar** bölümünde, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Görünüm x509 ortak anahtar](./media/active-directory-saas-workday-tutorial/IC782930.png "görünüm x509 ortak anahtar") 
   
    a. Merhaba, **adı** metin kutusuna, sertifikanızı için bir ad yazın (örneğin: *PPE\_SP*).
   
    b. Merhaba, **geçerlilik başlangıcı** metin kutusuna, türü hello sertifikanızı öznitelik değerinden geçerli.
   
    c.  Merhaba, **için geçerli** metin kutusuna, sertifikanızı tür hello geçerli tooattribute değeri.
   
    > [!NOTE]
    > Merhaba tarihinden itibaren geçerli alın ve çift tıklatarak indirilen hello sertifikasından geçerli toodate hello.  Merhaba tarihleri hello altında listelenen **ayrıntıları** sekmesi.
    > 
    >
   
    d.  Base-64 kodlanmış sertifikanızı not defteri sonra bunu içerik kopyalama hello açın.
   
    e.  Merhaba, **sertifika** metin kutusuna, panonuza Yapıştır Merhaba içeriğine.
   
    f.  **Tamam** düğmesine tıklayın.

15. Merhaba aşağıdaki adımları gerçekleştirin: 
   
    ![SSO yapılandırma](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO yapılandırma")
   
    a.  Merhaba etkinleştirmek **x509 özel anahtar çifti**.
   
    b.  Merhaba, **hizmet sağlayıcı kimliği** metin kutusuna, türü **http://www.workday.com**.
   
    c.  Seçin **etkinleştir SP tarafından başlatılan SAML kimlik doğrulaması**.
   
    d.  Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **SAML çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **IDP SSO hizmet URL'si** metin kutusu.
   
    e. Seçin **SP tarafından başlatılan kimlik doğrulama isteği Deflate değil**.
   
    f. Olarak **kimlik doğrulama isteği imza yöntemi**seçin **SHA256**. 
   
    ![Kimlik doğrulama isteği imza yöntemi](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "kimlik doğrulama isteği imza yöntemi") 
   
    g. **Tamam** düğmesine tıklayın. 
   
    ![TAMAM](./media/active-directory-saas-workday-tutorial/IC782933.png "TAMAM")
<CE>

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-workday-test-user"></a>Bir iş günü test kullanıcısı oluşturma

tooget iş günü içinde sağlanan bir sınama kullanıcısı, gereksinim duyduğunuz toocontact hello [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html).
Merhaba [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html) hello kullanıcı sizin için oluşturur.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooWorkday vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooWorkday hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Workday**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

