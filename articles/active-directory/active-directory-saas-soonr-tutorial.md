---
title: "Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Soonr çalışma arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma

Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Soonr çalışma Azure Active Directory'ye (Azure AD).  
Soonr çalışma alanına Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSoonr çalışma alanına sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSoonr çalışma (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Soonr çalışma alanı ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Soonr çalışma alanı çoklu oturum açma etkin abonelik


> [!NOTE] 
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.  
Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Soonr çalışma alanına ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Merhaba Galerisi'nden Soonr çalışma alanına ekleme
Azure AD'ye tooconfigure hello tümleştirme Soonr çalışma alanı tooadd Soonr çalışma alanına hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Soonr çalışma hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 

    ![Active Directory][1]

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.

    ![Uygulamalar][2]

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.

    ![Uygulamalar][3]

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
 
    ![Uygulamalar][4]

6. Merhaba arama kutusuna yazın **Soonr çalışma alanına**.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Merhaba sonuçlar bölmesinde seçin **Soonr çalışma alanına**ve ardından **tam** tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Azure AD çoklu oturum açmayı test Soonr çalışma alanı ile temel alarak "Britta Simon" adlı bir test kullanıcı.

Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı Soonr çalışma alanına tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Soonr çalışma hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.  

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Soonr çalışma.

tooconfigure ve Soonr çalışma alanı ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Soonr çalışma alanına test kullanıcısı oluşturma](#creating-a-soonr-workplace-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Soonr çalışma Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma Soonr çalışma alanına uygulamanızda yapılandırın.


**tooconfigure Azure AD çoklu oturum açma Soonr çalışma ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Klasik Azure portalı içinde **Soonr çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.

    ![Çoklu oturum açmayı yapılandırın][6] 

2. Merhaba üzerinde **nasıl tooSoonr çalışma alanına üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. **İleri**’ye tıklayın.

    > [!NOTE] 
    > Lütfen bu hello gerçek değer olmadığını unutmayın. Bu değeri hello gerçek ile oturum URL'yi tooupdate sahip. Bu değer Soonr çalışma alanına destek ekibi tooget başvurun.

4. Merhaba üzerinde **çoklu oturum açma Soonr yerindeki yapılandırma** sayfasında, **karşıdan meta veri** ve hello dosyayı bilgisayarınıza kaydedin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget uygulamanız için yapılandırılmış SSO Soonr çalışma alanına destek ekibinize başvurun ve ile Merhaba aşağıdakileri sağlar: 

    • hello indirilen **meta veri** dosyası

    • hello **veren URL'si**

    • hello **SAML SSO URL'si**

    • hello **tek Sign-Out hizmeti URL'si**

    >[!NOTE]
    >Bu uygulamanın yerine geçen <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask çalışma alanına</a> ve başvuruda bulunabilir <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">bu</a> öğretici Azure AD ile Merhaba uygulaması yapılandırma.
   
6. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.

    ![Azure AD çoklu oturum açma][10]

7. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
  
    ![Azure AD çoklu oturum açma][11]



### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.  

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.

    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.

    c. **İleri**’ye tıklayın.

6.  Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. Merhaba, **ad** metin kutusuna, türü **Britta**.  

    b. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.

    c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.

    d. Merhaba, **rol** listesinde **kullanıcı**.

    e. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Merhaba Hello değerini yazmak **yeni parola**.

    b. **Tamamla**’ya tıklayın.   



### <a name="creating-a-soonr-workplace-test-user"></a>Soonr çalışma alanına test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon Soonr çalışma alanında adlı bir kullanıcı var. Lütfen bir kullanıcı hello Platform Soonr çalışma alanına destek ekibi toocreate ile çalışır. Merhaba destek bileti Soonr ile yükseltebilirsiniz <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">burada</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Merhaba amacı, bu bölümde, kendi çalışma alanına erişim tooSoonr vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSoonr çalışma alanı hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Soonr çalışma alanına**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. Hello içinde hello üst menüsünde **kullanıcılar**.

    ![Kullanıcı atama][203] 

1. Merhaba kullanıcılar listesinden seçin **Britta Simon**.

2. Merhaba altta Hello araç çubuğunda **atamak**.

    ![Kullanıcı atama][205]



### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Soonr çalışma alanına döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Soonr çalışma alanına uygulama tooyour almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
