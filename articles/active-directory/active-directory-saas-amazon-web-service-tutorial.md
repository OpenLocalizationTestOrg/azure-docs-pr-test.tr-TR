---
title: "Öğretici: Azure Active Directory Tümleştirme Amazon Web Hizmetleri (AWS) ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Amazon Web Hizmetleri (AWS) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Öğretici: Azure Active Directory Tümleştirme Amazon Web Hizmetleri (AWS)

Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile Amazon Web Hizmetleri (AWS).

Amazon Web Hizmetleri (AWS) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAmazon Web Hizmetleri (AWS) sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooAmazon (çoklu oturum açma) Web Hizmetleri (AWS) etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Amazon Web Hizmetleri (AWS) ile tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Amazon Web Hizmetleri (AWS) çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Amazon Web Hizmetleri (AWS) hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Amazon Web Hizmetleri (AWS) hello Galerisi'nden ekleme
tooconfigure hello tümleştirmeye Amazon Web Hizmetleri (AWS) Azure AD, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Amazon Web Hizmetleri (AWS) gerekir.

**tooadd hello galerisinden Amazon Web Hizmetleri (AWS) hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Amazon Web Hizmetleri (AWS)**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. Merhaba Sonuçlar panelinde seçin **Amazon Web Hizmetleri (AWS)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Amazon Web Hizmetleri ("Britta Simon" adlı bir test kullanıcı tabanlı AWS) test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Amazon Web Hizmetleri (AWS) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Amazon Web Hizmetleri (AWS) arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Amazon Web Hizmetleri (AWS).

tooconfigure ve test Amazon Web Hizmetleri (AWS) ile Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Amazon Web Hizmetleri test kullanıcısı oluşturma](#creating-an-amazon-web-services-test-user)**  -toohave karşılık gelen, Britta Simon Amazon Web Hizmetleri (AWS) her bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Amazon Web Hizmetleri (AWS) uygulamanızda yapılandırın.

**Amazon Web Hizmetleri (AWS) ile tooconfigure Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde hello Azure Portal'ın **Amazon Web Hizmetleri (AWS)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. Merhaba üzerinde **Amazon Web Hizmetleri (AWS) etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Merhaba Amazon Web Hizmetleri (AWS) yazılım uygulaması hello SAML onaylar belirli bir biçimde bekliyor. Lütfen bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı  | Öznitelik değeri | Namespace |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | User.userPrincipalName | https://aws.Amazon.com/SAML/Attributes |
    | Rol            | User.assignedroles |  https://aws.Amazon.com/SAML/Attributes |
    
    >[!TIP]
    >Azure AD toofetch AWS Konsolu tüm hello rollerden sağlama tooconfigure hello kullanıcı gerekir. Lütfen aşağıdaki adımları sağlama hello bakın.

    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri. Yukarıda verilen Hello Namespace değerini ekleyin.
    
    d. **Tamam**’a tıklayın.

7. Tıklatın **kaydetmek** düğmesini Azure toosave hello ayarları.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. Farklı bir tarayıcı penceresinde yönetici olarak oturum açma tooyour Amazon Web Hizmetleri (AWS) şirket site.

9. Tıklatın **konsol giriş**.
   
    ![Çoklu oturum açmayı yapılandırın][11]

10. Tıklatın **IAM** gelen **güvenlik, Identity & Uyumluluk** hizmet.
   
    ![Çoklu oturum açmayı yapılandırın][12]

11. Tıklatın **kimlik sağlayıcıları**ve ardından **oluşturma sağlayıcısı**.
   
    ![Çoklu oturum açmayı yapılandırın][13]

12. Merhaba üzerinde **yapılandırma sağlayıcısı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırın][14]
 
    a. Olarak **sağlayıcı türü**seçin **SAML**.

    b. Merhaba, **sağlayıcı adı** metin kutusuna, bir sağlayıcı adı yazın (örneğin: *WAAD*).

    c. tooupload, indirilen meta veri dosyası tıklatın **Dosya Seç**.

    d. Tıklatın **sonraki adım**.

13. Merhaba üzerinde **sağlayıcısı bilgilerini doğrulayın** iletişim sayfasında, tıklatın **oluşturma**. 
    
    ![Çoklu oturum açmayı yapılandırın][15]

14. Tıklatın **rolleri**ve ardından **yeni rol oluşturma**. 
    
    ![Çoklu oturum açmayı yapılandırın][16]

15. Merhaba üzerinde **ayarlamak rol adı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin: 
    
    ![Çoklu oturum açmayı yapılandırın][17] 

    a. Merhaba, **rol adı** metin kutusuna, bir rol adı yazın (örneğin: *TestUser*). 

    b. Tıklatın **sonraki adım**.

16. Merhaba üzerinde **rol türünü seç** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin: 
    
    ![Çoklu oturum açmayı yapılandırın][18] 

    a. Seçin **kimlik sağlayıcısı erişim için rol**. 

    b. Merhaba, **Grant Web çoklu oturum açma (WebSSO) erişim tooSAML sağlayıcıları** 'yi tıklatın **seçin**.

