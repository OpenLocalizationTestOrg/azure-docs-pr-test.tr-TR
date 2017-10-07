---
title: "Öğretici: Azure Active Directory Tümleştirme ile SuccessFactors | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse SuccessFactors nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Öğretici: Azure Active Directory Tümleştirme SuccessFactors ile
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate SuccessFactors Azure Active Directory'ye (Azure AD).

SuccessFactors Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

* Erişim tooSuccessFactors sahip Azure AD'de kontrol edebilirsiniz
* Kullanıcıların tooautomatically get açan tooSuccessFactors (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure SuccessFactors ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

* Geçerli bir Azure aboneliği
* Bir kiracı SuccessFactors içinde

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.
> 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden SuccessFactors ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-successfactors-from-hello-gallery"></a>Merhaba Galerisi'nden SuccessFactors ekleme
Azure AD'ye tooconfigure hello tümleştirme SuccessFactors, tooadd SuccessFactors hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SuccessFactors hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
    ![Çoklu oturum açmayı yapılandırma][1]
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Çoklu oturum açmayı yapılandırma][2]
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Çoklu oturum açmayı yapılandırma][4]
6. Merhaba, **arama kutusu**, türü **SuccessFactors**.
   
    ![Çoklu oturum açmayı yapılandırma][5]
7. Merhaba Sonuçlar panelinde seçin **SuccessFactors**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Çoklu oturum açmayı yapılandırma][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Azure AD çoklu oturum açmayı test SuccessFactors ile temel alarak "Britta Simon" adlı bir test kullanıcı.

Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı SuccessFactors tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SuccessFactors hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** SuccessFactors içinde.

tooconfigure ve SuccessFactors ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SuccessFactors test kullanıcısı oluşturma](#creating-a-successfactors-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir SuccessFactors içinde Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma
Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma SuccessFactors uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile SuccessFactors, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **SuccessFactors** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.
   
    ![Çoklu oturum açmayı yapılandırma][7]
2. Merhaba üzerinde **nasıl tooSuccessFactors üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açmayı yapılandırma][8]
3. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**.
   
    ![Çoklu oturum açmayı yapılandırma][9]
   
    a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, URL desenlerini aşağıdaki hello birini kullanarak bir yazın: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. Merhaba, **yanıt URL'si** metin kutusuna, URL desenlerini aşağıdaki hello birini kullanarak bir yazın: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. **İleri**’ye tıklayın. 

    > [!NOTE]
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello gerçek oturum üzerinde URL'si ve yanıt URL'si ile bu değerlere sahip. Bu değerleri tooget başvurun [SuccessFactors destek ekibi](https://www.successfactors.com/en_us/support.html).

1. Merhaba üzerinde **çoklu oturum açma sırasında SuccessFactors yapılandırma** sayfasında, **indirme sertifika**ve yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin.
   
    ![Çoklu oturum açmayı yapılandırma][10]

2. Farklı web tarayıcısı penceresinde oturum açın, **SuccessFactors Yönetici portalı** yönetici olarak.

3. Ziyaret **uygulama güvenliği** ve yerel çok**tek oturum açma özelliğini**. 

4. Herhangi bir değer hello yerleştirin **sıfırlama belirteci** tıklatıp **Kaydet belirteci** tooenable SAML SSO.
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma][11]

    > [!NOTE] 
    > Bu değer yalnızca başlangıç anahtarı açık/kapalı olarak kullanılır. Herhangi bir değer kaydettiyseniz hello SAML SSO açık'tır. Boş bir değer kaydettiyseniz hello SAML SSO Kapalı'dır.

1. Yerel toobelow ekran ve hello aşağıdaki eylemleri gerçekleştirin.
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma][12]
   
    a. Select hello **SAML v2 SSO** radyo düğmesi
   
    b. Merhaba SAML sunduğundan taraf Name(e.g. SAml issuer + company name) ayarlayın.
   
    c. Merhaba, **SAML veren** textbox put hello değerini **veren URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.
   
    d. Seçin **yanıt (müşteri oluşturulan/IDP/AP)** olarak **zorunlu imza gerektir**.
   
    e. Seçin **etkin** olarak **etkinleştirmek SAML bayrağı**.
   
    f. Seçin **Hayır** olarak **oturum açma isteği imza (BT oluşturulan/SP/RP)**.
   
    g. Seçin **tarayıcı/Post profili** olarak **SAML profili**.
   
    h. Seçin **Hayır** olarak **sertifika geçerli süresi zorunlu**.
   
    ı. Merhaba hello indirilen sertifika dosyasının içeriğini kopyalayın ve hello yapıştırma **SAML doğrulama sertifikası** metin kutusu.

    > [!NOTE] 
    > Merhaba sertifika içeriğini sahip başlamalıdır sertifika ve bitiş sertifika etiketler.

