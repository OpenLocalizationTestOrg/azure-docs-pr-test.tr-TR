---
title: "Öğretici: Azure Active Directory Tümleştirme ile isteğe bağlı Proofpoint | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Proofpoint arasında isteğe bağlı yapılandırma konusunda bilgi edinin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a>Öğretici: Azure Active Directory Tümleştirme ile Proofpoint isteğe bağlı

Bu öğreticide, Azure Active Directory (Azure AD) ile Proofpoint isteğe bağlı tümleştirme öğrenin.

İsteğe bağlı Proofpoint Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- İsteğe bağlı Proofpoint erişimi, Azure AD'de kontrol edebilirsiniz
- Otomatik olarak Proofpoint isteğe bağlı (çoklu oturum açma) için Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

İsteğe bağlı Proofpoint ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- İsteğe bağlı çoklu oturum açma etkin abonelik üzerinde Proofpoint

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden isteğe bağlı Proofpoint ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a>Galeriden isteğe bağlı Proofpoint ekleme
Azure AD ile isteğe bağlı Proofpoint tümleştirmesini yapılandırmak için Proofpoint isteğe bağlı Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.

**Proofpoint Galeriden isteğe bağlı olarak eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.

    ![Uygulamalar][3]

4. Arama kutusuna **Proofpoint isteğe bağlı**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. Sonuçlar panelinde seçin **isteğe bağlı Proofpoint**ve ardından **Ekle** uygulama eklemek için düğmesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı isteğe bağlı Proofpoint ile test etme

Tekli çalışmaya oturum için Azure AD ne karşılık gelen Proofpoint isteğe bağlı olarak bir kullanıcı için Azure AD içinde olduğu bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının ve isteğe bağlı Proofpoint ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.

Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Proofpoint isteğe bağlı olarak.

Yapılandırmak ve Azure AD çoklu oturum açma ile isteğe bağlı Proofpoint sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Bir Proofpoint üzerinde isteğe bağlı test kullanıcısı oluşturma](#creating-a-proofpoint-on-demand-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı isteğe bağlı Proofpoint sağlamak için.
4. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, Proofpoint isteğe bağlı uygulama üzerinde yapılandırın.

**İsteğe bağlı Proofpoint ile Azure AD çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında üzerinde **Proofpoint isteğe bağlı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
  
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. Üzerinde **Proofpoint isteğe bağlı etki alanı ve URL'ler hakkında** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    a.In **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<hostname>.pphosted.com/ppssamlsp_hostname`

    b. İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<hostname>.pphosted.com/ppssamlsp`

    c.  İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri gerçek tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin. Kişi [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services) bu değerleri almak için. 

4. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. Üzerinde **isteğe bağlı yapılandırma Proofpoint** 'yi tıklatın **isteğe bağlı yapılandırma Proofpoint** açmak için **yapılandırma oturum açma** penceresi. Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. Çoklu oturum açma yapılandırmak için **isteğe bağlı Proofpoint** yan, indirilen göndermek için ihtiyacınız **Certificate(Base64)**,**SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** için [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services).

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!  Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. Bu değerler gerçek değildir. Bu değerleri gerçek ile güncelleştirme
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    a. İçinde **adı** metin kutusuna, türü **Britta Simon**.

    b. İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.

    c. Seçin **Göster parola** ve değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a>Bir Proofpoint üzerinde isteğe bağlı test kullanıcısı oluşturma

Bu bölümde, Britta Simon Proofpoint isteğe bağlı olarak adlandırılan bir kullanıcı oluşturun. Çalışmak [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services) isteğe bağlı bir platformda Proofpoint kullanıcılar eklemek için.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atama

Bu bölümde, isteğe bağlı Proofpoint için erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.

![Kullanıcı atama][200] 

**İsteğe bağlı Proofpoint Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Proofpoint isteğe bağlı**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Tıkladığınızda **Proofpoint isteğe bağlı** döşeme erişim panelinde oturumunuz otomatik olarak isteğe bağlı uygulama üzerinde Proofpoint için.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).  

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

