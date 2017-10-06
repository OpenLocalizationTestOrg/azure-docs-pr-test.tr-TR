---
title: "Öğretici: Azure Active Directory Tümleştirme ile ServiceNow | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve ServiceNow ve ServiceNow Express arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Öğretici: ServiceNow Azure Active Directory Tümleştirme
Bu öğreticide, bilgi nasıl toointegrate ServiceNow ve ServiceNow Express Azure Active Directory'ye (Azure AD).

ServiceNow ve ServiceNow Express Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

* Erişim tooServiceNow olan Azure AD ve ServiceNow Express kontrol edebilirsiniz
* Azure AD hesaplarına açan kullanıcıları tooautomatically get tooServiceNow ve ServiceNow Express (çoklu oturum açma) etkinleştir
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
Azure AD ile tümleştirme ServiceNow ve ServiceNow Express tooconfigure, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* ServiceNow, örneği veya ServiceNow, Calgary sürüm Kiracı için veya üzeri
* ServiceNow Express, ServiceNow Express, Helsinki sürüm örneği için veya üzeri
* Merhaba ServiceNow Kiracı hello olmalıdır [birden çok sağlayıcı tek oturum üzerinde eklentisi](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) etkin. Bu yapılabilir [hizmet isteği göndererek](https://hi.service-now.com). 

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.
> 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. ServiceNow hello Galerisi'nden ekleme
2. Çoklu oturum açmayı ServiceNow veya ServiceNow Express için yapılandırma ve Azure AD sınama

## <a name="adding-servicenow-from-hello-gallery"></a>ServiceNow hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme ServiceNow veya ServiceNow Express tooadd ServiceNow hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir. 

**tooadd ServiceNow hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1]
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2]
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]
6. Merhaba arama kutusuna yazın **ServiceNow**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. Merhaba sonuçlar bölmesinde seçin **ServiceNow**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve ServiceNow veya ServiceNow Express ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen ServiceNow içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve ServiceNow hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.
Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ServiceNow içinde. tooconfigure ve ServiceNow ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma için ServiceNow yapılandırma](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Azure AD çoklu oturum açma için ServiceNow Express yapılandırma](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable kullanıcılar toouse bu özellik.
3. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
4. **[ServiceNow test kullanıcısı oluşturma](#creating-a-servicenow-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir ServiceNow içinde Britta Simon biri.
5. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
6. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

> [!NOTE]
> 2. adım tooconfigure ServiceNow istiyorsanız atlayın. Benzer şekilde, tooconfigure istiyorsanız, 1. adım ServiceNow Express atlayın.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Azure AD çoklu oturum açma ServiceNow için yapılandırma
1. Hello Azure AD Klasik portalında, hello **ServiceNow** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim .
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")

2. Merhaba üzerinde **nasıl tooServiceNow üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749324.png "çoklu oturum açmayı yapılandırın")

3. Merhaba üzerinde **uygulama ayarlarını yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC769497.png "uygulama URL'sini yapılandırın")
   
    a. Merhaba, **üzerinde ServiceNow oturum URL'si** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan: `https://<instance-name>.service-now.com`.
   
    b. Merhaba, **tanımlayıcısı** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan: `https://<instance-name>.service-now.com`.
   
    c. **İleri**’ye tıklayın

4. toohave Azure AD otomatik olarak ServiceNow SAML tabanlı kimlik doğrulaması için yapılandırma, ServiceNow örneği adı, yönetici kullanıcı adı ve yönetici parolası hello girin **otomatik yapılandır çoklu oturum açma** form ve tıklayın  *Yapılandırma*. Sağlanan bu hello yönetici kullanıcı adı, hello olmalıdır Not **security_admin** ServiceNow içinde bu toowork için atanan rolü. Aksi takdirde, toomanually ServiceNow toouse Azure AD SAML kimlik sağlayıcısı yapılandırın, tıklatın **el ile Merhaba uygulaması çoklu oturum açma için yapılandırma**, ardından **sonraki** ve tam hello Aşağıdaki adımlar.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "uygulama URL'sini yapılandırın")

