---
title: "Öğretici: Azure Active Directory Tümleştirme Adobe Creative bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Adobe Creative bulut arasında."
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
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Öğretici: Adobe Creative bulut Azure Active Directory Tümleştirme

Bu öğreticide, bilgi Adobe Creative toointegrate bulut nasıl Azure Active Directory (Azure AD) ile.

Adobe Creative bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAdobe yaratıcı bulut sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooAdobe (çoklu oturum açma) yaratıcı bulut etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Adobe Creative bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Adobe Creative bulut çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Adobe Creative bulut hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Adobe Creative bulut hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Adobe Creative bulutun tooadd Adobe Creative bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Adobe Creative bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Adobe Creative bulut**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Merhaba Sonuçlar panelinde seçin **Adobe Creative bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmak ve Adobe Creative bulut "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Adobe Creative bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Adobe Creative bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Adobe Creative bulutta.

tooconfigure ve Adobe Creative bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Adobe Creative bulut test kullanıcısı oluşturma](#creating-an-adobe-creative-cloud-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Adobe Creative bulutta Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma, Adobe Creative bulut uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Adobe Creative bulutla hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde hello Azure Yönetim Portalı'nda **Adobe Creative bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Merhaba üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`https://www.okta.com/saml2/service-provider/<token>`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip. Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz. Bir kullanıcı toocreate el ile gerekiyorsa, toocontact hello Adobe Creative bulut destek ekibi gerekir.

4. Merhaba üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **SP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları** seçeneği

    b. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://adobe.com`

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Merhaba üzerinde **Adobe Creative bulut Yapılandırması** 'yi tıklatın **Adobe Creative bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Lütfen hello kopyalayın **SAML varlık kimliği** ve **SAML SSO hizmet URL'si** hızlı başvuru bölümünden.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour Adobe Creative bulut Kiracı.

8.  Çok Git**kimlik** sol gezinti bölmesinde hello ve etki alanınızı tıklatın. Merhaba aşağıdaki adımları gerçekleştirin **tek oturum yapılandırması gerekli** bölümü.

    ![Ayarları](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ayarları")

9. Tıklatın **Gözat** tooupload hello sertifika çok Azure AD'den indirilen**IDP sertifika**.

10. Merhaba, **IDP veren** hello değerini put textbox **SAML varlık kimliği** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.

11. Merhaba, **IDP oturum açma URL'si** hello değerini put textbox **SAML SSO hizmet URL'si** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.

12. Seçin **HTTP - yeniden yönlendirme** olarak **IDP bağlama**.

13. Seçin **e-posta adresi** olarak **kullanıcı oturum açma ayarı**.
 
14. Tıklatın **kaydetmek** düğmesi.

15. Merhaba Pano artık hello XML sunmak **"Meta veriler indirme"** dosya. Adobe EntityDescriptor URL ve AssertionConsumerService URL'sini içerir. Lütfen hello dosyasını açın ve hello Azure AD uygulaması yapılandırın.

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Kullanım hello EntityDescriptor değeri Adobe için sağlanan **tanımlayıcısı** hello üzerinde **uygulama ayarlarını yapılandır** iletişim.

    b. Kullanım hello AssertionConsumerService değeri Adobe için sağlanan **yanıt URL'si** hello üzerinde **uygulama ayarlarını yapılandır** iletişim.
 
### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Adobe Creative bulut test kullanıcısı oluşturma

Adobe Creative buluta sipariş tooenable Azure AD kullanıcıların toolog bunlar Adobe Creative bulutunu sağlanmalıdır.  
Adobe Creative bulut Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. Tooyour içinde Adobe Creative bulut şirket site yönetici olarak oturum açın.

2. Tıklatın **kişiler**.

    ![Kişiler](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "kişiler")

3. Tıklatın **davet kullanıcı**.

    ![Kullanıcıları davet](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "kullanıcıları davet et")

4. Merhaba üzerinde **kişileri davet** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Kişileri davet edin](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "kişileri davet edin")

    a. Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.
    
    b. Tıklatın **davet**.

    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooAdobe yaratıcı bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooAdobe yaratıcı bulut hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Adobe Creative bulut**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Adobe Creative bulut hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Adobe Creative bulut uygulaması almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
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