1. TooSAML V2 gidin ve ardından hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma][13]
   
    a. Seçin **Evet** olarak **destek SP tarafından başlatılan genel oturum kapatma**.
   
    b. Merhaba, **genel oturum kapatma hizmeti URL'si (LogoutRequest hedef)** textbox put hello değerini **uzak oturum kapatma URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.
   
    c. Seçin **Hayır** olarak **sp tüm NameID öğesi şifrelemek gerekir gerektiren**.
   
    d. Seçin **belirtilmeyen** olarak **NameID biçimi**.
   
    e. Seçin **Evet** olarak **etkinleştir sp tarafından başlatılan oturum açma (AuthnRequest)**.
   
    f. Merhaba, **şirket çapında veren olarak gönderme isteği** textbox put hello değerini **uzaktan oturum açma URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.
2. Toomake hello oturum açma kullanıcı adları istiyorsanız aşağıdaki adımları gerçekleştirin büyük küçük harf duyarsız.
   
    a. Ziyaret **şirket ayarları**(yakın hello alt).
   
    b. yakın onay kutusunu seçin **etkinleştirmek olmayan durumda duyarlı kullanıcıadı**.
   
    c.Click **kaydetmek**.
   
    ![Çoklu oturum açmayı yapılandırın][29]

    > [!NOTE] 
    > Bu tooenable çalışırsanız, yinelenen bir SAML oturum açma adı oluşturur, hello sistem denetler. Kullanıcı adları Kullanıcı1 hem Kullanıcı1 Hello müşteri varsa, örneğin. Büyük küçük harfe duyarlılığın hemen alma bu yinelemeleri yapar. Merhaba sistem bir hata iletisi alır ve hello özelliği izin vermez. gerçekte yazılmış şekilde hello müşteri toochange hello kullanıcı adları birini farklı gerekir. 

1. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
    ![Uygulamalar][14]
2. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.
   
    ![Uygulamalar][15]

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate bir test kullanıcısı Britta Simon adlı hello Klasik Portalı'nda ' dir.

![Azure AD Kullanıcı oluşturma][16]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma][17]
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma][18]
4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.
   
    ![Bir Azure AD test kullanıcısı oluşturma][19]
5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma][20]
   
    a. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
   
    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
   
    c. **İleri**’ye tıklayın.
6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma][21]
   
    a. Merhaba, **ad** metin kutusuna, türü **Britta**.  
   
    b. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.
   
    c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
   
    d. Merhaba, **rol** listesinde **kullanıcı**.
   
    e. **İleri**’ye tıklayın.
7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma][22]
8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma][23]
   
    a. Merhaba Hello değerini yazmak **yeni parola**.
   
    b. **Tamamla**’ya tıklayın.  

### <a name="creating-a-successfactors-test-user"></a>SuccessFactors test kullanıcısı oluşturma
SuccessFactors içine sipariş tooenable Azure AD kullanıcıların toolog bunların SuccessFactors sağlanmalıdır.  
SuccessFactors Hello durumda sağlama bir el ile bir görevdir.

SuccessFactors içinde oluşturulan tooget kullanıcıların toocontact hello ihtiyacınız [SuccessFactors destek ekibi](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama
Bu bölümde Hello amacı kendi erişim tooSuccessFactors vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.

![Kullanıcı atama][24]

**tooassign Britta Simon tooSuccessFactors hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Kullanıcı atama][25]
2. Merhaba uygulamalar listesinde **SuccessFactors**.
   
    ![Çoklu oturum açmayı yapılandırın][26]
3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Kullanıcı atama][27]
4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.
5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Kullanıcı atama][28]

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Hello erişim paneli SuccessFactors döşeme hello tıkladığınızda, otomatik olarak oturum açma SuccessFactors uygulama tooyour almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