5. Hello üzerinde **Servicenow'da çoklu oturum açma yapılandırma** sayfasında, **indirme sertifika**, yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749325.png "çoklu oturum açmayı yapılandırın")

6. Oturum açma ServiceNow uygulama yönetici olarak tooyour.

7. Merhaba etkinleştirme *tümleştirmesi - birden çok sağlayıcı tek oturum açma yükleyicisini* izleyerek eklentisi hello sonraki adımlar:
   
    a. Merhaba sol tarafında Hello Gezinti Bölmesi'nde çok Git**sistem tanımı** bölümünde ve ardından **eklentileri**.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "eklentisini etkinleştirme")
   
    b. Arama *tümleştirmesi - birden çok sağlayıcı tek oturum açma yükleyicisini*.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "eklentisini etkinleştirme")
   
    c. Merhaba eklentisi seçin. Rigth tıklayın ve **etkinleştir/yükseltme**.
   
    d. Merhaba tıklatın **etkinleştirme** düğmesi.

8. Merhaba Gezinti hello sol taraftaki bölmede **özellikleri**.  
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "uygulama URL'sini yapılandırın")

9. Merhaba üzerinde **birden çok sağlayıcı SSO özelliklerini** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "uygulama URL'sini yapılandırın")
   
    a. Olarak **birden çok sağlayıcı SSO etkinleştirme**seçin **Evet**.
   
    b. Olarak **hata ayıklama günlüğünü var etkinleştir hello birden çok sağlayıcı SSO tümleştirme**seçin **Evet**.
   
    c. İçinde **hello alan hello kullanıcı tablo...**  metin kutusuna, türü **user_name**.
   
    d. **Kaydet** düğmesine tıklayın.

10. Merhaba Gezinti hello sol taraftaki bölmede **x509 sertifikaları**.
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "çoklu oturum açmayı yapılandırın")

11. Merhaba üzerinde **X.509 sertifikalarını** iletişim kutusunda, tıklatın **yeni**.
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "çoklu oturum açmayı yapılandırın")

12. Merhaba üzerinde **X.509 sertifikalarını** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "çoklu oturum açmayı yapılandırın")
    
     a. **Yeni**’ye tıklayın.
    
     b. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **TestSAML2.0**).
    
     c. Seçin **etkin**.
    
     d. Olarak **biçimi**seçin **PEM**.
    
     e. Olarak **türü**seçin **deposu sertifika güven**.
    
     f. Base64 ile kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **PEM sertifika** metin kutusu.
    
     g. Tıklatın **güncelleştirme**.

13. Merhaba Gezinti hello sol taraftaki bölmede **kimlik sağlayıcıları**.
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "çoklu oturum açmayı yapılandırın")

14. Merhaba üzerinde **kimlik sağlayıcıları** iletişim kutusunda, tıklatın **yeni**:
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "çoklu oturum açmayı yapılandırın")

15. Merhaba üzerinde **kimlik sağlayıcıları** iletişim kutusunda, tıklatın **SAML2 Update1?**:
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "çoklu oturum açmayı yapılandırın")

