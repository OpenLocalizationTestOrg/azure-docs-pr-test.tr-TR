---
title: "Öğretici: Azure Active Directory Tümleştirme Adobe Creative bulut ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Adobe Creative bulut arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Öğretici: Adobe Creative bulut Azure Active Directory Tümleştirme

Bu öğreticide, Adobe Creative bulut Azure Active Directory (Azure AD) ile tümleştirme öğrenin.

Adobe Creative bulut Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- Adobe Creative bulut erişimi olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına otomatik olarak Adobe Creative buluta (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Adobe Creative Bulutla yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Adobe Creative bulut çoklu oturum açma etkin abonelik

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden Adobe Creative bulut ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a>Galeriden Adobe Creative bulut ekleme
Azure AD Adobe Creative bulut tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Adobe Creative bulut eklemeniz gerekir.

**Adobe Creative bulut Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.

    ![Uygulamalar][3]

4. Arama kutusuna **Adobe Creative bulut**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Sonuçlar panelinde seçin **Adobe Creative bulut**ve ardından **Ekle** uygulama eklemek için düğmesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmak ve Adobe Creative bulut "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.

Tekli çalışmaya oturum için Azure AD ne karşılık gelen Adobe Creative bulutta bir kullanıcı için Azure AD içinde olduğu bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Adobe Creative bulutta arasında bir bağlantı ilişkisi kurulması gerekir.

Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Adobe Creative bulutta.

Yapılandırma ve Azure AD çoklu oturum açma Adobe Creative bulut ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Adobe Creative bulut test kullanıcısı oluşturma](#creating-an-adobe-creative-cloud-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Adobe Creative bulut sağlamak için.
4. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma, Adobe Creative bulut uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma Adobe Creative Bulutla yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure Yönetim Portalı'nda üzerinde **Adobe Creative bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. İçinde **tanımlayıcısı** metin değeri olarak yazın:`https://www.okta.com/saml2/service-provider/<token>`

    b. İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Lütfen bu gerçek değerlerin olmadığına dikkat edin. Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirmeniz gerekir. Burada dizesinin benzersiz değeri tanımlayıcıda kullanmanızı öneririz. Bir kullanıcı el ile oluşturmanız gerekiyorsa, Adobe Creative bulut Destek ekibine başvurun gerekir.

4. Üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **SP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Tıklayın **Göster Gelişmiş URL ayarları** seçeneği

    b. İçinde **oturum açma URL'si** metin değeri olarak yazın:`https://adobe.com`

5. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Üzerinde **Adobe Creative bulut Yapılandırması** 'yi tıklatın **Adobe Creative bulut yapılandırma** açmak için **yapılandırma oturum açma** penceresi. Lütfen kopyalayın **SAML varlık kimliği** ve **SAML SSO hizmet URL'si** hızlı başvuru bölümünden.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. Farklı web tarayıcısı penceresinde Adobe Creative bulut kiracınız yönetici olarak oturum.

8.  Git **kimlik** sol gezinti bölmesindeki ve etki alanınızı tıklatın. Üzerinde aşağıdaki adımları gerçekleştirin **tek oturum yapılandırması gerekli** bölümü.

    ![Ayarları](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ayarları")

9. Tıklatın **Gözat** için Azure AD'den indirilen sertifikayı karşıya yüklemek için **IDP sertifika**.

10. İçinde **IDP veren** metin kutusuna, put değerini **SAML varlık kimliği** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.

11. İçinde **IDP oturum açma URL'si** metin kutusuna, put değerini **SAML SSO hizmet URL'si** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.

12. Seçin **HTTP - yeniden yönlendirme** olarak **IDP bağlama**.

13. Seçin **e-posta adresi** olarak **kullanıcı oturum açma ayarı**.
 
14. Tıklatın **kaydetmek** düğmesi.

15. Pano artık XML sunacaktır **"Meta veriler indirme"** dosya. Adobe EntityDescriptor URL ve AssertionConsumerService URL'sini içerir. Lütfen dosyayı açın ve Azure AD uygulaması yapılandırın.

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Adobe için sağlanan EntityDescriptor değerini kullanmak **tanımlayıcısı** üzerinde **uygulama ayarlarını yapılandır** iletişim.

    b. Adobe için sağlanan AssertionConsumerService değerini kullanmak **yanıt URL'si** üzerinde **uygulama ayarlarını yapılandır** iletişim.
 
### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. İçinde **adı** metin kutusuna, türü **BrittaSimon**.

    b. İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Adobe Creative bulut test kullanıcısı oluşturma

Azure AD kullanıcıların Adobe Creative bulutunu oturum etkinleştirmek için bunlar Adobe Creative bulutunu sağlanmalıdır.  
Adobe Creative bulut söz konusu olduğunda, sağlama bir el ile bir görevdir.

**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**

1. Adobe Creative bulut şirket sitenize yönetici olarak oturum açın.

2. Tıklatın **kişiler**.

    ![Kişiler](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "kişiler")

3. Tıklatın **davet kullanıcı**.

    ![Kullanıcıları davet](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "kullanıcıları davet et")

4. Üzerinde **kişileri davet** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:

    ![Kişileri davet edin](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "kişileri davet edin")

    a. İçinde **e-posta** metin kutusuna, Britta Simon hesabı e-posta adresini yazın.
    
    b. Tıklatın **davet**.

    > [!NOTE]
    > Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce kendi hesabı onaylamak için bağlantıyı izleyin.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atama

Bu bölümde, Adobe Creative buluta kendi erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.

![Kullanıcı atama][200] 

**Britta Simon Adobe Creative buluta atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Adobe Creative bulut**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Adobe Creative bulut parçasında tıklattığınızda, otomatik olarak Adobe Creative bulut uygulamanıza açan.


## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png