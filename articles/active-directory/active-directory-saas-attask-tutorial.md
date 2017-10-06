---
title: "Öğretici: Azure Active Directory Tümleştirme ile @Task| Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasında ve @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Öğretici: Azure Active Directory ile tümleştirme@Task
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate @Task Azure Active Directory'ye (Azure AD).  
Tümleştirme @Task ile Azure AD ile Merhaba aşağıdaki avantajları sağlar: 

* Erişimi olan Azure AD'de kontrol edebilirsiniztoo@Task
* Tooautomatically alma oturum açma, kullanıcılarınızın etkinleştirebilirsiniz too@Task (çoklu oturum açma) Azure AD hesaplarına sahip
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure Azure AD ile tümleştirme @Task, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* Bir @Task çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.
> 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.  
Bu öğreticide gösterilen hello senaryo üç ana yapı taşlarını oluşur:

1. Ekleme @Task hello Galeriden 
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-task-from-hello-gallery"></a>Ekleme @Task hello Galeriden
tooconfigure hello tümleştirilmesi @Task tooadd gereken Azure AD ile @Task hello galeri tooyour listesinden yönetilen SaaS uygulamaları.

**tooadd @Task hello Galerisi'nden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1] 
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2] 
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3] 
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4] 
6. Merhaba arama kutusuna yazın  **@Task** .
   
    ![Uygulamalar][5] 
7. Merhaba sonuçlar bölmesinde seçin  **@Task** ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Uygulamalar][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Merhaba, bu bölümün amacı olan, nasıl tooconfigure ve test Azure AD çoklu oturum açma ile tooshow @Task "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma Azure AD tooknow hangi hello karşılık gelen kullanıcı gereken @Task Azure AD'de tooan kullanıcıdır. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı arasında bir bağlantı ilişki @Task kurulan toobe gerekiyor.   
Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** içinde @Task.

tooconfigure ve test Azure AD çoklu oturum açma ile @Task, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Oluşturma bir @Tasktest kullanıcı](#creating-a-halogen-software-test-user)**  -toohave Britta Simon, karşılık gelen bir @Taskthat her bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma
Bu bölümde Hello amacı olduğundan tooenable Azure AD çoklu oturum açma hello Klasik Azure Portalı'nda ve tooconfigure çoklu oturum açma içinde @Task uygulama.

**Azure AD çoklu oturum açma tooconfigure ile @Task, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure Portalı'nda  **@Task**  uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. Merhaba üzerinde **nasıl gibi kullanıcıların toosign üzerinde yaptığınız too@Task**  sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][7] 
3. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama ayarlarını yapılandırın][8] 
   
     a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, toosign üzerinde kullanıcıların tooyour tarafından kullanılan türü hello URL @Task uygulama (örn:*https://<Tenant name>.attask ondemand.com*).
   
     b. **İleri**’ye tıklayın.
4. Merhaba üzerinde **çoklu oturum açma sırasında yapılandırma @Task**  sayfasında, **karşıdan meta veri**hello meta veri dosyası, bilgisayarınıza yerel olarak kaydedin ve ardından **sonraki**.
   
    ![Azure AD Connect nedir?][9] 
5. Oturum açma tooyour @Task yönetici olarak şirket site.
6. Çok Git**tek oturum açma yapılandırma**.
7. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, aşağıdaki adımları hello gerçekleştirmek
   
    ![Çoklu oturum açmayı yapılandırın][23]
   
    a. Olarak **türü**seçin **SAML 2.0**.
   
    b. Seçin **hizmet sağlayıcı kimliği**.
   
    c. Merhaba Hello Klasik Azure portalı, kopyalama **uzaktan oturum açma URL'si**ve hello yapıştırma **oturum açma portalı URL'si** metin kutusu.
   
    d. Merhaba Hello Klasik Azure portalı, kopyalama **tek Sign-Out hizmeti URL'si**ve hello yapıştırma **Sign-Out URL** metin kutusu.
   
    e. Merhaba Hello Klasik Azure portalı, kopyalama **değişiklik parola URL'si**ve hello yapıştırma **değişiklik parola URL'si** metin kutusu.
   
    f. **Kaydet** düğmesine tıklayın.
8. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**. 
   
    ![Azure AD Connect nedir?][10]
9. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
   
    ![Azure AD Connect nedir?][11]

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.  

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
   
    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
   
    c. **İleri**’ye tıklayın.
6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. Merhaba, **ad** metin kutusuna, türü **Britta**.  
   
    b. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.
   
    c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
   
    d. Merhaba, **rol** listesinde **kullanıcı**.

    e. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Merhaba Hello değerini yazmak **yeni parola**.
   
    b. **Tamamla**’ya tıklayın.   

### <a name="creating-an-task-test-user"></a>Oluşturma bir @Task test kullanıcısı
Bu bölümde Hello amacı olan toocreate Britta Simon adlı bir kullanıcı @Task.

**toocreate Britta Simon adlı bir kullanıcı @Task, hello aşağıdaki adımları gerçekleştirin:**

1. Tooyour üzerinde oturum @Task yönetici olarak şirket site.
2. Hello içinde hello üst menüsünde **kişiler**.
3. Tıklatın **yeni bir kişiye**. 
4. Merhaba yeni bir kişiye iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:
   
    ![Oluşturma bir @Task test kullanıcısı][21] 
   
    a. Merhaba, **ad** metin kutusuna, "Britta" yazın.
   
    b. Merhaba, **Soyadı** metin kutusuna, "Simon" yazın.
   
    c. Merhaba, **e-posta adresi** metin kutusuna, Azure Active Directory'de Britta Simon'ın e-posta adresini yazın.
   
    d. Tıklatın **kişiyi ekler**.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama
Merhaba amacı, bu bölümde her erişim vererek tooenabling Azure çoklu oturum açma Britta Simon toouse olan too@Task.

![Kullanıcı atama][200] 

**tooassign Britta Simon too@Task, hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.
   
    ![Kullanıcı atama][201] 
2. Merhaba uygulamalar listesinde  **@Task** .
   
    ![Kullanıcı atama][202] 
3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Kullanıcı atama][203] 
4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.
5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Kullanıcı atama][205]

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Merhaba tıkladığınızda @Task parçasında Merhaba erişim paneli, otomatik olarak oturum açma tooyour alması gereken @Task uygulama.

## <a name="additional-resources"></a>Ek Kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






