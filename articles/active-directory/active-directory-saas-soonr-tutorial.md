---
title: "Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Soonr çalışma arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma

Bu öğreticinin amacı Soonr çalışma alanına Azure Active Directory (Azure AD) ile tümleştirme Göster sağlamaktır.  
Soonr çalışma alanına Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- Soonr çalışma alanına erişimi olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına otomatik olarak (çoklu oturum açma) Soonr çalışma alanına açan kullanıcılarınıza etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Soonr çalışma alanınız ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Soonr çalışma alanı çoklu oturum açma etkin abonelik


> [!NOTE] 
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin amacı, Azure AD çoklu oturum açma bir test ortamında test etmenizi hale getirmektir.  
Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden Soonr çalışma alanına ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-soonr-workplace-from-the-gallery"></a>Galeriden Soonr çalışma alanına ekleme
Azure AD Soonr çalışma alanına tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Soonr çalışma alanına eklemeniz gerekir.

**Galeriden Soonr çalışma alanına eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**. 

    ![Active Directory][1]

2. Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.

3. Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.

    ![Uygulamalar][2]

4. Tıklatın **Ekle** sayfanın sonundaki.

    ![Uygulamalar][3]

5. Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.
 
    ![Uygulamalar][4]

6. Arama kutusuna **Soonr çalışma alanına**.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Sonuçlar bölmesinde seçin **Soonr çalışma alanına**ve ardından **tam** uygulama eklemek için.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümün amacı nasıl yapılandırılacağı ve Azure AD çoklu oturum açma Soonr çalışma alanı ile test göstermek için "Britta Simon" adlı bir test kullanıcı dayalıdır.

Tekli çalışmaya oturum için Azure AD Azure AD'de bir kullanıcıya karşılık gelen kullanıcı Soonr çalışma nedir bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Soonr çalışma arasında bir bağlantı ilişkisi kurulması gerekir.  

Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Soonr çalışma.

Yapılandırma ve Azure AD çoklu oturum açma Soonr çalışma alanı ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Soonr çalışma alanına test kullanıcısı oluşturma](#creating-a-soonr-workplace-test-user)**  - Azure AD gösterimini her için bağlantılı Soonr çalışma Britta Simon, karşılık gelen sağlamak için.
4. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma Klasik portalında etkinleştirin ve çoklu oturum açma Soonr çalışma alanına uygulamanızda yapılandırın.


**Azure AD çoklu oturum açma Soonr çalışma alanınız ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure Klasik portalında üzerinde **Soonr çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** açmak için **yapılandırma çoklu oturum açma** iletişim.

    ![Çoklu oturum açmayı yapılandırın][6] 

2. Üzerinde **Soonr çalışma alanına oturum açmasını nasıl istiyorsunuz** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. **İleri**’ye tıklayın.

    > [!NOTE] 
    > Lütfen bu gerçek değer olmadığını unutmayın. Bu değer gerçek oturum üzerinde URL ile güncelleştirmeniz gerekir. Bu değer almak için Soonr çalışma alanına Destek ekibine başvurun.

4. Üzerinde **çoklu oturum açma Soonr yerindeki yapılandırma** sayfasında, **karşıdan meta veri** ve dosyayı bilgisayarınıza kaydedin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. Uygulamanız için yapılandırılmış SSO almak için Soonr çalışma alanına destek ekibinize başvurun ve aşağıdaki verin: 

    • İndirilen **meta veri** dosyası

    • **Veren URL'si**

    • **SAML SSO URL'si**

    • **Tek oturum kapatma hizmeti URL'si**

    >[!NOTE]
    >Bu uygulamanın yerine geçen <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask çalışma alanına</a> ve başvuruda bulunabilir <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">bu</a> öğretici Azure AD ile uygulama yapılandırma.
   
6. Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **sonraki**.

    ![Azure AD çoklu oturum açma][10]

7. Üzerinde **tek oturum açma onay** sayfasında, **tam**.  
  
    ![Azure AD çoklu oturum açma][11]



### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı Klasik Azure portalında bir test kullanıcı oluşturmaktır.  

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.

3. Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.

    b. Kullanıcı adı **textbox**, türü **BrittaSimon**.

    c. **İleri**’ye tıklayın.

6.  Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. İçinde **ad** metin kutusuna, türü **Britta**.  

    b. İçinde **Soyadı** metin kutusuna, türü, **Simon**.

    c. İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.

    d. İçinde **rol** listesinde **kullanıcı**.

    e. **İleri**’ye tıklayın.

7. Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Değerini yazmak **yeni parola**.

    b. **Tamamla**’ya tıklayın.   



### <a name="creating-a-soonr-workplace-test-user"></a>Soonr çalışma alanına test kullanıcısı oluşturma

Bu bölümün amacı Britta Simon Soonr çalışma alanında adlı bir kullanıcı oluşturmaktır. Platform bir kullanıcı oluşturmak için Soonr çalışma alanına destek ekibi ile çalışın. Soonr ile destek bileti yükseltebilirsiniz <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">burada</a>.


### <a name="assigning-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atama

Bu bölümün amacı Britta Soonr çalışma alanına her erişim vererek, Azure çoklu oturum açma kullanılacak Simon için etkinleştirmektir.

![Kullanıcı atama][200] 

**Britta Simon Soonr çalışma alanına atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Soonr çalışma alanına**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. Üstteki menüde tıklatın **kullanıcılar**.

    ![Kullanıcı atama][203] 

1. Kullanıcılar listesinden seçin **Britta Simon**.

2. Araç çubuğunda alt tıklatın **atamak**.

    ![Kullanıcı atama][205]



### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.  
Erişim paneli Soonr çalışma alanına parçasında tıklattığınızda, otomatik olarak Soonr çalışma alanına uygulamanıza açan.


## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
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
