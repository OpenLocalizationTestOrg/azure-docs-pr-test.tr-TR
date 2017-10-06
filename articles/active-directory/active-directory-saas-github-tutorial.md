---
title: "Öğretici: Azure Active Directory Tümleştirme github | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve GitHub arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Öğretici: Azure Active Directory Tümleştirme github

Bu öğreticide, bilgi nasıl toointegrate GitHub Azure Active Directory'ye (Azure AD).

GitHub Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooGitHub sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooGitHub (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure GitHub ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir GitHub çoklu oturum açma etkin abonelik


> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. GitHub hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-github-from-hello-gallery"></a>GitHub hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme GitHub, tooadd GitHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd hello galeri Github'dan hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Github.com'u**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. Merhaba Sonuçlar panelinde seçin **GitHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı GitHub ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen github tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve github hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** github'da.

tooconfigure ve GitHub ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[GitHub test kullanıcısı oluşturma](#creating-a-GitHub-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir github'da, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma GitHub uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma github, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **GitHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. Merhaba üzerinde **GitHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://github.com/orgs/<entity-id>/sso`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Bu oturum açma hello gerçek URL ve tanımlayıcıdır değerlerle tooupdate var. Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz. Bu değerleri tooGitHub yönetici bölüm tooretrieve gidin. 

4. Merhaba üzerinde **kullanıcı öznitelikleri** bölümünde, select **kullanıcı tanımlayıcısı** user.mail olarak.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**. Ardından **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. Merhaba üzerinde **GitHub yapılandırma** 'yi tıklatın **yapılandırma GitHub** tooopen **yapılandırma oturum açma** penceresi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. Farklı web tarayıcısı penceresinde GitHub kuruluş sitenize yönetici olarak oturum açın.

12. Çok gidin**ayarları** tıklatıp **güvenlik**

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Merhaba denetleyin **etkinleştirmek SAML kimlik doğrulaması** hello çoklu oturum açma yapılandırma alanları ortaya kutusu. Ardından, Azure AD yapılandırmasına hello tek oturum açma değeri tooupdate hello tek oturum açma URL'si kullanın.

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Alanları aşağıdaki hello yapılandırın:

    a. **URL üzerinde oturum**: girin **SAML çoklu oturum açma hizmet URL'si** hello gelen **yapılandırma GitHub** Azure AD bölüm

    b. **Veren**: girin **SAML varlık kimliği** hello gelen **yapılandırma GitHub** Azure AD bölüm

    c. **Ortak sertifika**: açık hello "Sertifika başlayın" ve "Son SERTİFİKAYI" gibi bir not defteri ve kopyalama hello içerik Azure AD'den sertifika indirilir

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Tıklayın **Test SAML Yapılandırması** tooconfirm, hiçbir doğrulama hataları veya SSO sırasında hatalar.

    ![Ayarlar](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Tıklatın **Kaydet**

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 


### <a name="creating-a-github-test-user"></a>GitHub test kullanıcısı oluşturma

GitHub içine sipariş tooenable Azure AD kullanıcıların toolog bunların GitHub sağlanmalıdır.  
GitHub Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour GitHub şirket site yönetici olarak oturum açın.

2. Tıklatın **kişiler**.

    ![Kişiler](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "kişiler")

3. Tıklatın **davet üye**.

    ![Kullanıcıları davet](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "kullanıcıları davet et")

4. Merhaba üzerinde **davet üye** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    a. Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.

    ![Kişileri davet edin](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "kişileri davet edin")
    
    b. Tıklatın **Gönder davet**.

    ![Kişileri davet edin](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "kişileri davet edin")

    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooGitHub vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooGitHub hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Github.com'u**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba GitHub hello erişim paneli parçasında tıkladığınızda, oturum açma GitHub uygulama tooyour almanız gerekir. Bir kuruluş hesabı ancak gerek toolog sonra kişisel hesabınızla oturum.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
