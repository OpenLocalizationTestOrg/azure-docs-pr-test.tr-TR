---
title: "Öğretici: Azure Active Directory Tümleştirme ile Teamphoria | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Teamphoria arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Öğretici: Azure Active Directory Tümleştirme Teamphoria ile

Bu öğreticide, bilgi nasıl toointegrate Teamphoria Azure Active Directory'ye (Azure AD).

Teamphoria Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooTeamphoria sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooTeamphoria (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Ön koşullar

tooconfigure Teamphoria ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Teamphoria çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Teamphoria ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-teamphoria-from-hello-gallery"></a>Merhaba Galerisi'nden Teamphoria ekleme
Azure AD'ye tooconfigure hello tümleştirme Teamphoria, tooadd Teamphoria hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Teamphoria hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Teamphoria**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. Merhaba Sonuçlar panelinde seçin **Teamphoria**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Teamphoria sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Teamphoria içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Teamphoria hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Teamphoria içinde.

tooconfigure ve Teamphoria ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Teamphoria test kullanıcısı oluşturma](#creating-a-teamphoria-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Teamphoria içinde Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Teamphoria uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Teamphoria, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **Teamphoria** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. Merhaba üzerinde **Teamphoria etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello URL'si:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello ile bu değerlere sahip gerçek oturum açma URL'si. Kişi [Teamphoria istemci destek ekibi](https://www.teamphoria.com/) tooget hello oturum açma URL'si. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Teamphoria yapılandırma** 'yi tıklatın **yapılandırma Teamphoria** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **Teamphoria** tarafı, yönetici olarak oturum açma tooyour Teamphoria uygulama.

8. Çok Git**yönetici ayarları** seçeneği hello sol araç ve yapılandırma sekmesini üzerinde hello hello altında **tek oturum açma** tooopen hello SSO yapılandırma penceresi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Tıklayın **yeni kimlik sağlayıcı Ekle** hello sağ üst köşedeki tooopen hello formunda SSO hello ayarlarını ekleme seçeneği.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Aşağıdaki - açıklandığı gibi hello alanlarında Hello ayrıntılarını girin

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **GÖRÜNEN adı** : hello Yönetim sayfasında hello eklentisi hello görünen adını girin.

    b. **DÜĞME adı** : SSO oturum açmayı için hello oturum açma sayfasında görüntüler hello sekmesini hello adı.

    c. **Sertifika** : açık hello sertifika önceki hello Not Defteri'nde, kopyalama Merhaba içeriğine hello Azure portalı aynı indirdiğiniz ve buraya hello kutusuna yapıştırın.

    d. **Giriş noktası** : Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** önceki form hello Azure portal kopyalanır.

    e. Merhaba seçeneği çok geçiş**ON** ve tıklayın **KAYDETMEK**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-teamphoria-test-user"></a>Teamphoria test kullanıcısı oluşturma

Teamphoria içine sipariş tooenable Azure AD kullanıcıların toolog bunların Teamphoria sağlanmalıdır. Teamphoria Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour Teamphoria şirket site yönetici olarak oturum açın.

2. Tıklayın **yönetici** ayarları hello sol araç çubuğunda ve hello altında **Yönet** tıklatın sekmesi **kullanıcılar** tooopen hello Yönetim sayfası kullanıcılar için.

    ![Çalışanı ekleyin](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Tıklatın hello üzerinde **el ile davet** seçeneği.

    ![Kişileri davet edin](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. Bu sayfada, eylemi gerçekleştirin. 
    
    ![Kişileri davet edin](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. Merhaba, **e-posta adresi** metin kutusuna, hello **e-posta adresi** BrittaSimon biri.

    b. Merhaba, **ad** metin kutusuna, türü **Britta**.

    c. Merhaba, **SOYADI** metin kutusuna, türü **Simon**.

    d. Tıklatın **davet 1 kullanıcı**. Kullanıcı hello sistemde oluşturulan tooaccept hello davet tooget gerekir.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooTeamphoria vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooTeamphoria hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Teamphoria**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın. Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

