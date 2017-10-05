---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bynder | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Bynder arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Öğretici: Azure Active Directory Tümleştirme Bynder ile
Bu öğreticinin amacı Bynder Azure Active Directory (Azure AD) ile tümleştirme Göster sağlamaktır.

Bynder Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

* Bynder erişimi, Azure AD'de kontrol edebilirsiniz
* Otomatik olarak Bynder çoklu oturum açma (SSO) ile Azure AD hesaplarına için açan kullanıcılarınıza etkinleştirebilirsiniz
* Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
Azure AD tümleştirme Bynder ile yapılandırmak için aşağıdaki öğeleri gerekir:

* Bir Azure AD aboneliği
* Abonelik bir Bynder çoklu oturum açma (SSO) etkin

>[!NOTE]
>Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz. 
> 

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin amacı, Microsoft Azure AD SSO bir test ortamında test etmenizi hale getirmektir.

Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden Bynder ekleme
2. Yapılandırma ve Microsoft Azure AD SSO test etme

## <a name="add-bynder-from-the-gallery"></a>Galeriden Bynder Ekle
Azure AD Bynder tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Bynder eklemeniz gerekir.

**Galeriden Bynder eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**. 
   
    ![Active Directory][1]
2. Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.
3. Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.
   
    ![Uygulamalar][2]
4. Tıklatın **Ekle** sayfanın sonundaki.
   
    ![Uygulamalar][3]
5. Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]
6. Arama kutusuna **Bynder**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Sonuçlar panelinde seçin **Bynder**ve ardından **tam** uygulama eklemek için.
   
    ![Uygulama galerisinde seçme](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Yapılandırma ve Microsoft Azure AD SSO test etme
Bu bölümün amacı, size nasıl yapılandırılacağı ve Microsoft Azure AD "Britta Simon" adlı bir test kullanıcı tabanlı Bynder SSO'su test göstermektir.

Çalışmak SSO için Azure AD Bynder Azure AD'de bir kullanıcıya karşılık gelen kullanıcı ne olduğunu bilmeniz gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının Bynder ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Bynder içinde.

Yapılandırmak ve Microsoft Azure AD Bynder SSO'su sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Microsoft Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Microsoft Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Bynder test kullanıcısı oluşturma](#creating-a-bynder-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Bynder sağlamak için.
4. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Britta Microsoft Azure AD çoklu oturum açma kullanmak Simon etkinleştirmek için.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-microsoft-azure-ad-sso"></a>Microsoft Azure AD SSO yapılandırma
Bu bölümde, Microsoft Azure AD SSO Klasik portalda etkinleştirin ve SSO Bynder uygulamanızda yapılandırın.

**Microsoft Azure AD SSO ile Bynder yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Klasik Portalı'ndaki üzerinde **Bynder** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** açmak için **yapılandırma çoklu oturum açma** iletişim.
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. Üzerinde **Bynder için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfa, uygulamada yapılandırmak istiyorsanız **IDP başlatılan modu**, aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. **İleri**’ye tıklayın.
4. Uygulamada yapılandırmak istiyorsanız **SP tarafından başlatılan modu** üzerinde **uygulama ayarlarını yapılandır** iletişim sayfa sonra tıklatıldığında **"Göster Gelişmiş ayarları (isteğe bağlı)"** ve enter **oturum üzerinde URL'si** tıklatıp **sonraki**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.getbynder.com/login/`
  2. **İleri**’ye tıklayın.
  
   >[!NOTE]
   >Bu öğretici oturum üzerinde URL'si için yalnızca bir placeholfer değerdir. Ortamınız için gerçek vlaue almak için Bynder başvurun.
   >

5. Üzerinde **çoklu oturum açma sırasında Bynder yapılandırma** sayfasında, aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Tıklatın **karşıdan meta veri**ve ardından dosyayı bilgisayarınıza kaydedin.
  2. **İleri**’ye tıklayın.
6. Uygulamanız için yapılandırılmış SSO almak için Bynder destek ekibinize başvurun. İndirilen meta veri dosyası ekleme ve bunların tarafında SSO'yu ayarlamak için Bynder ekibi ile paylaşın.
7. Klasik Portalı'ndaki tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][10]
8. Üzerinde **tek oturum açma onay** sayfasında, **tam**.  
   
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı Klasik portalda bir test kullanıcı oluşturmaktır.

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.
3. Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
  2. Kullanıcı adı **textbox**, türü **BrittaSimon**.
  3. **İleri**’ye tıklayın.
6. Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. İçinde **ad** metin kutusuna, türü **Britta**.  
  2. İçinde **Soyadı** metin kutusuna, türü, **Simon**. 
  3. İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.
  4. İçinde **rol** listesinde **kullanıcı**.
  5. **İleri**’ye tıklayın.
7. Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Değerini yazmak **yeni parola**.
   2. **Tamamla**’ya tıklayın.   

### <a name="create-a-bynder-test-user"></a>Bynder test kullanıcısı oluşturma
Bu bölümün amacı Britta Simon içinde Bynder adlı bir kullanıcı oluşturmaktır. Bynder yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümde, eylem öğe yok. Yeni bir kullanıcı henüz yoksa Bynder erişme denemesi sırasında oluşturulur.

>[!NOTE]
>Bir kullanıcı el ile oluşturmanız gerekiyorsa, Bynder Destek ekibine başvurun gerekir. 
> 

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın
Bu bölümün amacı Britta Bynder için kendi erişim vererek Azure SSO kullanılacak Simon için etkinleştirmektir.

   ![Kullanıcı atama][200]

**Bynder için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.
   
    ![Kullanıcı atama][201]
2. Uygulamalar listesinde **Bynder**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Üstteki menüde tıklatın **kullanıcılar**.
   
    ![Kullanıcı atama][203]
4. Kullanıcılar listesinden seçin **Britta Simon**.
5. Araç çubuğunda alt tıklatın **atamak**.
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin
Bu bölümün amacı erişim paneli kullanılarak Microsoft Azure AD SSO yapılandırmanızı test sağlamaktır.

Erişim paneli Bynder parçasında tıklattığınızda, otomatik olarak Bynder uygulamanıza açan.

## <a name="additional-resources"></a>Ek kaynaklar
* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
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
