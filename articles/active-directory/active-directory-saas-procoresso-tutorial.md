---
title: "Öğretici: Azure Active Directory Tümleştirme Procore SSO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Procore SSO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Öğretici: Azure Active Directory Tümleştirme Procore SSO

Bu öğreticide, bilgi nasıl toointegrate Procore SSO Azure Active Directory'ye (Azure AD).

Procore SSO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooProcore SSO sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooProcore SSO (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Ön koşullar

tooconfigure Procore SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Procore SSO çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Procore SSO ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-procore-sso-from-hello-gallery"></a>Merhaba Galerisi'nden Procore SSO ekleme
Azure AD'ye tooconfigure hello tümleştirme Procore sso'nun tooadd Procore SSO hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd hello galerisinden Procore SSO hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Procore SSO**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. Merhaba Sonuçlar panelinde seçin **Procore SSO**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Procore "Britta Simon" adlı bir test kullanıcı tabanlı SSO ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Procore SSO tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Procore SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Procore sso.

tooconfigure ve Procore SSO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Procore SSO test kullanıcısı oluşturma](#creating-a-procore-sso-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Procore SSO Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Procore SSO uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Procore SSO hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **Procore SSO** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. Merhaba üzerinde **Procore SSO etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Procore SSO yapılandırma** 'yi tıklatın **yapılandırma Procore SSO** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **Procore SSO** tarafı, yönetici olarak oturum açma tooyour procore şirket site.

8. Merhaba araç kutusu açılır, aşağı, tıklayın **yönetici** tooopen hello SSO Ayarları sayfası.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Merhaba kutuları olarak Yapıştır hello değerleri aşağıdaki - açıklanan

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. Merhaba, **tek oturum üzerinde veren URL'si** kutusunda, SAML varlık kimliği kopyalanan hello Azure portal ' hello yapıştırın.

    b. Merhaba, **hedef URL üzerinde SAML oturum** kutusunda, SAML çoklu oturum açma hizmet URL'si kopyalanan hello Azure portal ' hello yapıştırın.

    c. Şimdi hello açmak **meta veri XML** hello Azure portal ve kopyalama hello sertifikası adlı hello etiketinde yukarıda indirilen **X509Certificate**. Yapıştır hello kopyaladığınız değeri hello **çoklu oturum açma x509 sertifika** kutusu.

10. Tıklayın **değişiklikleri kaydetmek**.

11. Bu ayarları sonra toosend hello ihtiyaç duyduğu **etki alanı adı** (örneğin **contoso.com**) hangi Procore toohello günlüğü aracılığıyla [Procore destek ekibi](https://support.procore.com/) ve bunlar Bu etki alanı için Federasyon SSO etkinleştirin.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-procore-sso-test-user"></a>Procore SSO test kullanıcısı oluşturma

Lütfen başlangıç adımları toocreate Procore test kullanıcısı aşağıda kendi tarafında izleyin.

1. Yönetici olarak oturum açma tooyour procore şirket sitesi.  

2. Merhaba araç kutusu açılır, aşağı, tıklayın **Directory** tooopen hello şirket dizin sayfası.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Tıklayın **bir kişi Ekle** seçeneği tooopen hello form ve girin seçenekler - gerçekleştirin

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. Merhaba, **ad** metin kutusuna, türü kullanıcının ilk adını gibi **Britta**.

    b. Merhaba, **Soyadı** metin kutusuna, türü kullanıcının soyadını gibi **Simon**.

    c. Merhaba, **e-posta adresi** türü kullanıcının e-posta adresi metin kutusuna, ister  **BrittaSimon@contoso.com** .

    d. Seçin **izin şablonu** olarak **izin şablonu daha sonra uygulamak**.

    e. **Oluştur**'a tıklayın.

4. Denetleyin ve hello kişi yeni eklenen için güncelleştirme hello ayrıntıları.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Tıklayın **Kaydet ve Gönder daveti** (posta yoluyla bir davet gerekliyse) veya **kaydetmek** (doğrudan Kaydet) toocomplete hello kullanıcı kaydı.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooProcore SSO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooProcore SSO hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Procore SSO**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın. Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586). Merhaba Procore SSO hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Procore SSO uygulaması almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

