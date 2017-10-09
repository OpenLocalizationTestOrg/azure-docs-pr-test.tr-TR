---
title: "Öğretici: Azure Active Directory Tümleştirme ile Halosys | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Halosys nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Öğretici: Azure Active Directory Tümleştirme Halosys ile

Bu öğreticide, bilgi nasıl toointegrate Halosys Azure Active Directory'ye (Azure AD).

Halosys Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooHalosys sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooHalosys (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Halosys ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Halosys çoklu oturum açma etkin abonelik


> [!NOTE] 
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Halosys ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-halosys-from-hello-gallery"></a>Merhaba Galerisi'nden Halosys ekleme
Azure AD'ye tooconfigure hello tümleştirme Halosys, tooadd Halosys hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Halosys hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.

    ![Active Directory][1]
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.

    ![Uygulamalar][2]

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.

    ![Uygulamalar][3]

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.

    ![Uygulamalar][4]

6. Merhaba arama kutusuna yazın **Halosys**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Merhaba sonuçlar bölmesinde seçin **Halosys**ve ardından **tam** tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Halosys sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Halosys içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Halosys hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Halosys içinde.

tooconfigure ve Halosys ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Halosys test kullanıcısı oluşturma](#creating-a-halosys-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Halosys içinde Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma Halosys uygulamanızda yapılandırın.


**tooconfigure Azure AD çoklu oturum açma ile Halosys, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Klasik Portalı'nda **Halosys** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma** iletişim.
     
    ![Çoklu oturum açmayı yapılandırın][6] 

2. Merhaba üzerinde **nasıl tooHalosys üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, desen aşağıdaki hello kullanarak, kullanıcılar toosign üzerinde tooyour Halosys uygulamanız tarafından kullanılan türü hello URL: `https://<company-name>.Halosys.com/client-api/api`.

    b.In hello **tanımlayıcı URL'si** metin kutusuna, türü hello hello desen aşağıdaki URL'de: `https://<company-name>.Halosys.com`. 
         
4. Merhaba üzerinde **çoklu oturum açma sırasında Halosys yapılandırma** sayfasında, **karşıdan meta veri**ve hello dosyayı bilgisayarınıza kaydedin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget uygulamanız için yapılandırılmış SSO Halosys Destek ekibine başvurun ve ile Merhaba aşağıdakileri sağlar:

    • hello indirilen **meta veri dosyası**
    
    • hello **SAML SSO URL'si**
    

6. Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.
    
    ![Azure AD çoklu oturum açma][10]

7. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
 
    ![Azure AD çoklu oturum açma][11]


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde, bir test kullanıcısı Britta Simon adlı hello Klasik portalda oluşturun.


![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: ![bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.

    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.

    c. **İleri**’ye tıklayın.

6.  Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: ![bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. Merhaba, **ad** metin kutusuna, türü **Britta**.  

    b. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.

    c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.

    d. Merhaba, **rol** listesinde **kullanıcı**.

    e. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Merhaba Hello değerini yazmak **yeni parola**.

    b. **Tamamla**’ya tıklayın.   



### <a name="creating-a-halosys-test-user"></a>Halosys test kullanıcısı oluşturma

Bu bölümde, Halosys içinde Britta Simon adlı bir kullanıcı oluşturun. Lütfen destek ekibi tooadd hello kullanıcılar hello Halosys Platform Halosys ile çalışır.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooHalosys vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooHalosys hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Halosys**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. Hello içinde hello üst menüsünde **kullanıcılar**.

    ![Kullanıcı atama][203]

4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.

5. Merhaba altta Hello araç çubuğunda **atamak**.

    ![Kullanıcı atama][205]


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Hello erişim paneli Halosys döşeme hello tıkladığınızda, otomatik olarak oturum açma Halosys uygulama tooyour almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