16. Merhaba SAML2 Update1 Özellikler iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:
    
     ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "çoklu oturum açmayı yapılandırın")

    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **SAML 2.0**).

    b. Merhaba, **kullanıcı alanı** metin kutusuna, türü **e-posta** veya **user_name**, toouniquely tanımlamak ServiceNow dağıtımınızda bulunan kullanıcılar hangi alan bağlı olarak kullanılır. 

    > [!NOTE] 
    > Azure AD configue tooemit ya da hello Azure AD kullanıcı kimliği (kullanıcı asıl adı) olabilir ya da hello SAML belirteci benzersiz tanımlayıcı tarafından giderek toohello hello gibi e-posta adresi hello **ServiceNow > öznitelikler > çoklu oturum açma** bölümü Klasik Azure portalı ve eşleme istenen hello alan toohello hello **NameIdentifier** özniteliği. Hello seçili öznitelik için Azure AD (örneğin kullanıcı asıl adı) depolanan hello değeri girilen hello alan (örneğin user_name) ServiceNow içinde depolanan hello değeriyle eşleşmelidir

    c. Hello Azure AD Klasik portalında hello kopyalama **kimlik sağlayıcı kimliği** değer ve hello yapıştırma **kimlik sağlayıcısı URL'si** metin kutusu.

    d. Hello Azure AD Klasik portalında hello kopyalama **kimlik doğrulaması istek URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının AuthnRequest** metin kutusu.

    e. Hello Azure AD Klasik portalında hello kopyalama **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının SingleLogoutRequest** metin kutusu.

    f. Merhaba, **ServiceNow giriş sayfası** metin kutusuna, ServiceNow örneği giriş sayfanız türü hello URL'si.

    > [!NOTE] 
    > Merhaba ServiceNow örneği giriş sayfası olan bir birleşimini, **ServieNow Kiracı URL** ve **/navpage.do** (örn:`https://fabrikam.service-now.com/navpage.do`).

    g. Merhaba, **varlık kimliği / veren** metin kutusuna, ServiceNow kiracınızın türü hello URL.

    h. Merhaba, **İzleyici URL** metin kutusuna, ServiceNow kiracınızın türü hello URL. 

    ı. Merhaba, **Protokolü bağlama hello IDP'ın SingleLogoutRequest için** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:bindings:HTTP-yeniden yönlendirme**.

    j. Hello NameID İlkesi metin kutusuna, yazın **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: belirtilmeyen**.

    k. Seçimini **bir AuthnContextClass oluşturma**.

    l. Merhaba, **AuthnContextClassRef yöntemi**, türü `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Bu, yalnızca bulut yalnızca kuruluş ise gereklidir. Kullanıyorsanız, ADFS veya MFA kimlik doğrulaması için bu değeri yapılandırmamalısınız sonra şirket içi. 

    m. İçinde **saat eğriltme** metin kutusuna, türü **60**.

    n. Olarak **üzerinde tek oturum betiği**seçin **MultiSSO_SAML2_Update1**.

    o. Olarak **x509 sertifika**seçin hello önceki adımda oluşturduğunuz hello sertifika.

    p. Tıklatın **gönderme**. 

1. Hello Azure AD Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**. 
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "çoklu oturum açmayı yapılandırın")

2. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "çoklu oturum açmayı yapılandırın")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Azure AD çoklu oturum açma ServiceNow Express için yapılandırma
1. Hello Azure AD Klasik portalında, hello **ServiceNow** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim .
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")

2. Merhaba üzerinde **nasıl tooServiceNow üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749324.png "çoklu oturum açmayı yapılandırın")

3. Merhaba üzerinde **uygulama ayarlarını yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC769497.png "uygulama URL'sini yapılandırın")
   
    a. Merhaba, **üzerinde ServiceNow oturum URL'si** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan: `https://<instance-name>.service-now.com`.
   
    b. Merhaba, **veren URL'si** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan `https://<instance-name>.service-now.com`.
   
    c. **İleri**’ye tıklayın

4. Tıklatın **el ile Merhaba uygulaması çoklu oturum açma için yapılandırma**, ardından **sonraki** tam hello adımları izleyerek.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "uygulama URL'sini yapılandırın")

5. Merhaba üzerinde **Servicenow'da çoklu oturum açma yapılandırma** sayfasında, **indirme sertifika**, yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749325.png "çoklu oturum açmayı yapılandırın")

6. Oturum açma ServiceNow Express uygulama yönetici olarak tooyour.

