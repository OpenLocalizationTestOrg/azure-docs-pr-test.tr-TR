---
title: "Öğretici: Azure Active Directory Tümleştirme ile Pingboard | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Pingboard arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Öğretici: Azure Active Directory Tümleştirme Pingboard ile

Bu öğreticide, bilgi nasıl toointegrate Pingboard Azure Active Directory'ye (Azure AD).

Pingboard Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooPingboard sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooPingboard (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Pingboard ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Pingboard çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Pingboard ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-pingboard-from-hello-gallery"></a>Merhaba Galerisi'nden Pingboard ekleme
Azure AD'ye tooconfigure hello tümleştirme Pingboard, tooadd Pingboard hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Pingboard hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Pingboard**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. Merhaba Sonuçlar panelinde seçin **Pingboard**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Pingboard sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Pingboard içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Pingboard hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Pingboard içinde.

tooconfigure ve Pingboard ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Pingboard test kullanıcısı oluşturma](#creating-a-pingboard-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Pingboard içinde Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Pingboard uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Pingboard, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **Pingboard** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. Merhaba üzerinde **Pingboard etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`http://<entity-id>.pingboard.com/sp`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip. Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz. Kişi [Pingboard istemci destek ekibi](https://support.pingboard.com/) tooget bu değerleri. 

4. Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`http://<sub-domain>.pingboard.com/sign_in`
     
5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure SSO Pingboard tarafında, yeni bir tarayıcı penceresi açın ve tooyour Pingboard hesap oturum. Üzerinde çoklu oturum açma yukarı Pingboard yönetici tooset olması gerekir.

8. Merhaba üst menüsünden seçin **uygulamaları > tümleştirmeler**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  Merhaba üzerinde **tümleştirmeler** sayfasında, hello Bul **"Azure Active Directory"** döşeme ve tıklatın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. Tıklatın izleyen hello kalıcı olarak **"Yapılandırma"**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. Sayfa aşağıdaki hello üzerinde "Azure SSO tümleştirme etkin olduğunu." fark edeceksiniz. Açık hello indirilen bir not defteri ve Yapıştır hello içerik meta veri XML dosyasında **IDP meta verileri**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. Merhaba dosya doğrulanacak ve her şey doğruysa, çoklu oturum açma şimdi etkinleştirilir

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-pingboard-test-user"></a>Pingboard test kullanıcısı oluşturma

Pingboard içine sipariş tooenable Azure AD kullanıcıların toolog bunların Pingboard sağlanmalıdır.  
Pingboard Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour Pingboard şirket site yönetici olarak oturum açın.

2. Tıklatın **"Çalışan Ekle"** düğmesini **Directory** sayfası.

    ![Çalışanı ekleyin](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. Merhaba üzerinde **"Çalışan Ekle"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin.

    ![Kişileri davet edin](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. Merhaba, **tam adı** metin kutusuna, tür Britta Simon hello tam adı.

    b. Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.

    c. Merhaba, **iş unvanı** metin kutusuna, Britta Simon türü hello iş unvanı.

    d. Merhaba, **konumu** açılan listesinde, Britta Simon select başlangıç konumu.
    
    e. **Ekle**'ye tıklayın.   

4. Bir onay ekranı tooconfirm hello eklenmesi kullanıcı gelecektir.
    
    ![Onayla](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooPingboard vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooPingboard hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Pingboard**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Pingboard hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Pingboard uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
