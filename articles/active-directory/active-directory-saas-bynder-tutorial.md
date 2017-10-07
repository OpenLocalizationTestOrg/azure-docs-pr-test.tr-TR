---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bynder | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Bynder arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Öğretici: Azure Active Directory Tümleştirme Bynder ile
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Bynder Azure Active Directory'ye (Azure AD).

Bynder Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

* Erişim tooBynder sahip Azure AD'de kontrol edebilirsiniz
* Kullanıcıların tooautomatically get açan tooBynder çoklu oturum açma (SSO) ile Azure AD hesaplarına etkinleştirebilirsiniz
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure Bynder ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* Abonelik bir Bynder çoklu oturum açma (SSO) etkin

>[!NOTE]
>tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz. 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Microsoft Azure AD SSO bir sınama ortamında.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Bynder ekleme
2. Yapılandırma ve Microsoft Azure AD SSO test etme

## <a name="add-bynder-from-hello-gallery"></a>Merhaba Galerisi'nden Bynder ekleme
Azure AD'ye tooconfigure hello tümleştirme Bynder, tooadd Bynder hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Bynder hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1]
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2]
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]
6. Merhaba arama kutusuna yazın **Bynder**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Merhaba Sonuçlar panelinde seçin **Bynder**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Merhaba Galerisi'nde Hello uygulama seçme](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Yapılandırma ve Microsoft Azure AD SSO test etme
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve test Bynder ile Microsoft Azure AD SSO temel alarak "Britta Simon" adlı bir test kullanıcı.

SSO toowork için Azure AD hangi hello karşılık gelen kullanıcı Bynder tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Bynder hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Bynder içinde.

tooconfigure ve Microsoft Azure AD Bynder SSO'su test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Microsoft Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -Microsoft Azure AD çoklu oturum açma Britta Simon ile tootest.
3. **[Bynder test kullanıcısı oluşturma](#creating-a-bynder-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Bynder içinde Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Microsoft Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-microsoft-azure-ad-sso"></a>Microsoft Azure AD SSO yapılandırma
Bu bölümde, Microsoft Azure AD SSO hello Klasik portalında etkinleştirin ve SSO Bynder uygulamanızda yapılandırın.

**tooconfigure Bynder, Microsoft Azure AD SSO'su hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Klasik Portalı'nda **Bynder** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma** iletişim.
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. Merhaba üzerinde **nasıl tooBynder üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Merhaba üzerinde **uygulama ayarlarını yapılandır** tooconfigure hello uygulamada istiyorsanız iletişim sayfasında, **IDP başlatılan modu**, hello aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. **İleri**’ye tıklayın.
4. Tooconfigure hello uygulamada istiyorsanız **SP tarafından başlatılan modu** hello üzerinde **uygulama ayarlarını yapılandır** iletişim sayfa sonra hello tıklatıldığında **"Göster Gelişmiş ayarları (isteğe bağlı)"**ve hello enter **oturum üzerinde URL'si** tıklatıp **sonraki**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.getbynder.com/login/`
  2. **İleri**’ye tıklayın.
  
   >[!NOTE]
   >Merhaba hello oturum üzerinde URL'si Bu öğreticide yalnızca bir placeholfer değeridir. tooget hello gerçek vlaue, ortamınız için Bynder başvurun.
   >

5. Merhaba üzerinde **çoklu oturum açma sırasında Bynder yapılandırma** sayfasında hello aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Tıklatın **karşıdan meta veri**ve ardından hello dosyayı bilgisayarınıza kaydedin.
  2. **İleri**’ye tıklayın.
6. Uygulamanız için yapılandırılmış SSO tooget Bynder destek ekibinize başvurun. Hello indirilen meta veri dosyası ekleme ve bunların tarafında SSO yukarı Bynder takım tooset ile paylaşın.
7. Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][10]
8. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
   
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate bir test kullanıcısı Britta Simon adlı hello Klasik Portalı'nda ' dir.

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
  2. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
  3. **İleri**’ye tıklayın.
6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. Merhaba, **ad** metin kutusuna, türü **Britta**.  
  2. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**. 
  3. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
  4. Merhaba, **rol** listesinde **kullanıcı**.
  5. **İleri**’ye tıklayın.
7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Merhaba Hello değerini yazmak **yeni parola**.
   2. **Tamamla**’ya tıklayın.   

### <a name="create-a-bynder-test-user"></a>Bynder test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon içinde Bynder adlı bir kullanıcı ' dir. Bynder yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümde, eylem öğe yok. Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Bynder sırasında oluşturulur.

>[!NOTE]
>Bir kullanıcı toocreate el ile gerekiyorsa, toocontact hello Bynder destek ekibi gerekir. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın
Bu bölümde Hello amacı her erişim tooBynder vererek tooenabling Britta Simon toouse Azure SSO olur.

   ![Kullanıcı atama][200]

**tooassign Britta Simon tooBynder hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Kullanıcı atama][201]
2. Merhaba uygulamalar listesinde **Bynder**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Kullanıcı atama][203]
4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.
5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin
Bu bölümde Hello amacı olan tootest hello erişim paneli Microsoft Azure AD SSO kullanarak yapılandırma.

Merhaba Bynder hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Bynder uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
