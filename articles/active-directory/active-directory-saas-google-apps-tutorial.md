---
title: "Öğretici: Google Apps Azure Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Google Apps arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Öğretici: Google Apps Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Google Apps Azure Active Directory'ye (Azure AD).

Google Apps Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooGoogle uygulamaları sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooGoogle uygulamalara (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla bilgi tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Google Apps ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Google Apps çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Video öğretici
Nasıl tooEnable çoklu oturum açma tooGoogle uygulamaları 2 dakika içinde:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Sık Sorulan Sorular
1. **S: Azure AD çoklu oturum açma ile uyumlu Chromebooks ve diğer Chrome aygıtları misiniz?**
   
    A: Evet Chromebook cihazlarını Azure AD kimlik bilgilerini kullanarak içine mümkün toosign kullanıcılardır. Bu bkz [Google Apps destek makalesi](https://support.google.com/chrome/a/answer/6060880) neden hakkında bilgi için kimlik bilgilerini iki kez kullanıcılardan.

2. **S: ı çoklu oturum açma etkinleştirirseniz, kullanıcılar olacak kendi Azure AD kimlik bilgilerini toosign Google sınıf, GMail, Google sürücü, YouTube vb. gibi herhangi bir Google ürünü içine mümkün toouse olabilir?**
   
    A: Evet hangisini seçtiğinize bağlı [hangi Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) tooenable seçin veya kuruluşunuz için devre dışı bırakın.

3. **S: Google Apps Kullanıcılarım yalnızca bir kısmı için çoklu oturum açmayı etkinleştir?**
   
    A: Hayır çoklu oturum açma üzerinde hemen kapatılması, kendi Azure AD kimlik bilgilerine sahip tüm Google Apps kullanıcılar tooauthenticate gerektirir. Google Apps birden çok kimlik sağlayıcısı sahip desteklemediğinden hello kimlik sağlayıcısı Google Apps ortamınız için Azure AD ya da olabilir veya Google--ancak ikisini Merhaba, aynı anda.

4. **S: bir kullanıcının Windows oturum açtığı, bunlar otomatik olarak tooGoogle uygulamalar için bir parola istendiğinde alma olmadan kimlik doğrulaması olur mu?**
   
    Y: Bu senaryoyu etkinleştirmek için iki seçenek vardır. İlk olarak, kullanıcılar Windows 10 cihazlara üzerinden oturum [Azure Active Directory katılım](active-directory-azureadjoin-overview.md). Alternatif olarak, kullanıcıların etki alanına katılmış tooan şirket içi tek oturum açma tooAzure AD için etkin Active Directory Windows cihazları oturum bir [Active Directory Federasyon Hizmetleri (AD FS)](active-directory-aadconnect-user-signin.md) dağıtım. Her iki seçenek tooperform hello hello öğretici tooenable çoklu oturum açma Azure AD arasında aşağıdaki adımlarda gerektirir ve Google Apps.

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Google Apps hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-google-apps-from-hello-gallery"></a>Google Apps hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Google uygulamaların tooadd Google Apps hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**Google Apps hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Google Apps**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. Merhaba Sonuçlar panelinde seçin **Google Apps**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Google "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı uygulamalar ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Google Apps içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Google Apps hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Google Apps içinde.

tooconfigure ve Google Apps ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Google Apps test kullanıcısı oluşturma](#creating-a-google-apps-test-user)**  -toohave Britta Simon Google uygulamalardaki kullanıcı bağlantılı toohello Azure AD gösterimidir, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Google Apps uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Google Apps ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Google Apps** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Merhaba üzerinde **Google Apps etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Bu değer gerçek değil. Merhaba değerini hello gerçek oturum açma URL'si ile güncelleştirin. Merhaba başvurun [Google destek ekibi](https://www.google.com/contact/).
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Google Apps Yapılandırması** 'yi tıklatın **yapılandırma Google Apps** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML çoklu oturum açma hizmet URL'si ve değişiklik parola URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Tarayıcınızda yeni bir sekme açın ve oturum hello [Google Apps Yönetici Konsolu](http://admin.google.com/) yönetici hesabını kullanarak.

8. Tıklatın **güvenlik**. Merhaba bağlantısını görmüyorsanız, hello altında gizli olabilir **daha fazla denetim** hello ekranın hello menüsünde.
   
    ![Güvenlik'e tıklayın.][10]

9. Merhaba üzerinde **güvenlik** sayfasında, **çoklu oturum açmayı kurduğunuzda (SSO).**
   
    ![SSO'ı tıklatın.][11]

10. Yapılandırma değişiklikleri izleyen hello gerçekleştirin:
   
    ![SSO yapılandırın][12]
   
    a. Seçin **üçüncü taraf kimlik sağlayıcısı ile Kurulum SSO**.

    b. İçinde **oturum açma sayfası URL'si** alan Google Apps, hello değerini yapıştırın **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.

    c. Merhaba, **oturum kapatma sayfası URL'si** alan Google Apps, hello değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan. 

    d. Merhaba, **değiştirmek parola URL'si** alan Google Apps, hello değerini yapıştırın **değiştirmek parola URL'si**, Azure portalından kopyalanan. 

    e. Hello için Google Apps içinde **doğrulama sertifikası**, Azure Portalı'ndan indirilen karşıya yükleme hello sertifika.

    f. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-google-apps-test-user"></a>Google Apps test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon Google Apps yazılım adlı bir kullanıcı var. Google Apps otomatik sağlama, varsayılan olarak etkin olduğu destekler. Bu bölümdeki hiçbir şey yoktur. Bir kullanıcı zaten Google Apps yazılımda yoksa, tooaccess Google Apps yazılım çalıştığında yeni bir tane oluşturulur.

>[!NOTE] 
>Bir kullanıcı toocreate el ile gerekiyorsa hello başvurun [Google destek ekibi](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, tooGoogle uygulamaları erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooGoogle uygulamaları hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Google Apps**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, tek oturum açma ayarlarınızı, açık hello adresinden erişim Paneli'nde tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)hello test hesaba oturum açın ve tıklatın **Google Apps** döşeme hello erişim paneli.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png