7. Merhaba Gezinti hello sol taraftaki bölmede **çoklu oturum açma**.  
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "uygulama URL'sini yapılandırın")

8. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, hello üst sağ ve ayarlanmış hello özellikler aşağıdaki hello yapılandırma simgesine tıklayın:
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "uygulama URL'sini yapılandırın")
   
    a. İki durumlu **birden çok sağlayıcı SSO etkinleştirme** toohello sağ.
   
    b. İki durumlu **etkinleştir hata ayıklama hello için birden çok sağlayıcı SSO tümleştirme günlüğü** toohello sağ.
   
    c. İçinde **hello alan hello kullanıcı tablo...**  metin kutusuna, türü **user_name**.
9. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, tıklatın **yeni sertifika Ekle**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "çoklu oturum açmayı yapılandırın")
10. Merhaba üzerinde **X.509 sertifikalarını** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "çoklu oturum açmayı yapılandırın")
    
    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **TestSAML2.0**).
    
    b. Seçin **etkin**.
    
    c. Olarak **biçimi**seçin **PEM**.
    
    d. Olarak **türü**seçin **deposu sertifika güven**.
    
    e. Bir Base64 ile kodlanmış dosyası indirilen sertifikanızı oluşturun.
    
    > [!NOTE]
    > Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Base64 ile kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **PEM sertifika** metin kutusu.
    
    g. Tıklatın **güncelleştirme**.
11. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, tıklatın **ekleme yeni IDP**.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "çoklu oturum açmayı yapılandırın")
12. Merhaba üzerinde **yeni kimlik sağlayıcı Ekle** iletişim altında **yapılandırma kimlik sağlayıcısı**, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "çoklu oturum açmayı yapılandırın")

    a. Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **SAML 2.0**).

    b. Hello Azure AD Klasik portalında hello kopyalama **kimlik sağlayıcı kimliği** değer ve hello yapıştırma **kimlik sağlayıcısı URL'si** metin kutusu.

    c. Hello Azure AD Klasik portalında hello kopyalama **kimlik doğrulaması istek URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının AuthnRequest** metin kutusu.

    d. Hello Azure AD Klasik portalında hello kopyalama **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının SingleLogoutRequest** metin kutusu.

    e. Olarak **kimlik sağlayıcısı sertifikası**seçin hello önceki adımda oluşturduğunuz hello sertifika.


1. Tıklatın **Gelişmiş ayarları**ve altında **ek kimlik sağlayıcısı özellikleri**, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "çoklu oturum açmayı yapılandırın")
   
    a. Merhaba, **Protokolü bağlama hello IDP'ın SingleLogoutRequest için** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:bindings:HTTP-yeniden yönlendirme**.
   
    b. Merhaba, **NameID İlkesi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: belirtilmeyen**.    
   
    c. Merhaba, **AuthnContextClassRef yöntemi**, türü **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Seçimini **bir AuthnContextClass oluşturma**.

2. Altında **ek hizmet sağlayıcısı özellikleri**, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "çoklu oturum açmayı yapılandırın")
   
    a. Merhaba, **ServiceNow giriş sayfası** metin kutusuna, ServiceNow örneği giriş sayfanız türü hello URL'si.
   
    > [!NOTE]
    > Merhaba ServiceNow örneği giriş sayfası olan bir birleşimini, **ServieNow Kiracı URL** ve **/navpage.do** (örn: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. Merhaba, **varlık kimliği / veren** metin kutusuna, ServiceNow kiracınızın türü hello URL.
   
    c. Merhaba, **İzleyici URI'si** metin kutusuna, ServiceNow kiracınızın türü hello URL. 
   
    d. İçinde **saat eğriltme** metin kutusuna, türü **60**.
   
    e. Merhaba, **kullanıcı alanı** metin kutusuna, türü **e-posta** veya **user_name**, toouniquely tanımlamak ServiceNow dağıtımınızda bulunan kullanıcılar hangi alan bağlı olarak kullanılır.
   
    > [!NOTE]
    > Azure AD configue tooemit ya da hello Azure AD kullanıcı kimliği (kullanıcı asıl adı) olabilir ya da hello SAML belirteci benzersiz tanımlayıcı tarafından giderek toohello hello gibi e-posta adresi hello **ServiceNow > öznitelikler > çoklu oturum açma** bölümü Klasik Azure portalı ve eşleme istenen hello alan toohello hello **NameIdentifier** özniteliği. Hello seçili öznitelik için Azure AD (örneğin kullanıcı asıl adı) depolanan hello değeri girilen hello alan (örneğin user_name) ServiceNow içinde depolanan hello değeriyle eşleşmelidir
    > 
    > 
   
    f. **Kaydet** düğmesine tıklayın. 

3. Hello Azure AD Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**. 
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "çoklu oturum açmayı yapılandırın")

4. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "çoklu oturum açmayı yapılandırın")

## <a name="configuring-user-provisioning"></a>Kullanıcı hazırlama işleminin yapılandırılması
Bu bölümde Hello amacı olan toooutline tooServiceNow tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:
1. Hello Azure Yönetim Portalı'nda Klasik, hello üzerinde **ServiceNow** uygulama tümleştirme sayfasını tıklatın **kullanıcı sağlamayı Yapılandır**. 
   
    ![Kullanıcı sağlamayı](./media/active-directory-saas-servicenow-tutorial/IC769498.png "kullanıcı hazırlama")

2. Merhaba üzerinde **, ServiceNow kimlik bilgileri tooenable otomatik kullanıcı sağlamayı girin** sayfasında, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
     a. Merhaba, **ServiceNow örneği adı** metin kutusuna, tür hello ServiceNow örneğinin adı.
   
     b. Merhaba, **ServiceNow yönetici kullanıcı adı** metin kutusuna, tür hello hello ServiceNow yönetici hesabı adını.
   
     c. Merhaba, **ServiceNow yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.
   
     d. Tıklatın **doğrulamak** tooverify yapılandırmanızı.
   
     e. Merhaba tıklatın **sonraki** düğmesini tooopen hello **sonraki adımlar** sayfası.
   
     f. Tüm kullanıcıların toothis uygulama tooprovision istiyorsanız seçin "**otomatik olarak hello dizin toothis uygulamadaki tüm kullanıcı hesapları sağlama**". 
   
    ![Sonraki adımlar](./media/active-directory-saas-servicenow-tutorial/IC698804.png "sonraki adımlar")
   
     g. Merhaba üzerinde **sonraki adımlar** sayfasında, **tam** toosave yapılandırmanızı.

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde, bir test kullanıcısı Britta Simon adlı hello Klasik portalda oluşturun.

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
   
    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
   
    c. **İleri**’ye tıklayın.

6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. Merhaba, **ad** metin kutusuna, türü **Britta**.  
   
   b. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.
   
   c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
   
   d. Merhaba, **rol** listesinde **kullanıcı**.
   
   e. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Merhaba Hello değerini yazmak **yeni parola**.
   
    b. **Tamamla**’ya tıklayın.   

### <a name="creating-a-servicenow-test-user"></a>ServiceNow test kullanıcısı oluşturma
Bu bölümde, ServiceNow içinde Britta Simon adlı bir kullanıcı oluşturun. Bu bölümde, ServiceNow içinde Britta Simon adlı bir kullanıcı oluşturun. Nasıl tooadd ServiceNow veya ServiceNow hızlı bir kullanıcı hesabı bilmiyorsanız, ServiceNow Destek ekibine başvurun.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama
Bu bölümde, kendi erişim tooServiceNow vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooServiceNow hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ServiceNow**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Kullanıcı atama][203] 

4. Merhaba tüm kullanıcılar listesinden seçin **Britta Simon**.

5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Kullanıcı atama][205]

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba ServiceNow hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ServiceNow uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