17. Merhaba üzerinde **kurmak güven** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:  
    
    ![Çoklu oturum açmayı yapılandırın][19] 

    a. SAML sağlayıcısı, daha önce oluşturmuş hello SAML sağlayıcısını seçin (örneğin: *WAAD*)
  
    b. Tıklatın **sonraki adım**.

18. Merhaba üzerinde **doğrulayın rol güven** iletişim kutusunda, tıklatın **sonraki adım**.
    
    ![Çoklu oturum açmayı yapılandırın][32]

19. Merhaba üzerinde **ekleme İlkesi** iletişim kutusunda, tıklatın **sonraki adım**.
    
    ![Çoklu oturum açmayı yapılandırın][33]

20. Merhaba üzerinde **gözden geçirme** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın][34]
 
    a. Tıklatın **rolü oluşturma**.

    b. Gerektiğinde kadar rolleri oluşturun ve bunları toohello kimlik sağlayıcısı eşleyin.

21. Şimdi hello kullanıcı toofetch hazırlama AWS tüm hello rollerini yapılandırma

    a. Kök hesabınızla Hello AWS konsol oturum açma

    b. Merhaba sağ üst köşedeki adınıza tıklayın ve ardından hello tıklayın **My güvenlik kimlik bilgileri** seçeneği. Bu ekran yukarı bir uyarı iletisi açar. Merhaba düğmesini **güvenlik kimlik bilgileri** düğmesini toopass Merhaba ekranında.
        
       ![Çoklu oturum açmayı yapılandırın][36]

       ![Çoklu oturum açmayı yapılandırın][37]

    c. Merhaba erişim tuşları bölümüne tıklatın hello **yeni erişim anahtarı oluştur** düğmesi. Bu, hello erişim anahtarı kimliği ve bir belirteç değeri oluşturur.
    
       ![Çoklu oturum açmayı yapılandırın][38]

    d. Bu değerleri kopyalayın ve böylece bu kaybetmeyin Ayrıca, indirin.

    e. Merhaba Amazon Web Hizmetleri (AWS) uygulama tümleştirmesi sayfasında hello Azure Portal'ı tıklatın **sağlama**.
        
       ![Çoklu oturum açmayı yapılandırın][35]

    f. Merhaba hazırlama modunu çok ayarlamak**otomatik**
        
       ![Çoklu oturum açmayı yapılandırın][39]

    g. Merhaba, şimdi **clientsecret** ve **gizli belirteci** AWS konsolundan kopyaladığınız hello karşılık gelen değerler yapıştırın.
    
    h. Merhaba tıklayabilirsiniz **Bağlantıyı Sına** düğmesini tootest hello bağlantısı. Başarılı olduktan sonra Bağlayıcıyı sağlamadan hello başlatabilirsiniz.
       
       ![Çoklu oturum açmayı yapılandırın][40]

    ı. Şimdi hello sağlama durumu çok etkinleştirmek**üzerinde**. Bu, hello uygulamadan hello rolleri getiriliyor başlatır.

       ![Çoklu oturum açmayı yapılandırın][41]

    > [!NOTE]
    > Azure AD sağlama hizmeti çalıştığında AWS bazı zaman toosync hello rollerden sonra her. Tüm hello kimlik sağlayıcısı AWS rolleri Azure AD ile bağlı ve hello uygulama toousers ya da grupları atarken kullanabilmek için görmeniz gerekir.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Amazon Web Hizmetleri test kullanıcısı oluşturma

TooAmazon Web Hizmetleri (AWS) içinde sipariş tooenable Azure AD kullanıcıların toolog bunlar Amazon Web Hizmetleri (AWS) içine sağlanmalıdır. Merhaba durumda Amazon Web Hizmetleri (AWS), sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Amazon Web Hizmetleri (AWS)** yönetici olarak şirket site.

2. Merhaba tıklatın **konsol giriş** simgesi. 
   
    ![Çoklu oturum açmayı yapılandırın][11]

3. Kimlik'i tıklatın ve erişim yönetimi. 
   
    ![Çoklu oturum açmayı yapılandırın][28]

4. Hello Pano, tıklatın **kullanıcılar**ve ardından **Create New Users**. 
   
    ![Çoklu oturum açmayı yapılandırın][29]

5. Merhaba kullanıcı oluştur iletişim kutusunda hello aşağıdaki adımları gerçekleştirin: 
   
    ![Çoklu oturum açmayı yapılandırın][30]   
    
    a. Merhaba, **kullanıcı adlarını girin** metin kutuları, Azure AD'de Brita Simon'ın kullanıcı adı (userprincipalname) yazın.

    b. Tıklatın **oluşturun.**
        
### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooAmazon Web Hizmetleri (AWS) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooAmazon Web Hizmetleri (AWS), hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Amazon Web Hizmetleri (AWS)**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Üzerinde **rolü Seç** sekmesi, hello kullanıcı için uygun rolü seçin hello. Bu rolleri hello rol adı ve kimlik sağlayıcısı adı ile gösterilir. Bu şekilde, AWS hello rollerden kolayca tanımlayabilirsiniz.

8. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Amazon Web Hizmetleri (AWS) hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak oturum açma Amazon Web Hizmetleri (AWS) uygulama tooyour almanız gerekir. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
