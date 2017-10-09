---
title: "Öğretici: Azure Active Directory Tümleştirme ile FilesAnywhere | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FilesAnywhere arasında."
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
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>Öğretici: Azure Active Directory Tümleştirme FilesAnywhere ile

Bu öğreticide, bilgi nasıl toointegrate FilesAnywhere Azure Active Directory'ye (Azure AD).

FilesAnywhere Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooFilesAnywhere sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooFilesAnywhere (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure FilesAnywhere ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir FilesAnywhere çoklu oturum açma etkin abonelik


> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden FilesAnywhere ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-filesanywhere-from-hello-gallery"></a>Merhaba Galerisi'nden FilesAnywhere ekleme
Azure AD'ye tooconfigure hello tümleştirme FilesAnywhere, tooadd FilesAnywhere hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd FilesAnywhere hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **FilesAnywhere**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. Merhaba Sonuçlar panelinde seçin **FilesAnywhere**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FilesAnywhere sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen FilesAnywhere içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı FilesAnywhere hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** FilesAnywhere içinde.

tooconfigure ve FilesAnywhere ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[FilesAnywhere test kullanıcısı oluşturma](#creating-a-filesanywhere-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir FilesAnywhere içinde Britta Simon biri.
3. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
4. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FilesAnywhere uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile FilesAnywhere, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **FilesAnywhere** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. Merhaba üzerinde **FilesAnywhere etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu**:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    a. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> Lütfen bu hello değerini not edin **215** olan bir **ClientID** ve yalnızca bir örnektir. Tooreplace ihtiyacınız hello gerçek ClientID değeri ile.

4. Merhaba üzerinde **FilesAnywhere etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    a. Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları** seçeneği

    b. Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello gerçek oturum üzerinde URL'si ve yanıt URL'si ile bu değerlere sahip. Kişi [FilesAnywhere destek ekibi](mailto:support@FilesAnywhere.com) tooget bu değerleri. 

5. FilesAnywhere yazılım uygulama hello SAML onaylar belirli bir biçimde bekler. Lütfen bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    Ne zaman, kullanıcılar işaretleriyle yukarı hello değeri elde FilesAnywhere hello **ClientID** özniteliğini [FilesAnywhere takım](mailto:support@FilesAnywhere.com). FilesAnywhere tarafından sağlanan hello benzersiz değer ile tooadd hello "İstemci kimliği" özniteliğine sahip. Yukarıda gösterilen bu öznitelikler gereklidir.
    > [!NOTE] 
    > Lütfen bu hello değerini not edin **2331** , **ClientID** yalnızca bir örnektir. Tooprovide hello gerçek değer gerekir.


6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ---------------| --------------- |    
    | istemci kimliği | *"uniquevalue"* |

    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. Tıklatın **Tamam**

7. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. Merhaba üzerinde **FilesAnywhere yapılandırma** 'yi tıklatın **yapılandırma FilesAnywhere** tooopen **yapılandırma oturum açma** penceresi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. tooget SSO yapılandırması tamamlandı FilesAnywhere uçtaki kişi, uygulamanız için [FilesAnywhere destek ekibi](mailto:support@FilesAnywhere.com) ve indirilen hello SAML belirteç sertifika ve çoklu oturum açma (SSO) URL imzalama verin.

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 



### <a name="creating-a-filesanywhere-test-user"></a>FilesAnywhere test kullanıcısı oluşturma

Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler. 


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooFilesAnywhere vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooFilesAnywhere hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **FilesAnywhere**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba FilesAnywhere hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour FilesAnywhere uygulama almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
