---
title: "Öğretici: Azure Active Directory Tümleştirme ile PlanMyLeave | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile PlanMyLeave arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Öğretici: Azure Active Directory Tümleştirme PlanMyLeave ile

Bu öğreticide, Azure Active Directory (Azure AD) ile PlanMyLeave tümleştirmek öğrenin.

PlanMyLeave Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- PlanMyLeave erişimi, Azure AD'de kontrol edebilirsiniz
- Otomatik olarak için PlanMyLeave (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme PlanMyLeave ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir PlanMyLeave çoklu oturum açma etkin abonelik


> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden PlanMyLeave ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-planmyleave-from-the-gallery"></a>Galeriden PlanMyLeave ekleme
Azure AD PlanMyLeave tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden PlanMyLeave eklemeniz gerekir.

**Galeriden PlanMyLeave eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.

    ![Uygulamalar][3]

4. Arama kutusuna **PlanMyLeave**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. Sonuçlar panelinde seçin **PlanMyLeave**ve ardından **Ekle** uygulama eklemek için düğmesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PlanMyLeave sınayın.

Tekli çalışmaya oturum için Azure AD PlanMyLeave karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının PlanMyLeave ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** PlanMyLeave içinde.

Yapılandırma ve Azure AD çoklu oturum açma PlanMyLeave ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[PlanMyLeave test kullanıcısı oluşturma](#creating-a-planmyleave-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı PlanMyLeave sağlamak için.
4. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma PlanMyLeave uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma ile PlanMyLeave yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure Yönetim Portalı'nda üzerinde **PlanMyLeave** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Üzerinde **çoklu oturum açma** iletişim sayfası olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. Üzerinde **PlanMyLeave etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. İçinde **tanımlayıcı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Lütfen bu gerçek değerlerin olmadığına dikkat edin. Bu değerler gerçek oturum üzerinde URL ve tanımlayıcıdır ile güncelleştirmeniz gerekir. Kişi [PlanMyLeave destek ekibi](mailto:support@planmyleave.com) bu değerleri almak için.

4. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**. Ardından **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. Üzerinde **PlanMyLeave yapılandırma** 'yi tıklatın **yapılandırma PlanMyLeave** açmak için **yapılandırma oturum açma** penceresi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. Farklı web tarayıcısı penceresinde PlanMyLeave Kiracı yönetici olarak oturum açın.

11. Git **sistem kurulumu**. Sonra da **güvenlik yönetimi** bölümünde **şirket SAML ayarları** .

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. Üzerinde **SAML ayarları** bölümünde, düzenleyici simgesine tıklayın.

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. Üzerinde **güncelleştirme SAML ayarlarını** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  İçinde **oturum açma URL'si** metin kutusuna, put değerini **SAML çoklu oturum açma hizmet URL'si** Azure AD uygulama yapılandırma penceresinden.

    b.  Açık, indirilen sertifika dosyasını Not Defteri'nde kopyalayın yalnızca içeriği---başlamak sertifika---ve---bitiş---'ın sertifikasını, Pano içine arasında ve kendisine yapıştırma **sertifika** metin kutusu.

    c. Ayarlama "**etkin**"için"**Evet**".

    d. **Kaydet** düğmesine tıklayın.



### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. İçinde **adı** metin kutusuna, türü **BrittaSimon**.

    b. İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 



### <a name="creating-a-planmyleave-test-user"></a>PlanMyLeave test kullanıcısı oluşturma

Bu bölümün amacı Britta Simon içinde PlanMyLeave adlı bir kullanıcı oluşturmaktır. PlanMyLeave yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümde, eylem öğe yok. Yeni bir kullanıcı henüz yoksa PlanMyLeave erişme denemesi sırasında oluşturulur.

> [!NOTE]
> Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [PlanMyLeave destek ekibi](mailto:support@planmyleave.com).



### <a name="assigning-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atama

Bu bölümde, Britta PlanMyLeave için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı atama][200] 

**PlanMyLeave için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **PlanMyLeave**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli PlanMyLeave parçasında tıklattığınızda, otomatik olarak PlanMyLeave uygulamanıza açan.


## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png