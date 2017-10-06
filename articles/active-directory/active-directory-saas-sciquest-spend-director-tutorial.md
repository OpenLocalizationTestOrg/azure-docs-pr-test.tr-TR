---
title: "Öğretici: Azure Active Directory Tümleştirme SciQuest harcamanız Director ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SciQuest harcamanız Director arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Öğretici: Azure Active Directory Tümleştirme SciQuest harcamanız Director ile
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate SciQuest harcamanız Director Azure Active Directory'ye (Azure AD).  
SciQuest harcadığı Director Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar: 

* Erişim tooSciQuest harcama Director sahip Azure AD'de kontrol edebilirsiniz 
* Kullanıcıların tooautomatically get açan tooSciQuest (çoklu oturum açma) harcama Director Azure AD hesaplarına ile etkinleştirebilirsiniz
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure SciQuest harcamanız Director ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* Bir SciQuest harcamanız Director çoklu oturum açma etkin abonelik

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

1. Merhaba Galerisi'nden SciQuest harcamanız Director ekleme 
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Merhaba Galerisi'nden SciQuest harcamanız Director ekleme
Azure AD'ye tooconfigure hello tümleştirme SciQuest harcamanız Director, tooadd SciQuest harcamanız Director hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SciQuest harcamanız Director hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1]

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2]

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]

6. Merhaba arama kutusuna yazın **sciQuest harcamanız director**.
   
    ![Uygulamalar][5]

7. Merhaba sonuçlar bölmesinde seçin **SciQuest harcamanız Director**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Uygulamalar][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Azure AD çoklu oturum açmayı test SciQuest harcamanız Director ile temel alarak "Britta Simon" adlı bir test kullanıcı.

Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı SciQuest harcamanız Director tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve SciQuest harcamanız Director hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.  
Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SciQuest harcamanız Director.

tooconfigure ve SciQuest harcamanız Director ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD tek tek oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SciQuest harcadığı Director test kullanıcısı oluşturma](#creating-a-halogen-software-test-user)**  -toohave karşılık gelen, Britta Simon SciQuest harcamanız Director her bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Azure AD çoklu çoklu oturum açma yapılandırma
Bu bölümde Hello amacı tooenable Azure AD çoklu oturum açma hello Klasik Azure Portalı'nda ve tooconfigure çoklu oturum açma SciQuest harcamanız Director uygulamanızda ' dir.

**Azure AD çoklu oturum açma tooconfigure harcamanız SciQuest Director ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Klasik Azure portalı içinde **SciQuest harcamanız Director** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**iletişim.
   
    ![Çoklu oturum açmayı yapılandırın][8]

2. Merhaba üzerinde **nasıl tooSciQuest harcama Director üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][9]

3. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulama ayarlarını yapılandırın][10]
   
     a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü URL'niz, kullanıcıların toosign desen aşağıdaki hello kullanarak tooyour SciQuest harcamanız Director uygulama tarafından kullanılan: *https://.* SciQuest.com/.**
   
     b. Merhaba, **yanıt URL'si** metin kutusuna, türü hello aynı değeri, hello yazmış **oturum üzerinde URL'si** metin kutusu. 
   
     c. **İleri**’ye tıklayın.

4. Merhaba üzerinde **çoklu oturum açma SciQuest harcamanız Director yapılandırma** sayfasında, **karşıdan meta veri**ve hello meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.
   
    ![Azure AD Connect nedir?][11]

5. SciQuest destek tooenable hello yukarıdaki indirilen meta verileri kullanarak bu kimlik doğrulama yöntemini başvurun.

6. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim. 
   
    ![Azure AD Connect nedir?][15]

7. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Azure AD Connect nedir?][100] 

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Azure AD Connect nedir?][101] 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**. 
   
    ![Azure AD Connect nedir?][102] 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Azure AD Connect nedir?][103] 
   
    a. Olarak **kullanıcı türü**seçin **kuruluşunuzdaki yeni kullanıcı**.
   
    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
   
    c. **İleri**’ye tıklayın.

6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Azure AD Connect nedir?][104] 
   
    a. Merhaba, **ad** metin kutusuna, türü **Britta**.  
   
    b. Merhaba, **Soyadı** txtbox, türü, **Simon**.
   
    c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
   
    d. Merhaba, **rol** listesinde **kullanıcı**.
   
    e. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Azure AD Connect nedir?][105]  

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Azure AD Connect nedir?][106]   
   
    a. Merhaba Hello değerini yazmak **yeni parola**.
   
    b. **Tamamla**’ya tıklayın.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>SciQuest harcadığı Director test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon SciQuest harcamanız Director uygulamasında adlı bir kullanıcı var.

Oluşturulan, test hesap tooget hakkında hello ayrıntılarla sağlayacağını ve toocontact SciQuest harcamanız Director destek ekibinize gerekir.

Alternatif olarak, yalnızca zaman da kullanabilirsiniz sağlama, SciQuest harcamanız Director tarafından desteklenen tek bir oturum açma özelliği.  
Yalnızca zaman sağlama etkinse, yoksa kullanıcılar otomatik olarak SciQuest harcamanız Director tarafından bir tek oturum açma girişimi sırasında oluşturulur. Bu özellik hello ihtiyacını ortadan kaldıran toomanually tek oturum açma karşılık gelen kullanıcılar oluşturun.

yalnızca zaman tooget sağlama etkin, SciQuest harcamanız Director destek ekibinize olduğunuz toocontact gerekir.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama
Bu bölümde Hello amacı kendi erişim tooSciQuest harcama Director vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.

![Azure AD Connect nedir?][200]

**tooassign Britta Simon tooSciQuest harcama Director hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.
   
    ![Azure AD Connect nedir?][201]

2. Merhaba uygulamalar listesinde **SciQuest harcamanız Director**.
   
    ![Azure AD Connect nedir?][202]

3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Azure AD Connect nedir?][203]

4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.
   
    ![Azure AD Connect nedir?][204]

5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Azure AD Connect nedir?][205]

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Merhaba SciQuest harcamanız Director hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SciQuest harcamanız Director uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek Kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

