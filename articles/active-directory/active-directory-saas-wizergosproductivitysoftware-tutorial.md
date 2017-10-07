---
title: "Öğretici: Azure Active Directory Tümleştirme Wizergos üretkenlik ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Wizergos üretkenlik arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Öğretici: Azure Active Directory Tümleştirme ile Wizergos üretkenlik
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Wizergos üretkenlik Azure Active Directory'ye (Azure AD).

Wizergos üretkenlik Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

* Erişim tooWizergos üretkenlik sahip Azure AD'de kontrol edebilirsiniz
* Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooWizergos üretkenlik çoklu oturum açma (SSO) etkinleştir
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure Wizergos üretkenlik ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* Abonelik Wizergos üretkenlik yazılım SSO etkin

>[!NOTE]
>tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz. 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD SSO bir sınama ortamında.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Wizergos üretkenlik ekleme
2. Yapılandırma ve Azure AD SSO test etme

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Merhaba Galerisi'nden Wizergos üretkenlik ekleme
Azure AD'ye tooconfigure hello tümleştirme Wizergos üretkenlik yazılımın tooadd Wizergos üretkenlik hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Wizergos üretkenlik hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1]
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2]
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]
6. Merhaba arama kutusuna yazın **Wizergos üretkenlik**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. Merhaba Sonuçlar panelinde seçin **Wizergos üretkenlik**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Merhaba Galerisi'nde Hello uygulama seçme](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Yapılandırma ve Azure AD SSO test etme
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve test Wizergos üretkenlik ile Azure AD SSO temel alarak "Britta Simon" adlı bir test kullanıcı.

SSO toowork için Azure AD hangi hello karşılık gelen kullanıcı Wizergos üretkenlik tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Wizergos üretkenlik hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** Wizergos üretkenlik yazılım.

tooconfigure ve BynWizergos üretkenlik Softwareder ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Wizergos üretkenlik test kullanıcısı oluşturma](#creating-a-wizergos-productivity-software-test-user)**  -toohave karşılık gelen, Britta Simon Wizergos üretkenlik yazılımında, her bağlı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-sso"></a>Azure AD SSO yapılandırma
Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma Wizergos üretkenlik uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Wizergos üretkenlik ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Klasik Portalı'nda **Wizergos üretkenlik** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**iletişim.
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. Merhaba üzerinde **nasıl tooWizergos üretkenlik üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, tıklatın **sonraki**:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. Merhaba üzerinde **çoklu oturum açma sırasında Wizergos üretkenlik yapılandırma** sayfasında, **indirme sertifika**ve ardından hello dosyayı bilgisayarınıza kaydedin:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour Wizergos üretkenlik Kiracı.
6. Merhaba hamburger menüsünden seçin **yönetici**.
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. Sol taraftaki menüsünde Yönetim sayfasında seçin **kimlik doğrulaması** ve tıklayın **Azure AD**.
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Aşağıdaki adımları hello gerçekleştirmek **kimlik doğrulaması** bölümü.
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Tıklatın **karşıya** düğmesini tooupload hello Azure AD'den sertifika indirilir. 
  2. Merhaba, **veren URL'si** textbox put hello değerini **veren URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.
  3. Merhaba, **çoklu oturum açma URL'si** textbox put hello değerini **çoklu oturum açma hizmet URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.
  4. Merhaba, **tek Sign-Out URL** textbox put hello değerini **tek Sign-out hizmeti URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.
  5. Tıklatın **kaydetmek** düğmesi.
9. Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][10]
10. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
    
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate bir test kullanıcısı Britta Simon adlı hello Klasik Portalı'nda ' dir.

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
  2. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
  3. **İleri**’ye tıklayın.
6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. Merhaba, **ad** metin kutusuna, türü **Britta**.  
  2. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.
  3. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
  4. Merhaba, **rol** listesinde **kullanıcı**.
  5. **İleri**’ye tıklayın.
7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Merhaba Hello değerini yazmak **yeni parola**.
  2. **Tamamla**’ya tıklayın.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Wizergos üretkenlik test kullanıcısı oluşturma
Bu bölümde, Britta Simon Wizergos üretkenlik adlı bir kullanıcı oluşturun. Lütfen Wizergos üretkenlik destek ekibi ile çalışmak [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello kullanıcılar hello Wizergos üretkenlik Platform.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın
Bu bölümde Hello amacı kendi erişim tooWizergos üretkenlik vererek tooenabling Britta Simon toouse Azure SSO olur.

  ![Kullanıcı atama][200]

**tooassign Britta Simon tooWizergos üretkenlik, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Kullanıcı atama][201]
2. Merhaba uygulamalar listesinde **Wizergos üretkenlik**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Kullanıcı atama][203]
4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.
5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba Wizergos üretkenlik hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Wizergos üretkenlik uygulaması almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
